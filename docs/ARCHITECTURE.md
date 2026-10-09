# Architecture (as developed in these notes)

A summary of the design the learning path builds toward. Diagrams and reasoning are in [learning-path.md](learning-path.md) and [diagrams/](diagrams/); this page is the map.

## The core split

```
                         Users
          +----------------+------------------+
          v                v                  v
    CONTROL PLANE      DATA PLANE         USER EVENTS
 login, catalog,       movies, episodes,   watch events, clicks,
 search, subscriptions, live streams,      searches
 watch history,        segments, audio,
 recommendations,      subtitles
 playback authorization
```

Key rule from the notes: application servers decide who may watch, but they must not deliver every video byte.

## Control plane

Client -> load balancer -> stateless API servers (one gateway fronting auth/user, catalog, search, subscription, playback-authorization and recommendation responsibilities) -> Redis for hot application data -> database.

- Start as a monolith and separate responsibilities early, but avoid premature microservices.
- Keep API servers stateless so they scale horizontally.
- Redis serves repeated reads (home page, catalog metadata, profile data); the CDN serves media. They solve different problems.

## Data plane

```
Upload -> Object storage -> Job queue -> Transcoding workers
       -> Segmented video + manifests -> Object storage / origin -> CDN -> Player
```

- Transcoding is too slow for the upload request, so uploads create background jobs (queues, worker pools, retries, idempotency, job status).
- Video is cut into segments and described by a manifest, so the player can switch quality per segment (adaptive bitrate streaming).
- Object storage holds media; the database holds metadata. Segments are served from the CDN, with the origin protected behind it.

## Playback flow

1. Authenticate, browse the catalog, pick a title.
2. Client asks for playback authorization (entitlement, subscription, device and geo rules).
3. The API returns playback information; the player fetches the manifest.
4. The player requests segments from the CDN and keeps requesting the next ones, adapting bitrate to the connection.

Protection against unpaid downloads: entitlement checks, signed URLs, short-lived tokens and DRM.

## Four workloads

| Workload | Example | Primary scaling tool |
|---|---|---|
| Control plane | Login, catalog, playback auth | Stateless API servers + caches |
| Video delivery | Segment requests | CDN |
| Content processing | Transcoding and segmentation | Queues + workers |
| Event processing | Watch events, clicks, searches | Kafka + async consumers |

"One million viewers" is not one number: each workload grows differently, so scaling starts by asking which one is growing.

## Live streaming and reliability

- Live differs from on-demand: live ingest, real-time segment generation, live manifests, latency and DVR windows. A cache that works for on-demand content conflicts with freshness needs for live, and millions joining one match within minutes pressures the CDN and origin; the notes cover pre-warming CDN caches, regional scaling and origin capacity planning.
- Reliability: multi-region deployment, database replication, failover and disaster recovery, regional routing, health checks and graceful degradation.

## Design principles the notes keep returning to

- Separate control traffic from media traffic.
- Think in workloads, not just user count.
- Keep servers stateless; put state in caches, databases and object storage.
- Move slow work (transcoding) off the request path.
- Protect the origin with a CDN.
- Use an event stream for high-volume behavioural data.

## Not covered yet

Layer 3, the "everyone presses play" problem, has only a title. Capacity numbers, cost modelling and observability are listed as topics in the study order but not worked through.
