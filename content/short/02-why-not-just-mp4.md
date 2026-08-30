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
Bro: "why is my laptop fan sound like a jet engine"

**[THE PANIC FIX — still naive]**

So bro's genius fix? He moves the video to "cloud storage" but STILL routes
every single request through his one server, because "the API has to control
it right."

tch tch tch... closer bro. CLOSER. But still no.

**[THE ACTUAL LESSON]**

Here's what bro was missing: the API should hand out *permission*, not
*bytes*. Video should live in object storage, fronted by a CDN — a system
literally built to blast the same file to millions of people at once.

```
API (Control Plane)
  → decides WHO can watch

CDN + Object Storage (Data Plane)
  → actually DELIVERS the video
```

Two completely different jobs. Bro was making one exhausted server do both.

**[OUTRO]**

Next time: bro realizes movie.mp4 itself is the problem — because his
cousin on 4G and his uncle on the office wifi both need DIFFERENT versions
of the same movie. 👀

Follow for part 3.

---

*True Story!! 😂*

---

**Caption for post:**
Bro's server caught actual smoke 💀 turns out "just use cloud storage" isn't
the whole fix either. Part 2 of the Hio Jotstar saga. #systemdesign
#hiojotstar #cdn #softwareengineering
