# Hio Jotstar — Episode 2: "The Meltdown"

**Format:** Insta Reel / YT Short script. Continues directly from Episode 1.

---

**[HOOK]**

StoryTime part 2 📖 Last time on Hio Jotstar...

Bro's server was literally handing out movie.mp4 to every single user
directly. We told you it wouldn't survive. IT DID NOT SURVIVE.

**[THE DISASTER]**

Day 1 of Hio Jotstar going public: 100,000 people open the app.

Bro's ONE FastAPI server, streaming full 5GB mp4 files to all of them at
once:

```
100,000 Users
      │
      ▼
   FastAPI 😵💀🔥
      │
      ▼
    Storage
```

Server: *dies immediately*
Bro: "why is my laptop fan sound like a jet engine about to achieve liftoff"
Bro's electricity bill: also achieving liftoff

**[THE PANIC FIX — still naive]**

So bro's genius fix? He moves the video to "cloud storage" but STILL routes
every single request through his one server, because "the API has to
control it, right?"

tch tch tch... closer bro. CLOSER. Bro basically moved the buffet to a
bigger kitchen but is still personally hand-delivering every plate to every
table himself. Still no.

**[THE ACTUAL LESSON]**

Here's what bro was missing: the API should hand out *permission*, not
*bytes*. Video should live in object storage, fronted by a CDN — a system
literally built to blast the same file to millions of people at once, no
sweat, no jet-engine laptop required.

```
API (Control Plane)
  → decides WHO can watch

CDN + Object Storage (Data Plane)
  → actually DELIVERS the video
```

Two completely different jobs. Bro was making one exhausted server do both,
like a waiter who also insists on being the delivery truck.

**[THE PUNCHLINE]**

Let's tod fod it. 🫡

**[OUTRO]**

Next time: bro realizes movie.mp4 itself is the problem — because his
cousin on 4G and his uncle on the office wifi both need DIFFERENT versions
of the same movie, and bro is about to learn that the hard way too. 👀

Follow for part 3.

---

*True Story!! 😂*

---

**Caption for post:**
Bro's server caught actual smoke 💀 turns out "just use cloud storage" isn't
the whole fix either. Part 2 of the Hio Jotstar saga. Let's tod fod it.
#systemdesign #hiojotstar #cdn #softwareengineering

---

## Voiceover-only script

*(No visual directions — read straight over cat footage. Pause where marked
for diagrams.)*

Last time on Hio Jotstar, bro's one server was handing out the full movie
file to every single person directly. We said it wouldn't survive. It did
not survive.

Day one, a hundred thousand people open the app at once.

*(pause — diagram: 100,000 Users → FastAPI → Storage, server on fire)*

Bro's laptop fan starts sounding like it's trying to achieve liftoff. Bro's
electricity bill is also trying to achieve liftoff.

So bro's genius fix — and I want you to sit with this — bro moves the video
to cloud storage, but keeps routing every single request through his one
server anyway. Because, quote, "the API has to control it, right?"

Closer, bro. Closer. But no. That's like moving the buffet to a bigger
kitchen and still insisting on personally carrying every single plate to
every single table yourself.

Here's the actual fix. The API's job is to hand out permission — not bytes.
The video itself should live in object storage, sitting behind a CDN, a
system that is literally built to blast the same file to millions of people
at once without breaking a sweat.

One system says "you're allowed." A completely different system delivers
the video. Two jobs. Bro was making one exhausted server do both.

Let's tod fod it.
