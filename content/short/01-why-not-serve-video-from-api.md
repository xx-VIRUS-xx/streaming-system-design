# Short post — X/LinkedIn thread

Learning system design by rebuilding Hotstar from scratch. Day 1 lesson:

Your API server should never serve video bytes directly.

Here's the naive version everyone starts with:

```
User → FastAPI Server → Storage
```

Looks fine for one user. Now put 100,000 users on it.

Every single one of those users is now streaming video *through* your
application server. Congratulations, you just turned your API into a video
delivery network. It wasn't built for that. It falls over.

The fix: split the system into two planes.

- **Control plane** — login, catalog, search, "can this user watch this?"
- **Data plane** — the actual video bytes

The API's only job is to say yes/no and hand back a URL. It never touches
the video itself. The video comes from object storage, fronted by a CDN.

```
API → decides who can watch
CDN  → actually delivers the bytes
```

One rule I keep coming back to: **the API controls access, the CDN delivers
content.** Never let those two jobs live in the same server.

Next up: why streaming apps don't just serve you a movie.mp4.
