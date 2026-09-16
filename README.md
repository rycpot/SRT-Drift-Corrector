# SRT Drift Corrector

A single HTML file that fixes subtitles which slowly fall out of sync with a video.

Common when an `.srt` found online was timed for a different release (different fps, cut, or encode) — the first line matches, but by the end it's seconds or minutes off. Drift corrects this by stretching the whole timeline between two points you give it.

## How it works

If an `.srt` subtitle file is initially in sync but gradually becomes
out of sync with the movie, this tool lets you correct the drift using
two reference points.

You:

1.  Load the `.srt` file.
2.  Choose an earlier subtitle and enter its correct time.
3.  Choose a later subtitle and enter its correct time.
4.  The tool calculates a **linear correction** between those two
    points.
5.  That correction is **extrapolated across the entire subtitle file**.
6.  Download the corrected `.srt` file.

Both the start and end times of every subtitle are adjusted.

## Why two points

A single offset only fixes sync at one moment. If the drift grows over time (usually a frame-rate mismatch between the subtitle source and your video), you need two points to solve for both the offset *and* the rate of drift — Drift does this with simple linear interpolation:

```
scale = (new_B − new_A) / (orig_B − orig_A)
new_time = new_A + (orig_time − orig_A) × scale
```

## Notes

- Works entirely client-side — just a static HTML/CSS/JS file.
- Best results come from picking reference points as far apart as possible.

![enter image description here](https://files.catbox.moe/yrl4te.png)
