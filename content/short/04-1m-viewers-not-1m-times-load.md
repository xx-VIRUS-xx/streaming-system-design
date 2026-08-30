# Short post — X/LinkedIn thread

Learning in public: "1 million concurrent users" doesn't mean 1 million times
the load on every part of your system. This was the most useful reframe I've
hit so far studying Hotstar-scale design.

Break the traffic apart by what it actually touches:

```
1M viewers
   ├── Control traffic  → APIs (login, catalog, recommendations)
   ├── Playback traffic → CDN (video segments)
   └── Event traffic    → Analytics (play, pause, seek, complete)
```

The API load scales roughly linearly and is small per user — GET /catalog,
GET /recommendations. Stateless servers behind a load balancer handle this
fine.

Playback traffic is a different beast. One viewer might request ~15 segments
a minute. At 1M concurrent viewers, that's 15 million segment requests a
minute — roughly 250,000 requests/second. Your API servers were never going
to survive that. The CDN has to absorb almost all of it, serving from edge
caches so only cache *misses* ever reach your origin.

Event traffic (every pause, seek, skip) is high-volume but doesn't need to be
synchronous. It goes onto a stream (Kafka) and gets processed by analytics
and recommendation pipelines later, not written straight to Postgres on the
request path.

Three totally different scaling problems hiding under one number: "1 million
users." The number of users isn't the same thing as the load on any single
component — you have to break it apart by workload first.
