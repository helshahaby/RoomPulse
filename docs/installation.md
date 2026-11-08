# Installation guide

Requirements: Node 20+ or Bun 1.1+, a webcam, Chrome/Edge (recommended) or Safari 15.4+. No GPU needed.

```bash
git clone <repo> roompulse-ai && cd roompulse-ai
bun install            # or: npm install
bun run dev            # opens on http://localhost:8080
bun run test           # run the automated tests
bun run build          # production build
```

- The camera only works on `localhost` or HTTPS.
- First start downloads the MediaPipe face model (~3.5 MB) and WASM runtime from public CDNs; afterwards they are cached by the browser.
- Allow camera permission when prompted. If denied, the app shows how to fix it.

Good capture: face the camera ~50–80 cm away, light from the front, avoid backlight, keep still for 15–20 s. For respiration, include shoulders and upper chest in frame.
