# Control Plane vs Data Plane: What I Learned Rebuilding Hotstar's Architecture (In My Head)

*Part of a "learning in public" series where I work through how a large-scale
streaming platform like Hotstar is actually built, one failure case at a time.*

## The starting question

I wanted to understand how an app like Hotstar handles a cricket match with
tens of millions of concurrent viewers. Rather than reading a system design
doc top-down, I started from the simplest possible version and kept asking
"what breaks first?"

## Version 0: the naive app

```
User
  |
  v
FastAPI Server
  |
  v
Database
```

And for video specifically:

```
User
  |
  | GET /movie.mp4
  v
FastAPI Server
  |
  v
Storage
```

This is genuinely fine for a toy project. One user, one server, one file.
Login works, metadata works, playback works.

## Where it breaks

Put 100,000 users on this. Every one of them is now pulling video bytes
*through* your application server. Your API server — the thing meant to
handle logic like "is this user logged in?" — has become, by accident, your
video delivery network. It wasn't designed for that job, and it collapses
under it: slow, expensive, fragile.

The core mistake is conflating two jobs that have completely different
scaling characteristics:

1. Deciding *who* can watch *what* (small, fast, logic-heavy)
2. Actually moving gigabytes of video to millions of screens (huge, dumb,
   bandwidth-heavy)

## The fix: split into two planes

**Control plane** — everything about deciding and describing:

- Login and authentication
- User profile
- Catalog
- Search
- Subscriptions
- Watch history
- Recommendations
- Playback authorization

**Data plane** — everything about actually moving media:

- Movies, episodes, live streams
- Video segments
- Audio tracks, subtitles

The redesigned flow:

```
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

The rule that stuck with me: **the API gives the player permission and
playback information. The CDN delivers the actual video.** The API should
never see a video byte pass through it.

## Why this split matters more than it sounds

It's tempting to read this as "just use a CDN," but the deeper point is
architectural: these two planes have different growth curves. Control plane
traffic grows roughly linearly with user count and is cheap per request.
Data plane traffic is where almost all your bytes and almost all your cost
live, and it needs a completely different scaling strategy — caching,
regional edges, origin protection — that has nothing to do with your
application logic.

Once I separated these mentally, the rest of the system started making more
sense: transcoding pipelines, adaptive bitrate, CDN cache invalidation — they
all live entirely inside the data plane. Playback authorization, catalog,
recommendations — all control plane. Almost every hard problem in a
streaming platform is "how do we scale the data plane without touching the
control plane's simplicity," or vice versa.

## What's next

The next piece in this series covers why the data plane can't just serve a
single `movie.mp4` — and how segmentation, manifests, and adaptive bitrate
streaming solve the "network keeps changing" problem.
