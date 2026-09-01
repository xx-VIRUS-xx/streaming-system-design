# Hio Jotstar — Episode 1: "The Ban" (Twitter/X thread)

**Posting note:** Quote-tweet or reply-chain this thread under the video clip,
or post standalone. Tweet 1 must work as a hook with zero context.

---

**1/**
StoryTime 📖

My bro got into beef with Ambani.

Got PERMANENTLY banned from Jio Hotstar.

So bro did what any unemployed genius would do. He built his own app.

Presenting: 🔥 HIO JOTSTAR 🔥

**2/**
Bro's entire backend. For streaming movies. To potentially millions of users.

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

tch tch tch. Bro is so naive.

**3/**
Bro's one FastAPI server is going to hand out 5GB movie files to every
single user, directly, forever.

Bro's server when 100 people open the app at once:

💀💀💀

**4/**
Here's the thing nobody tells you: your API server's job is to say "yes you
can watch this" — NOT to hand over the actual video.

Bro built himself a bouncer, then made the bouncer personally carry every
guest into the club on his back.

For 100,000 guests.

**5/**
The moment your app server starts pushing video bytes to users, it IS your
video delivery network now. And it was never built for that job.

Real fix: one system checks who's allowed. A completely different system —
storage + CDN — delivers the bytes.

**6/**
Let's tod fod it. 🫡

Next time: bro finds out the hard way what happens when 100k people show up
on day one. His laptop starts sounding like a 747.

Follow for part 2 👇
