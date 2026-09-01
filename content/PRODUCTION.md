# Production Notes — 3-Dudez / Hio Jotstar

Account name: **3-Dudez** (3 cats, each cast as a recurring character across
episodes, roles change per episode as needed).

## Cast (Episode 1 casting)

Left to right in the group photo (`Clips/ECBB1E8D-BFAA-4D6C-8B1E-7E58921B6187.PNG`):

| Position | Cat | Character (Ep. 1) |
|---|---|---|
| Left | black-and-white kitten | **Bambani** (the Ambani stand-in bro beefed with) |
| Middle | ginger/orange kitten | **Bro** (the naive founder building Hio Jotstar) |
| Right | orange-and-white kitten | **Tod Fod Engineer** (the one who "fixes"/roasts the architecture — delivers the punchline) |

Character casting can change per episode/topic — note the mapping used in
each episode's script file so continuity is trackable across the series.

## Voice / language

- **Hinglish rhyme, not English prose.** Episode 1 script is a rhyming
  Hindi/Hinglish verse (see `content/short/01-why-not-serve-video-from-api.md`),
  delivered as VO over cat cuts, one line roughly per cat-cut. This is the
  house style going forward, not just a one-off — write new episodes as
  rhyme first, then a short plain-language technical tag right after for
  the actual lesson, then the "Let's tod fod it" punchline.
- Old plain-English scripts are kept at the bottom of each file as
  superseded drafts, not deleted, in case tone/pacing needs reference.

## Visual style

- **Diagram overlays:** whiteboard-sketch style — semi-transparent panel,
  hand-marker font (`Marker Felt` on macOS, bundled system font, good
  stand-in for a hand-drawn look), boxes/arrows drawn like someone annotating
  live over the cat footage. Not a clean slide cutaway.
- **Punchline stamp:** "Let's tod fod it" appears as an on-screen stamp/text
  moment right when Tod Fod Engineer is on screen, timed to the audio line.
- **Aspect ratio:** vertical 9:16 for Reels/Shorts.

## Raw assets

- `Clips/` — source cat footage and photos, gitignored (video/image binaries
  not committed; see `.gitignore`).
- Voiceover recordings: transcribed via local `whisper` (see
  `content/short/01-transcript-raw.txt` for the Ep.1 example), then matched
  against the script for timing.

## Pipeline (per episode)

1. Drop voiceover recording + raw cat clips into `Clips/`
2. Transcribe voiceover with whisper, get timestamps
3. Cut/sequence cat clips against the voiceover track (ffmpeg)
4. Generate whiteboard-sketch diagram overlays as PNGs, composite at the
   right timestamps (ffmpeg overlay filter)
5. Burn in punchline stamp ("Let's tod fod it") synced to the audio line
6. Export vertical rough-cut MP4
7. Polish pass in **InShot** (punch-ins, pacing, trending audio) before
   posting — see [`README.md`](README.md) for why InShot over CapCut
   (CapCut is banned in India as of 2020, still in effect 2026)
