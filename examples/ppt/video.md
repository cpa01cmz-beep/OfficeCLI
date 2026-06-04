# Embedded Video (media)

Three files work together:

- **video.py** — Python build script (requires `imageio`, `imageio-ffmpeg`, `numpy`).
- **video.pptx** — The generated 4-slide deck.
- **video.md** — This file.

## Regenerate

```bash
cd examples/ppt
pip install imageio imageio-ffmpeg numpy
python3 video.py
# → video.pptx
```

## Slides

### Slide 1 — Title slide

Background gradient (`radial:`), title placeholder (`ctrTitle`), subtitle placeholder (`subTitle`).

### Slide 2 — Embedded video with `autoPlay` and `volume`

```bash
officecli add deck.pptx /slide[2] --type video \
  --prop src=/path/to/video.mp4 \
  --prop poster=/path/to/cover.png \
  --prop x=2cm --prop y=4cm --prop width=22cm --prop height=12.5cm \
  --prop volume=80 --prop autoPlay=true
```

`src=` embeds the video (alias `path=`). `poster=` sets the static preview
thumbnail. `volume=` is 0–100. `autoPlay=true` starts playback when the
slide is shown.

### Slide 3 — Video stats + chart

Demonstrates embedding a chart on the same slide as a video.

### Slide 4 — `loop` / `trimStart` / `trimEnd`

```bash
officecli add deck.pptx /slide[4] --type video \
  --prop src=/path/to/video.mp4 \
  --prop x=2cm --prop y=4cm --prop width=22cm --prop height=12.5cm \
  --prop autoPlay=true \
  --prop loop=true \
  --prop trimStart=0 \
  --prop trimEnd=2
```

| Property | Type | Effect |
|---|---|---|
| `loop=true` | bool | video restarts after it ends |
| `trimStart=N` | number (seconds) | playback starts at N seconds |
| `trimEnd=N` | number (seconds) | playback stops at N seconds |

`trimStart`/`trimEnd` are clamped to actual video duration. Both can
be combined with `loop=true` to create a looping clip from a specific
sub-range.

**Features:** `src` (embed), `poster` (thumbnail), `volume`, `autoPlay`,
`loop`, `trimStart`, `trimEnd`.

