# Hotstar-Like Streaming System: Learning Path

This path starts from a naive video app and gradually builds toward a large-scale OTT platform like Hotstar. The goal is to understand why each system component exists, what problem it solves, and what tradeoffs it introduces.

## 1. Start With The Mental Model

A streaming platform has two major planes:

Detailed diagrams for this layer: [Layer1_Flow_Diagrams.md](diagrams/Layer1_Flow_Diagrams.md)

Scaling diagrams for the next layer: [Layer2_Flow_Diagrams.md](diagrams/Layer2_Flow_Diagrams.md)

### Control Plane

The control plane handles user-facing application logic and metadata.

- Login and authentication
- User profile
- Catalog
- Search
- Subscriptions
- Watch history
- Recommendations
- Playback authorization

### Data Plane

The data plane handles actual media delivery.

- Movies
- Episodes
- Live streams
- Video segments
- Audio tracks
- Subtitles

Key idea: application servers should control access to video, but they should not directly deliver every video byte.

## 2. Build The Naive Architecture

Start with the simplest possible design:

```text
User
  |
  v
FastAPI Server
  |
  v
Database
```

For video delivery:

```text
User
  |
  | GET /movie.mp4
  v
FastAPI Server
  |
  v
Storage
```

This works for learning basic API and storage flows, but it fails quickly at scale.

### What To Learn

- Basic API design
- User login
- Movie metadata storage
- Simple file upload
- Simple file download

### Main Failure

If 100,000 users request video through your application servers, those servers become your video delivery network. That is expensive, slow, and fragile.

## 3. Separate Control Plane From Data Plane

The API should handle metadata, authentication, and authorization. Video bytes should be served from object storage and a CDN.

```text
Client
  |
  v
API / Control Plane
  |
  | metadata, auth, playback permission
  v
Database

Object Storage
  |
  v
CDN
  |
  v
Users
```

### What To Learn

- Object storage
- CDN basics
- Cache hits and cache misses
- Origin server
- Signed URLs
- Separating metadata from media

### Main Design Rule

The API gives the player permission and playback information. The CDN delivers the actual video.

## 4. Understand Video Segmentation

Uploading one large `movie.mp4` is not enough for modern streaming. A 5 GB file should be processed into smaller chunks called segments.

```text
Original Video
  |
  v
Transcoder
  |
  v
Video Segments
  |
  +-- segment001
  +-- segment002
  +-- segment003
  +-- segment004
```

The player does not download the whole movie. It continuously requests the next segment as playback progresses.

### What To Learn

- Video chunks / segments
- Manifests
- HLS
- MPEG-DASH
- Player segment fetching
- Buffering

## 5. Learn Adaptive Bitrate Streaming

Networks change. A user may start with 20 Mbps and suddenly drop to 2 Mbps. The player needs to switch quality without restarting playback.

Adaptive bitrate streaming solves this by creating multiple versions of the same video.

```text
Original Video
  |
  +-- 1080p segments
  +-- 720p segments
  +-- 480p segments
```

The player uses the manifest to choose which quality to request.

### What To Learn

- Bitrate
- Resolution
- Codecs
- Bandwidth estimation
- Buffer health
- Quality switching
- HLS master playlist
- DASH manifest

### Key Question

How does the player decide whether to request 1080p, 720p, or 480p?

That leads to adaptive bitrate algorithms.

## 6. Add The Transcoding Pipeline

Transcoding is too slow to happen inside the upload request. Instead, uploads should create background jobs.

```text
Creator Upload
  |
  v
Object Storage
  |
  v
Job Queue
  |
  +-- Worker
  +-- Worker
  +-- Worker
  |
  v
Transcoded Segments
  |
  v
Object Storage
```

### What To Learn

- Background jobs
- Queues
- Worker pools
- CPU vs GPU transcoding
- Retries
- Idempotency
- Job status
- Failure recovery

### Important Failure Case

What happens if a transcoding worker crashes halfway through?

That leads to retries, checkpoints, idempotent jobs, and explicit job state.

## 7. Design The Storage Layout

A simple object storage layout:

```text
/videos/
  movie123/
    original/
    1080p/
    720p/
    480p/
    manifests/
```

### Core Tables

```text
Video
-----
id
title
duration
source_uri
status
created_at
updated_at
```

```text
VideoRepresentation
-------------------
video_id
resolution
codec
bitrate
manifest_uri
```

### What To Learn

- Object key design
- Metadata modeling
- Video lifecycle states
- Manifest storage
- Source file vs generated outputs

## 8. Put CDN In Front Of Storage

If one million people request the same segment, the object store should not serve every request. The CDN should cache popular segments at edge locations.

```text
Object Storage / Origin
  |
  v
CDN Edge
  |
  +-- User
  +-- User
  +-- User
```

### What To Learn

- Edge caching
- Cache hit ratio
- TTL
- Cache invalidation
- Origin shielding
- Regional edge locations
- Hot content handling

### Key Question

What happens when 10 million people watch the same cricket match?

That leads to CDN scaling, live streaming, origin scaling, and regional traffic management.

## 9. Understand Playback Authorization

Users should not be able to watch paid content without permission.

Typical playback flow:

```text
1. User opens app
2. User authenticates
3. App fetches catalog
4. User selects movie
5. Client requests playback authorization
6. API returns playback information
7. Player obtains manifest
8. Player requests segments
9. CDN serves segments
10. Player keeps requesting next segments
```

### What To Learn

- Authentication
- Authorization
- Entitlements
- Subscriptions
- Signed URLs
- Token expiry
- DRM basics
- Device limits
- Geo restrictions

### Key Question

How do we stop someone from downloading content they have not paid for?

That leads to signed URLs, short-lived tokens, entitlement checks, and DRM.

## 10. Add Catalog, Search, And Recommendations

Once video delivery works, the product needs discovery.

### Catalog

Learn how to model:

- Movies
- Shows
- Episodes
- Genres
- Languages
- Release dates
- Cast and crew
- Availability windows

### Search

Millions of users searching the catalog leads to:

- Search indexing
- Ranking
- Autocomplete
- Typo tolerance
- Query caching
- Popular result caching

### Recommendations

Personalized recommendations require:

- Event collection
- Watch history
- Feature pipelines
- Ranking models
- Real-time and batch signals
- A/B testing

## 11. Learn Live Streaming

Live streaming has different constraints from video-on-demand.

### What To Learn

- Live ingest
- Encoding ladder
- Segment generation in real time
- Live manifests
- Latency
- DVR windows
- CDN scaling for live events
- Origin protection

### Key Question

What happens when millions of users join the same live cricket stream within minutes?

That leads to pre-warming CDN caches, regional scaling, and careful origin capacity planning.

## 12. Add Reliability And Multi-Region Design

At large scale, one region failing should not take down the whole service.

### What To Learn

- Multi-region deployment
- Database replication
- Failover
- Disaster recovery
- Regional routing
- Data consistency
- Health checks
- Graceful degradation

### Key Question

How do we keep the service alive if an entire region fails?

That leads to replication, failover automation, and disaster recovery planning.

## 13. Final Architecture

```text
CONTROL PLANE

Client
  |
  v
API Gateway
  |
  +-- Auth / User Service
  +-- Catalog Service
  +-- Search Service
  +-- Subscription Service
  +-- Playback Authorization Service
  +-- Recommendation Service
  |
  v
Databases / Indexes / Caches


DATA PLANE

Upload
  |
  v
Object Storage
  |
  v
Queue
  |
  v
Transcoding Workers
  |
  v
Segmented Video + Manifests
  |
  v
Object Storage / Origin
  |
  v
CDN
  |
  v
Player
```

## Suggested Study Order

1. Simple streaming API
2. Object storage and CDN
3. Video segmentation
4. HLS or MPEG-DASH
5. Adaptive bitrate streaming
6. Upload and transcoding pipeline
7. Queue and worker design
8. Playback authorization
9. Signed URLs and DRM basics
10. Catalog modeling
11. Search indexing
12. Recommendation pipeline
13. Live streaming
14. Multi-region reliability
15. Observability, alerts, and cost optimization

## Practice Projects

### Project 1: Naive Video App

Build a small API that stores video metadata and serves a video file directly.

Focus:

- Upload
- Metadata
- Simple playback URL
- Basic database schema

### Project 2: CDN-Ready Video App

Move video files to object storage and make the API return playback URLs instead of serving bytes.

Focus:

- Object storage layout
- Signed URLs
- API/data-plane separation

### Project 3: Segment-Based Player

Convert a video into HLS segments and serve a manifest to a browser player.

Focus:

- FFmpeg
- HLS
- Manifests
- Segment requests

### Project 4: Transcoding Pipeline

Create a background job system that transcodes uploaded videos into multiple resolutions.

Focus:

- Queue
- Workers
- Job status
- Retries
- Failed job recovery

### Project 5: Scalable Streaming Design

Write a complete system design for video-on-demand and live streaming.

Focus:

- CDN behavior
- Playback authorization
- Search
- Recommendations
- Multi-region failover

## Interview-Style Questions

- Why should application servers not serve video bytes directly?
- How does a CDN reduce load on object storage?
- What is the difference between control plane and data plane?
- Why do streaming systems use video segments?
- How does adaptive bitrate streaming work?
- What is stored in a video manifest?
- How would you design a transcoding pipeline?
- How do you retry failed transcoding jobs safely?
- How do signed URLs protect video segments?
- What extra problems appear in live streaming?
- How would you scale for a major cricket match?
- How would you design search for a large media catalog?
- How would recommendations be generated?
- How would the system survive a regional outage?

## End Goal

By the end, you should be able to explain and design this progression:

```text
Simple Streaming System
  -> Scalable Streaming System
  -> Large-Scale Video-On-Demand
  -> Live Streaming
  -> Global Distribution
  -> Hotstar-Like Architecture
```
