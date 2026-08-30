# Content: Learning in Public

This folder turns the Hotstar system-design notes into public content — the theme is
**learning in public**: showing the thinking, the wrong turns, and the "why" behind
each design decision, not just a polished final answer.

## Structure

- `short/` — one idea per post (X/Twitter threads, LinkedIn posts). Named
  `NN-topic.md`, numbered in the order they'd be posted.
- `long/` — full articles/blog posts that go deeper on one layer of the system.
  Named `NN-topic.md`.

## Voice guidelines

- Write as "I'm learning X" / "today I figured out Y", not as an authority.
- Every post should center one specific question or failure case (the notes are
  already structured this way — reuse it).
- Short posts end with a hook into the next post or a question for the reader.
- Long posts can include the ASCII diagrams from the source notes.

## Source material

- [`../Hotstar_Learning_Path.md`](../Hotstar_Learning_Path.md) — full curriculum
- [`../Layer1.txt`](../Layer1.txt) / [`../Layer1_Flow_Diagrams.md`](../Layer1_Flow_Diagrams.md) — ingestion → playback
- [`../Layer2.txt`](../Layer2.txt) / [`../Layer2_Flow_Diagrams.md`](../Layer2_Flow_Diagrams.md) — scaling to 1M+ users
- [`../Layer3.txt`](../Layer3.txt) — not started yet ("The Everyone Presses Play Problem")

## Status

| # | Short post | Long post |
|---|---|---|
| 01 | Why your API shouldn't serve video bytes | Control plane vs data plane in streaming systems |
| 02 | Why streaming apps don't just serve movie.mp4 | Building a naive streaming app (and why it breaks) |
| 03 | The adaptive bitrate problem in one thread | — |
| 04 | 1M concurrent viewers ≠ 1M times the load | Scaling to a cricket match: the four workloads |
