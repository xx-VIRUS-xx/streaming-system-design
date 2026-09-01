# Hio Jotstar — Episode 1: "The Ban"

**Format:** Insta Reel / YT Short script. Hinglish rhyme storytime, delivered
over cat footage. Cast: Bambani (left), Bro (middle), Tod Fod Engineer
(right) — see [`../PRODUCTION.md`](../PRODUCTION.md).

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
architecture h guu"]**

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

**[THE LESSON — quick VO tag right after the rhyme, before cutting to
Tod Fod Engineer]**

Ek hi server sab kuch kar raha hai — permission bhi de raha hai, aur poora
movie file bhi khud hi bhej raha hai lakhon logon ko. Ye kaam ek akela
FastAPI server ke liye nahi hai. Jab 100,000 log ek saath aayenge, ye server
udd jayega.

Asli fix: ek system decide karta hai "kaun dekh sakta hai" — doosra system
(CDN + storage) actually video deliver karta hai. Do alag kaam, do alag
system.

**[THE PUNCHLINE — Tod Fod Engineer on screen, stamp on screen: "Let's tod
fod it"]**

Let's tod fod it. 🫡

**[OUTRO / HOOK FOR NEXT EP]**

100,000 log aaye, Bro ka server pura crash ho gaya. Agli baar dikhayenge
kaise.

Follow for part 2.

---

*True Story!! 😂*

---

**Caption for post:**
Hum hai 3-Dudez 🐱 Bambani, Bro, aur Tod Fod Engineer. Bro ka architecture
dekh ke khud hi bologe "yeh kya bakwaas hai" 💀 #hiojotstar #systemdesign
#3dudez #catsofinstagram #buildinpublic

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
   over Bro's shot
9. Lesson VO → diagram stays on screen or transitions to corrected
   two-box diagram
10. "Let's tod fod it" → hard cut to Tod Fod Engineer, punchline stamp
    on-screen, timed to hit exactly on the line

---

## Older English draft (superseded)

Kept for reference — not the version being produced. The rhyme script above
is canonical for Episode 1 going forward.

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
