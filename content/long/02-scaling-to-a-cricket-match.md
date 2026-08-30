# Scaling to a Cricket Match: The Four Workloads Hiding Inside "1 Million Users"

*Part of a "learning in public" series on building a Hotstar-scale streaming
system from first principles.*

## The question that reframed everything for me

Once I had control plane and data plane separated (see [part
1](01-control-plane-vs-data-plane.md)), the next question was: what actually
happens when 10 million people watch the same cricket match?

My first instinct was to think of this as "10 million times normal load."
That instinct is wrong, and figuring out why was the most useful thing I
learned this week.

## Load isn't one number

```
1M VIEWERS
    │
    ├── Control traffic  → APIs
    ├── Playback traffic → CDN
    └── Events traffic   → Analytics
```

These three traffic types don't scale the same way, don't hit the same
infrastructure, and don't even have the same performance requirements. Lumping
them into "1M users" hides all of the interesting engineering.

### 1. Control plane traffic

`GET /home`, `GET /catalog`, `POST /login`, `POST /playback` — these are
small, cheap, and mostly stateless.

```
1M users
    │
    ▼
Load Balancer
    │
┌───┼───┐
▼   ▼   ▼
API-1 API-2 API-3
    │
    ▼
Services
```

This scales the boring, well-understood way: horizontally scaled stateless
API servers behind a load balancer. Add more boxes, load balances across
them. Nothing exotic.

### 2. Playback (data plane) traffic

This is where the numbers get scary. One viewer requesting a new video
segment roughly every 4 seconds is about 15 segment requests a minute. At 1
million concurrent viewers:

```
15 × 1,000,000 = 15,000,000 segment requests / minute
              ≈ 250,000 segment requests / second
```

There is no origin server or database that survives 250K requests/second
without help. The answer is that almost none of these requests should ever
reach the origin:

```
User
  │
  ▼
CDN
  │
┌─┴─┐
▼   ▼
cache hit   cache miss
  │           │
  ▼           ▼
User        Origin → Object Storage
```

For a hit show or a live match, the same handful of segments are being
requested by everyone at once — cache locality is extremely high, which is
exactly what makes CDN caching so effective here. Push those popular segments
to edge locations near the users:

```
        Origin
          │
 ┌────────┼────────┐
 ▼        ▼        ▼
Delhi   Mumbai    Jaipur
 Edge     Edge      Edge
  │        │         │
users    users     users
```

This improves latency, throughput, *and* protects the origin — three
benefits from one design choice.

**The live-streaming wrinkle:** for VOD, a segment is immutable once
generated, so it can be cached basically forever. Live content is different —
new segments are being produced continuously, and caching too aggressively
means viewers see stale data, while not caching enough means the origin gets
hammered by everyone requesting the "latest" segment simultaneously. Cache
freshness and cache effectiveness are directly in tension for live content in
a way they aren't for VOD.

### 3. Event traffic

Every pause, seek, skip, and completed episode is a signal that could feed
analytics or recommendations. But at scale, none of these events should be
written synchronously to your primary database:

```
Client
  │
  ▼
Event API
  │
  ▼
Kafka / Event Stream
  │
┌─┴───────────┐
▼             ▼
Analytics   Recommendation
Pipeline      Pipeline
```

Decoupling ingestion (fast, append-only) from processing (batch or
near-real-time) means a slow analytics job never becomes a reason playback
requests start failing.

### 4. Content processing

Not directly tied to concurrent viewers, but worth naming as its own
workload: transcoding, segmentation, and manifest generation happen
asynchronously via queues and worker pools, independent of how many people
are currently watching anything.

## Putting it together

```
                     USERS
                       │
         ┌─────────────┴─────────────┐
         ▼                           ▼
   CONTROL PLANE                DATA PLANE
         │                           │
         ▼                           ▼
   Load Balancer                    CDN
         │                           │
         ▼                           ▼
    API Servers                 Video Segments
         │                           │
   ┌─────┼──────┐                    ▼
   ▼     ▼      ▼              Object Storage
 Redis  DB   Services

                 USER EVENTS
                       │
                       ▼
                     Kafka
                  ┌────┼────┐
                  ▼    ▼    ▼
             Analytics ML  Recommendations
```

Note that even inside the control plane, not every read hits Postgres
directly — a cache layer (Redis) sits in front of the database for
frequently-requested data, the same way the CDN sits in front of object
storage for video. Same pattern, applied at two different layers of the
stack.

## The takeaway

The single biggest mental shift for me this week: **the number of concurrent
users is not the load on any individual component.** You have to decompose
"1 million users" into the distinct workloads they generate — control,
playback, events, processing — because each one has a different bottleneck,
a different scaling strategy, and in the live-streaming case, genuinely
competing constraints (freshness vs. cache effectiveness) that don't have a
clean universal answer.

Next up in this series: what changes when the content isn't a pre-existing
movie file but a cricket match being generated live, second by second.
