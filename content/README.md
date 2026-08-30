# Content: Learning in Public — "Hio Jotstar" series

Theme: **learning in public**, but funny. Not threads, not lectures.

The format: a running storytime bit called **Hio Jotstar** — my bro got
banned from Jio Hotstar for beefing with Ambani, so he builds his own
knockoff streaming app. Every episode he ships something naive, it breaks at
scale, we roast his architecture ("tch tch tch bro is so naive"), then land
the actual system design lesson in one clean beat. Ends with a hook into the
next episode.

## Structure

- `short/` — Insta Reel / YT Short scripts. One episode = one failure = one
  fix. Named `NN-topic.md`, in episode order. Each file has the full script
  (hook / setup / roast / lesson / outro) plus a ready-to-use caption.
- `long/` — companion "director's cut" write-ups for YouTube long-form or a
  blog, same Hio Jotstar story but with the full technical depth and
  diagrams. Optional — not every short needs one.

## Format per short episode

1. **Hook** (first 2 sec) — story opener, has to earn the swipe
2. **Setup** — bro's naive decision, shown as an ASCII/text diagram
3. **Roast** — "tch tch tch bro is so naive" beat, keep it fun not mean
4. **Lesson** — the ONE real system design concept, in plain language, no jargon dump
5. **Outro** — tease next episode's problem, "Follow for part N"

Keep each script short enough to read aloud in 30-45 seconds.

## Source material

- [`../Hotstar_Learning_Path.md`](../Hotstar_Learning_Path.md) — full curriculum
- [`../Layer1.txt`](../Layer1.txt) / [`../Layer1_Flow_Diagrams.md`](../Layer1_Flow_Diagrams.md) — ingestion → playback
- [`../Layer2.txt`](../Layer2.txt) / [`../Layer2_Flow_Diagrams.md`](../Layer2_Flow_Diagrams.md) — scaling to 1M+ users
- [`../Layer3.txt`](../Layer3.txt) — not started yet ("The Everyone Presses Play Problem")

## Episode status

| # | Episode title | Lesson | Long-form companion |
|---|---|---|---|
| 01 | The Ban | API shouldn't serve video bytes directly | Control plane vs data plane |
| 02 | The Meltdown | Split control plane (permission) from data plane (delivery) | — |
| 03 | One File to Rule Them All (Bad Idea) | Segments + adaptive bitrate streaming | — |
| 04 | Everyone Presses Play | 1M users = 3 different workloads, not 1 big number | Scaling to a cricket match |
| 05 | TBD (from Layer3) | Live streaming: content doesn't exist yet when people start watching | — |

## Next up

Layer3.txt is just a title so far: "The Everyone Presses Play Problem." Once
that layer gets fleshed out, Episode 5 covers live streaming — the video
being generated in real time as the match happens.
