# Hio Jotstar — Story 1, Part 1: "The Ban"

**Format:** Insta Reel / YT Short script. Hinglish rhyme storytime, delivered
over cat footage. Cast: Bambani (left), Bro (middle), Tod Fod Engineer
(right) — see [`../PRODUCTION.md`](../PRODUCTION.md).

Story 1 is a multi-part series. Part 1 = intro + setup + cliffhanger only.
The roast/lesson/fix for the naive architecture lands in **Part 2**
([`01b-story1-part2-the-fix.md`](01b-story1-part2-the-fix.md)).

---

## THE SCRIPT (official — rhyme, VO)

*(Read aloud, matched to cat cuts — one line per cat-cut roughly, see timing
notes below.)*

```
Hum h teen dudez
ek Bambani ek Bro or me hu Tod Fod Engineer

we got some foodz
but Bro or Bambani ka hua lafda

Bambani h mota seth or Bro k paas nhi h kapda
Bro ne kiya Bambani pe vaar

Bambani ne kiya ban from Jio Hotstar
ab Bro lega badla

dikhaega kitna h hoshiyar,
Bro ka hua h tiraskar

Bro bnaega Hio Jotstar
but yeh kya

Bro ka architecture h guu
Bro h bada wala chuuuu
```

**[THE ARCHITECTURE — whiteboard-sketch overlay, timed to "Bro ka
architecture h guu", held on screen through the cut to black]**

```
User
  │
  │ GET /movie.mp4
  ▼
FastAPI
  │
  ▼
Storage
```

**[END OF PART 1 — CLIFFHANGER, no lesson/punchline yet]**

Hold on the diagram + Bro's shocked/naive framing. Text overlay: "kya hoga
iska? part 2 me pata chalega 👀"

Caption tease, no resolution — the roast/fix/punchline all live in Part 2.

---

*True Story!! 😂 Part 1/? — follow for Part 2*

---

**Caption for post:**
Hum hai 3-Dudez 🐱 Bambani, Bro, aur Tod Fod Engineer. Bro ka architecture
dekh ke khud hi bologe "yeh kya bakwaas hai" 💀 Part 1 — Part 2 mein hoga
tod fod. #hiojotstar #systemdesign #3dudez #catsofinstagram #buildinpublic

---

## Timing / cutting notes for the edit

Rough beat-to-cat mapping (adjust once VO is recorded and timestamped):

1. "Hum h teen dudez" → group shot (all 3 in frame, e.g. the bed photo)
2. "ek Bambani" → cut/hold on Bambani (left, b&w kitten)
3. "ek Bro" → cut to Bro (middle, ginger kitten)
4. "or me hu Tod Fod Engineer" → cut to Tod Fod Engineer (right, orange-white)
5. "we got some foodz" → playful/eating or neutral cutaway if available
6. "lafda" / "vaar" / "ban" lines → alternate quick cuts between Bambani and
   Bro to sell the beef, faster cut pace
7. "Bro bnaega Hio Jotstar" → hold on Bro, confident framing
8. "Bro ka architecture h guu" → whiteboard-sketch diagram overlay appears
   over Bro's shot, holds through end card
9. Cut to black / "Part 2 me pata chalega" tease card

---

## Older English draft (superseded)

Kept for reference — not the version being produced. The rhyme script above
is canonical going forward.

**[HOOK — first 2 seconds, punchy]**

StoryTime 📖 Once my bro got into beef with Ambani...

**[SETUP]**

...and got PERMANENTLY banned from Jio Hotstar. 😭 Bro couldn't accept
defeat. So bro did what any unemployed genius would do — he built his OWN
app.

**[REVEAL]**

Ladies and gentlemen... presenting... HIO JOTSTAR

**[THE ARCHITECTURE]**

```
User
  │
  │ GET /movie.mp4
  ▼
FastAPI
  │
  ▼
Storage
```

**[THE LESSON]**

Your API server's job is to say "yes you can watch this" — NOT to actually
hand over the video. The second your app server starts pushing video bytes
to users, it IS your video delivery network now, and it was never built for
that job. Real platforms split it: one server says "you're allowed," a
completely different system (CDN + storage) actually delivers the bytes.

**[PUNCHLINE]**

Let's tod fod it. 🫡
