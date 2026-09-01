# Hio Jotstar — Story 1, Part 2: "The Fix"

**Format:** Insta Reel / YT Short script. Continues directly from Part 1
([`01a-story1-part1-the-ban.md`](01a-story1-part1-the-ban.md)). Cast:
Bambani (left), Bro (middle), Tod Fod Engineer (right).

Recap the diagram cliffhanger from Part 1 in the first second, then land
the roast, the lesson, and the punchline.

---

## THE SCRIPT (draft — rhyme continuation + VO tag)

*(Open on a quick recap of Part 1's diagram, then continue in the same
rhyme voice before dropping into plain Hinglish for the technical tag.)*

```
Pichli baar dekha tha Bro ka plan
ek hi server pe tika sara gyaan

100,000 log aaye jab ek saath
server bola "bhai ab meri gayi raat"
```

**[THE ARCHITECTURE RECAP — same whiteboard-sketch overlay from Part 1,
now with a big red X or "CRASH" scribble over it]**

```
User
  │
  │ GET /movie.mp4
  ▼
FastAPI  ❌ (crashed)
  │
  ▼
Storage
```

**[THE LESSON — plain Hinglish VO tag, Tod Fod Engineer enters frame]**

Ek hi server sab kuch kar raha tha — permission bhi de raha tha, aur poora
movie file bhi khud bhej raha tha lakhon logon ko. Ye kaam ek akela FastAPI
server ke liye nahi hai.

Asli fix: ek system decide karta hai "kaun dekh sakta hai" — doosra system
(CDN + storage) actually video deliver karta hai. Do alag kaam, do alag
system.

**[CORRECTED ARCHITECTURE — whiteboard-sketch overlay, drawn fresh]**

```
API (permission only)
     │
     ▼
  Database

CDN + Storage (actual video)
     │
     ▼
   Users
```

**[THE PUNCHLINE — Tod Fod Engineer front and center, stamp on screen]**

Let's tod fod it. 🫡

**[OUTRO / HOOK FOR NEXT EP]**

Bro ka server bach gaya... but ab agla problem: sabko same movie file nahi
chahiye. Kisi ko 4G pe chahiye, kisi ko 4K TV pe. Bro phir naiv nikla.

Follow for Story 2.

---

*True Story!! 😂 Part 2/2 — Story 1 complete*

---

**Caption for post:**
Part 2 — Bro ka server bacha, but sirf isliye kyunki humne architecture tod
fod kar di 💀 #hiojotstar #systemdesign #3dudez #catsofinstagram

---

## Timing / cutting notes for the edit

1. Cold open on Part 1's crashed diagram (recap, ~2 sec)
2. Rhyme couplet over quick cuts of Bro looking stressed / server-crash gag
3. "100,000 log aaye" → fast cut montage feel if multiple clips available
4. Lesson VO tag → Tod Fod Engineer enters frame, becomes the on-screen
   focus for the rest of the video
5. Corrected diagram overlay — clean two-box version, held long enough to
   read
6. "Let's tod fod it" → hard cut to Tod Fod Engineer close-up, stamp appears
   exactly on the line
7. Outro tease → quick cut to Bro looking confused/defeated for the next
   cliffhanger
