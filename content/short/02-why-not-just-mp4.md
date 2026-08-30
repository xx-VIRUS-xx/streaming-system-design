# Short post — X/LinkedIn thread

Learning in public: today's question was "why doesn't Hotstar just give me a
movie.mp4 and let my browser play it?"

Turns out that would break constantly. Here's why.

A single mp4 file locks in one resolution, one bitrate, one codec. But:

- Your mobile network fluctuates between 20 Mbps and 2 Mbps in the same commute
- You switch from Wi-Fi to mobile data mid-episode
- You seek to 1:32:14 and don't want to download everything before it
- Someone's watching on a 480p phone, someone else on a 4K TV

One file can't serve all of that.

The actual approach: cut the video into small segments, and generate multiple
quality versions of each one.

```
Source
  ├── 1080p → segment001, segment002, segment003...
  ├── 720p  → segment001, segment002, segment003...
  └── 480p  → segment001, segment002, segment003...
```

A manifest file tells the player what qualities exist and where the segments
live. The player reads the manifest, checks its current network/buffer
conditions, and picks the next segment — sometimes at a different quality
than the last one. That's adaptive bitrate streaming (HLS / MPEG-DASH).

This is also why seeking is fast: jumping to 1:32:14 just means requesting a
different segment, not downloading everything before it.

One mp4 → many small pieces, many qualities, one map (the manifest). That's
the whole trick.
