# Content: Learning in Public — "Hio Jotstar" series

Theme: **learning in public**, but funny. Not threads, not lectures.

The format: a running storytime bit called **Hio Jotstar** — my bro got
banned from Jio Hotstar for beefing with Ambani, so he builds his own
knockoff streaming app. Every episode he ships something naive, it breaks at
scale, we roast his architecture ("tch tch tch bro is so naive"), then land
the actual system design lesson in one clean beat. Ends with a hook into the
next episode.

**Series punchline (every episode, right after the fix is revealed):**
> "Let's tod fod it."

This is the sign-off/stamp — say it out loud right after explaining the real
fix, before the outro tease. It's the "and that's the tea" of this series;
keep it in every episode so it becomes recognizable.

## Structure

- `short/` — Insta Reel / YT Short scripts. Each system-design failure/fix
  is a **Story**, and each Story can span multiple **Parts** (a cliffhanger
  Part 1, a payoff Part 2, etc.) — a Story doesn't have to resolve in one
  video. Files are named `NNx-storyN-partN-topic.md` (e.g.
  `01a-story1-part1-the-ban.md`, `01b-story1-part2-the-fix.md`). Each part
  has the script (rhyme intro where applicable, roast, lesson, punchline,
  outro) plus a ready-to-use caption.
- `twitter/` — X/Twitter thread version of each episode, same beats
  compressed into tweet-sized chunks with inline ASCII diagrams. Post it as
  a reply-chain under the video clip, or standalone for people who'd rather
  read than watch.
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

## Story / Part status

| Story | Part | Title | Lesson | Twitter thread | Long-form companion |
|---|---|---|---|---|---|
| 1 | 1 | The Ban | Setup/cliffhanger — naive one-server architecture revealed | — | — |
| 1 | 2 | The Fix | API shouldn't serve video bytes directly; split control/data plane | — | Control plane vs data plane |
| 2 | 1 | The Meltdown | (topic content exists under old `02-*.md`, not yet split into Story/Part) | ✅ | — |
| 3 | 1 | One File to Rule Them All (Bad Idea) | Segments + adaptive bitrate streaming | ✅ | — |
| 4 | 1 | Everyone Presses Play | 1M users = 3 different workloads, not 1 big number | ✅ | Scaling to a cricket match |
| 5 | — | TBD (from Layer3) | Live streaming: content doesn't exist yet when people start watching | — | — |

Note: Stories 2-4 still use the flat `NN-topic.md` naming from before the
Story/Part convention was introduced — rename/split them the same way as
Story 1 when they're next revised.

## Next up

Layer3.txt is just a title so far: "The Everyone Presses Play Problem." Once
that layer gets fleshed out, it becomes Story 5 — live streaming, the video
being generated in real time as the match happens.
