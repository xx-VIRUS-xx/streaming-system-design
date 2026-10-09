# Streaming System Design

A learning project: working out, layer by layer, how a large video-on-demand and live streaming platform (the kind Hotstar-style OTT services run) is put together, and turning those notes into short-form comedy content. It is study material, not an implementation: the repository contains notes, diagrams and scripts, no running code.

> The notes describe a generic "Hotstar-like" architecture reasoned from first principles. They are not based on, and do not describe, the internals of any real company's system.

System design summary: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

## Problem it addresses

System design is hard to learn from a finished diagram. This project starts from a naive video app, lets it break, and adds one component at a time (segmentation, adaptive bitrate, transcoding queue, CDN, authorization, caching, event pipelines), recording why each exists and what failure it fixes. Then it retells each lesson as a story so it sticks.

## What is in the repo

| Path | What it is |
|---|---|
| [docs/learning-path.md](docs/learning-path.md) | 13-step curriculum from the naive architecture to the final design, with study order, five practice projects and interview-style questions |
| [docs/diagrams/](docs/diagrams/) | Layer 1 (ingestion to playback, 10 Mermaid diagrams) and Layer 2 (scaling to one million viewers, 15 Mermaid diagrams) as flowcharts with explanations; they render on GitHub |
| [docs/raw-notes/](docs/raw-notes/) | Original working notes: `Layer1.txt`, `Layer2.txt`, `Notes.txt` (ASCII diagrams and scribbles) and `Layer3.txt` (only a title, "The Everyone Presses Play Problem") |
| [content/](content/) | "Hio Jotstar" comedy series: Reel/Short scripts, X/Twitter thread versions, long-form write-ups and production notes; see [content/README.md](content/README.md) |

## How to use it

Read `docs/learning-path.md` top to bottom, opening the Layer 1 and Layer 2 diagram files when the text points to them. There is nothing to install or run. Raw video, audio and exported cuts used for the series are excluded by `.gitignore`.

## Architecture in one paragraph

Split the platform into a **control plane** (login, catalog, search, subscriptions, watch history, recommendations, playback authorization) behind stateless API servers with Redis and a database, and a **data plane** (upload, object storage, a job queue, transcoding workers, segmented video with manifests, a CDN, the player). Scale them differently by thinking in four workloads: control traffic, video delivery, content processing and event processing. The details are in [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Limitations and next steps

- Conceptual only: no code, tests, benchmarks or capacity measurements, so every number or sizing claim is an exercise, not a result.
- Not validated against any real production system, and the content series is a comedy format, not a technical source.
- Layer 3 ("everyone presses play": the thundering-herd problem for live events) is not written yet; Layer 3 has a title and nothing else.
- `Notes.txt` and the other raw notes are unedited working notes and contain typos.
- The comedy scripts use a satirical character for a real public figure; check you are comfortable with that before sharing widely.
- No LICENSE has been chosen.
