# Hio Jotstar — Episode 2: "The Meltdown" (Twitter/X thread)

**Posting note:** Quote-tweet or reply-chain under the video clip, or post
standalone. Tweet 1 should recap enough that it works without having seen
part 1.

---

**1/**
StoryTime part 2 📖

Last time on Hio Jotstar: bro's ONE server was handing out full movie files
to every single user directly.

We told you it wouldn't survive.

IT DID NOT SURVIVE.

**2/**
Day 1 of Hio Jotstar going public. 100,000 people open the app.

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
Bro: "why does my laptop fan sound like it's trying to achieve liftoff"

**3/**
So bro's genius fix?

He moves the video to "cloud storage" — but STILL routes every single
request through his one server. Because "the API has to control it, right?"

tch tch tch. Closer bro. CLOSER. But still no.

**4/**
That's like moving the buffet to a bigger kitchen and still insisting on
personally carrying every plate to every table yourself.

**5/**
The actual fix: the API hands out *permission*, not *bytes*.

```
API (Control Plane)
  → decides WHO can watch

CDN + Object Storage (Data Plane)
  → actually DELIVERS the video
```

Two completely different jobs. Bro was making one exhausted server do both.

**6/**
Let's tod fod it. 🫡

Next time: bro realizes movie.mp4 itself is the problem — his cousin on 4G
and his uncle on office wifi need DIFFERENT versions of the same movie.

Follow for part 3 👇
