# Hio Jotstar — Episode 4: "Everyone Presses Play" (Twitter/X thread)

**Posting note:** Quote-tweet or reply-chain under the video clip, or post
standalone.

---

**1/**
StoryTime part 4 📖

Bro's app is actually working now. Multiple qualities, smooth playback,
uncle stopped complaining. Bro basically thinks he's Reliance at this point.

Then bro made a HUGE mistake.

Bro announced he got the streaming rights to a cricket match.

**2/**
10 million people. Same match. Same moment. Everyone hits play within
seconds of each other. A stampede — except everyone's stampeding toward a
loading wheel.

Bro, confidently: "it's fine, I already fixed the video thing"

Narrator: it was not fine.

**3/**
tch tch tch. Bro thought "1 million users" was one big scary number that
needed one big scary server. 😩

Nah bro. It's 3 different problems wearing a trenchcoat:

```
10M viewers hitting play
        │
   ┌────┼────┐
   ▼    ▼    ▼
 Login  Video  "user paused
 traffic traffic  at 3:42" etc
```

**4/**
Login / "what's on" traffic? Chill, spread it across a few servers. Bro's
grandma could scale this part.

**5/**
Video traffic? 10M people asking for a new chunk every few seconds = HUNDREDS
of THOUSANDS of requests/second.

Bro's storage bucket alone was never surviving that. Needs a CDN caching
popular chunks near every city so most requests never even reach the origin.

**6/**
Every pause/skip/rage-quit event? Can't hit the main database directly per
event, or bro's database dies before the toss even happens. Before a single
ball is bowled.

**7/**
Bro's mistake: treating "10 million users" as one uniform pile of load.

It's three separate problems. Each needs its own fix.

Let's tod fod it. 🫡

**8/**
Next time: what happens when the video doesn't even exist yet, because it's
being filmed live, right now, as people are already watching it. 🎥

Follow for the finale 👇
