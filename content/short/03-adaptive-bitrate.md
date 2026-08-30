# Short post — X/LinkedIn thread

Learning in public: how does the video player actually decide "give me 1080p"
vs "give me 480p"? This tripped me up until I traced through the numbers.

Say a video has these representations:

```
1080p → 8 Mbps
720p  → 5 Mbps
480p  → 2 Mbps
360p  → 800 Kbps
```

You start on decent Wi-Fi, ~15 Mbps available. Player picks 1080p — plenty of
headroom.

Then you walk out the door onto mobile data. Bandwidth drops to ~3 Mbps.

The player doesn't know your bandwidth number directly — it watches its own
buffer. If the buffer is draining faster than it refills, that's the signal
something's wrong. It responds by requesting the *next* segment at a lower
quality:

```
1080p → 720p → 480p
```

Not the whole video — just the next chunk. That's why quality changes
mid-playback without a restart or a spinner: it's a segment-by-segment
decision, not a whole-file one.

The part that reframed it for me: adaptive bitrate isn't really about
"detecting your network speed." It's about protecting the buffer from running
dry. Bandwidth estimation is just one input into that.
