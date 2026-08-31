# Hio Jotstar — Episode 4: "Everyone Presses Play"

**Format:** Insta Reel / YT Short script.

---

**[HOOK]**

StoryTime part 4 📖 Bro's app is actually working now. Multiple qualities,
smooth playback, uncle stopped complaining. Bro is basically Reliance at
this point, in his own head.

Then bro made a HUGE mistake.

Bro announced he got the streaming rights to a cricket match.

**[THE SETUP]**

10 million people. Same match. Same moment. Everyone hits play within
literal seconds of each other, like a stampede but for buffering wheels.

Bro, confidently: "it's fine, I already fixed the video streaming thing"

Narrator: it was not fine.

**[THE ROAST]**

tch tch tch bro thought "1 million users" was just... one big scary number
he needed one big scary server for. 😩

Nah bro. It's not ONE problem. It's like 3 different problems wearing a
trenchcoat and pretending to be one guy:

```
10M viewers hitting play
        │
   ┌────┼────┐
   ▼    ▼    ▼
 Login  Video  "user paused
 /home traffic  at 3:42" etc
 traffic         (events)
```

Login and "what's on" traffic? Chill, spread it across a few servers, easy,
bro's grandma could scale this one.

Video traffic? 10 million people asking for a new chunk every few seconds —
that's HUNDREDS of THOUSANDS of requests per second. Bro's storage bucket
alone was never going to survive that; it needs a CDN caching the same
popular chunks near each city so most requests never even reach the origin.

Every pause/skip/rage-quit event? Also can't hit the main database directly
per event or bro's database dies before the toss even happens — literally
before a single ball is bowled.

**[THE PAYOFF]**

Bro's mistake: treating "10 million users" as one uniform load, like
counting calories by counting plates instead of what's on them.

It's three completely different problems that each need their own fix.

**[THE PUNCHLINE]**

Let's tod fod it. 🫡

**[OUTRO]**

Next time: what happens when the video doesn't even exist yet because it's
being filmed live, right now, as people are already watching it. Bro's about
to learn that "buffering" hits different when the future hasn't happened
yet. 🎥

Follow for the finale.

---

*True Story!! 😂*

---

**Caption for post:**
Bro learned "10 million users" isn't one problem, it's three 💀 part 4 —
this is why Hotstar doesn't fall over during IPL finals. Let's tod fod it.
#systemdesign #hiojotstar #scalability #cricket

---

## Voiceover-only script

*(No visual directions — read straight over cat footage. Pause where marked
for diagrams.)*

Bro's app is actually working now. Multiple qualities, smooth playback,
uncle stopped complaining. Bro basically thinks he's Reliance at this
point.

Then bro made a huge mistake. Bro announced he got the streaming rights to
a cricket match.

Ten million people. Same match. Same moment. Everyone hits play within
seconds of each other — a stampede, except everyone's stampeding toward a
loading wheel.

Bro, confidently: "it's fine, I already fixed the video thing." Narrator:
it was not fine.

Here's what bro got wrong. Bro thought "one million users" was one big
scary number that needed one big scary server. It's not one problem. It's
three different problems wearing a trenchcoat.

*(pause — diagram: 10M viewers → login traffic / video traffic / event traffic)*

Login and "what's on" traffic — chill, spread it across a few servers, easy,
bro's grandmother could scale this part.

Video traffic — ten million people asking for a new chunk every few seconds.
That's hundreds of thousands of requests per second. Bro's storage bucket
alone was never surviving that. It needs a CDN, caching the same popular
chunks near every city, so most requests never even reach the origin.

Every pause, every skip, every rage-quit — that's an event. You cannot let
ten million of those hit your main database directly, or the database dies
before the toss even happens. Before a single ball is bowled.

Bro's mistake was treating ten million users as one uniform pile of load.
It's three separate problems. Each one needs its own fix.

Let's tod fod it.
