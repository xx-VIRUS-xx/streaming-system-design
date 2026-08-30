# Hio Jotstar — Episode 4: "Everyone Presses Play"

**Format:** Insta Reel / YT Short script.

---

**[HOOK]**

StoryTime part 4 📖 Bro's app is actually working now. Multiple qualities,
smooth playback, no more buffering complaints.

Then bro made a HUGE mistake.

Bro announced he got the streaming rights to a cricket match.

**[THE SETUP]**

10 million people. Same match. Same moment. Everyone hits play within
literal seconds of each other.

Bro, confidently: "it's fine, I already fixed the video streaming thing"

Narrator: it was not fine.

**[THE ROAST]**

tch tch tch bro thought "1 million users" was just... one big number he
needed one big server for. 😩

Nah bro. It's not ONE problem. It's like 3 different problems wearing a
trenchcoat:

```
10M viewers hitting play
        │
   ┌────┼────┐
   ▼    ▼    ▼
 Login  Video  "user paused
 /home traffic  at 3:42" etc
 traffic         (events)
```

Login and "what's on" traffic? Chill, spread it across a few servers, easy.

Video traffic? 10 million people asking for a new chunk every few seconds —
that's HUNDREDS of THOUSANDS of requests per second. Bro's storage bucket
alone was never going to survive that; it needs a CDN caching the same
popular chunks near each city so most requests never even reach the origin.

Every pause/skip/rage-quit event? Also can't hit the main database directly
per event or bro's database dies before the toss even happens. Needs to go
into a queue and get processed later, calmly.

**[THE PAYOFF]**

Bro's mistake: treating "10 million users" as one uniform load. It's not.
It's three completely different problems that each need their own fix.

**[OUTRO]**

Next time: what happens when the video doesn't even exist yet because it's
being filmed live, right now, as people are already watching it. 🎥

Follow for the finale.

---

*True Story!! 😂*

---

**Caption for post:**
Bro learned "10 million users" isn't one problem, it's three 💀 part 4 —
this is why Hotstar doesn't fall over during IPL finals. #systemdesign
#hiojotstar #scalability #cricket
