# Hio Jotstar — Episode 1: "The Ban"

**Format:** Insta Reel / YT Short script. Storytime voice, comedic delivery,
text overlay for the diagram.

---

**[HOOK — first 2 seconds, punchy]**

StoryTime 📖 Once my bro got into beef with Ambani...

**[SETUP]**

...and got PERMANENTLY banned from Jio Hotstar. 😭

Bro couldn't accept defeat. So bro did what any unemployed genius would do —

He built his OWN app.

**[REVEAL — dramatic zoom]**

Ladies and gentlemen... presenting...

# 🔥 HIO JOTSTAR 🔥

**[THE ARCHITECTURE — show as text/diagram overlay]**

Bro's entire backend, for streaming movies to potentially millions of users:

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

**[REACTION — the roast]**

tch tch tch... 😩 Bro is SO naive.

Bro thinks his one little FastAPI server is going to hand out 5GB movie files
to every single user, directly, forever.

Bro's server when 100 people open the app at once:
💀💀💀

**[THE LESSON — quick, no lecture tone]**

See here's the thing nobody tells you: your API server's job is to say "yes
you can watch this" — NOT to actually hand over the video. The second your
app server starts pushing video bytes to users, it IS your video delivery
network now. And it was never built for that job.

That's why real platforms split it into two jobs: one server says "you're
allowed," a completely different system (CDN + storage) actually delivers
the bytes.

**[OUTRO / HOOK FOR NEXT EP]**

Bro found this out the hard way when 100k people showed up on day one.

Next time: bro discovers his server melted. 🔥 Follow for part 2.

---

*True Story!! 😂*

---

**Caption for post:**
Bro got banned from Jio Hotstar so he built Hio Jotstar 💀 spoiler: his
architecture is NOT it. #systemdesign #softwareengineering #buildinpublic
#learningtocod #hiojotstar
