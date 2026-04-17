# 6-7 Flip Challenge 🤚🤚

A browser-based hand-tracking game inspired by the viral 6-7 meme. Use your webcam and both hands to rack up as many flips as possible before the timer runs out — no controller, no keyboard, just you and your hands.

---

## What is the 6-7 Movement?

Hold both hands out horizontally in front of your webcam, palms facing the camera. The challenge is simple: alternate which hand goes up and which goes down, back and forth as fast as you can. One hand up, other hand down — then swap. That's one flip. Go.

---

## Features

- **Real-time hand tracking** powered by MediaPipe Hands — runs entirely in the browser, no installs
- **Three time modes** — 10s, 30s, and 60s challenges
- **Personal best tracking** per mode, saved to localStorage
- **Streak counter** with combo popups and bonus sounds at x5, x10, and every 10 after
- **Speed meter** showing your current flips/sec
- **Auto-calibration** phase before each round to tune detection to your environment
- **Single-hand fallback** — counting continues even if one hand drops out of frame momentarily
- **Fully client-side** — just open the HTML file, no server needed

---

## How to Play

1. Open `index.html` in a Chromium-based browser (Chrome or Edge recommended)
2. Allow webcam access when prompted
3. Select your time mode (10s / 30s / 60s)
4. Click **START GAME**
5. Hold both hands horizontally in front of the camera during the calibration phase
6. When the countdown hits GO — start flipping!

---

## Tech Stack

| Technology | Purpose |
|---|---|
| [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) | Real-time hand landmark detection |
| MediaPipe Camera Utils | Webcam frame capture pipeline |
| Web Audio API | Procedural sound effects (no audio files) |
| Vanilla JS + HTML5 Canvas | Game logic, rendering, UI |
| localStorage | Personal best persistence |

Zero dependencies to install. Everything loads from CDN.

---

## Detection Algorithm

The game tracks the **wrist landmark (point 0)** of each hand and watches the direction of vertical travel over a rolling 6-frame buffer. A flip is registered when:

- **Both hands visible:** one hand is moving UP while the other moves DOWN simultaneously
- **One hand visible (fallback):** the visible hand alternates between upward and downward motion

MediaPipe is configured with relaxed confidence thresholds (`detection: 0.4`, `tracking: 0.3`) to handle fast motion and partial blur without losing tracking mid-game.

---

## Browser Compatibility

| Browser | Support |
|---|---|
| Chrome 90+ | ✅ Full support |
| Edge 90+ | ✅ Full support |
| Firefox | ⚠️ May have webcam/MediaPipe issues |
| Safari | ❌ Not recommended |

A webcam is required. Works on desktop and laptop — not designed for mobile.

---

## Project Structure

```
index.html   ← entire game (single file, self-contained)
README.md    ← this file
```

---

## Tips for Best Detection

- **Good lighting** makes a big difference — face a light source, don't have one behind you
- **Plain background** helps MediaPipe distinguish your hands
- **Keep hands in frame** during the calibration phase so the threshold tunes correctly
- **Distance:** about 50–80cm from the camera works best
- Hold hands roughly at chest height, fingers pointing toward the camera

---

## License

MIT — do whatever you want with it.
