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
you can watch this" — NOT to actually hand over the video. Bro built himself
a bouncer, and then made the bouncer also personally carry every guest into
the club on his back. One at a time. For 100,000 guests.

The second your app server starts pushing video bytes to users, it IS your
video delivery network now. And it was never built for that job — it was
built to check IDs, not deadlift 5GB files.

That's why real platforms split it into two jobs: one server says "you're
allowed," a completely different system (CDN + storage) actually delivers
the bytes.

**[THE PUNCHLINE]**

Let's tod fod it. 🫡

**[OUTRO / HOOK FOR NEXT EP]**

Bro found this out the hard way when 100k people showed up on day one and
his laptop started sounding like a 747 on takeoff.

Next time: bro discovers his server melted. Literally. 🔥 Follow for part 2.

---

*True Story!! 😂*

---

**Caption for post:**
Bro got banned from Jio Hotstar so he built Hio Jotstar 💀 spoiler: his
architecture is NOT it. #systemdesign #softwareengineering #buildinpublic
#learningtocod #hiojotstar

---

## Voiceover-only script

*(No visual directions — read this straight over your cat footage. Pause
where marked for the diagram to sit on screen.)*

Once upon a time, my bro got into beef with Ambani, so bro got banned from
Jio Hotstar.

Now, like any rational developer, bro decided to build his own version —
Hio Jotstar.

But the problem was, the app architecture looked like this.

*(pause — diagram on screen: User → GET /movie.mp4 → FastAPI → Storage)*

Bro is so naive.

Bro's entire app is one server, handing out the movie file directly to
every single person who asks for it. That's fine for bro. That is not fine
for a hundred thousand people opening the app on day one.

Now let me make a correction in the architecture.

The API server's only job should be to say "yes, you're allowed to watch
this." It should never be the one handing over the actual video. The moment
it starts doing that, it's not an API anymore — it's a video delivery
network, and it was never built to survive that.

So the real fix: split it into two jobs. One system checks who's allowed.
A completely different system — storage plus a CDN — actually delivers the
video.

Let's tod fod it.

*(hold on corrected diagram, cut — text overlay: "Let's tod fod it" as end-card stamp)*

