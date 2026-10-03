# Frame Fitting Mirror (web)

A single-page glasses try-on. It opens the front camera, tracks 478 face landmarks with
MediaPipe Face Landmarker, and draws the selected frame over the eyes so it follows
position, size, tilt and head turn.

## Run it

The camera needs https or localhost:

```sh
cd web
python3 -m http.server 8000
# open http://localhost:8000
```

No camera? Use **Use a photo** to try frames on a still image.

## What's inside

- `index.html` — the whole app (HTML, CSS, JS in one file).
- `tryon.html` — the same page without the `<html>/<head>` wrapper, used for the Claude artifact build.
- `vendor/` — MediaPipe tasks-vision 1.0.1 (JS bundle, WASM) and the `face_landmarker.task` model,
  so the page works offline. If they are missing it falls back to jsDelivr and Google's model host.

## Extending

Frames, finishes and lens tints are plain data at the top of the script (`FRAMES`, `FINISHES`, `TINTS`).
Each frame is drawn on a canvas in a 1000-unit space (temple to temple, eye line at y = 0), so no
image assets are needed and the same definitions can be reused in the mobile app.

Face measurements (face shape, PD, width) are estimates that use the average iris width (11.7 mm)
as a ruler. They are a guide, not a prescription.
