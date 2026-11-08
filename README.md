# RoomPulse AI — The Invisible Health Guardian

**BioHack 2026 · Vitals, No Wearable.** Contactless heart rate (rPPG) and experimental respiration from an ordinary webcam, with a transparent TrustScore that withholds any reading it cannot support.

> RoomPulse AI is an experimental research prototype. Measurements are not intended for medical diagnosis, treatment, or emergency decision-making.

## What works (and how it was checked)

| Capability | Status | Evidence |
|---|---|---|
| Webcam capture, start/pause/stop, FPS + latency display | Done | Headless Chromium with fake camera device |
| Face detection + forehead/cheek ROIs (MediaPipe Face Landmarker, CPU) | Done | Headless run with a still face image as camera: face + 3 ROIs tracked |
| POS, CHROM, Green rPPG + Welch PSD | Done | Unit tests on synthetic signals (72/96 BPM recovered within ±3–4 BPM) |
| TrustScore GREEN/AMBER/RED + rejection reasons | Done | Unit tests; still-photo camera input correctly → RED "no pulsatile skin signal" |
| Respiration (optical flow on shoulders/chest) | **Experimental** | Synthetic unit test only; **not validated against ground truth** |
| History, CSV/JSON/PDF export, clear-all | Done | Unit tests for persistence + CSV |
| Validation Lab (UBFC-rPPG + generic CSV adapters) | Done (code) | Metric unit tests. **No dataset results included** — the dataset isn't bundled |
| Real-face heart-rate accuracy | **Untested by us** | Requires a live person or a reference dataset run |

## Architecture deviation from the brief

The brief suggested a Python/FastAPI backend. This build runs **entirely in the browser (TypeScript)**: the hosting platform is a React/TanStack Start stack, and on-device processing is also the strongest privacy guarantee — video never leaves the machine. The same algorithms (detrend, Butterworth-style zero-phase bandpass, POS, CHROM, Welch, Lucas–Kanade flow) are implemented in `src/lib/` and unit-tested. No GPU required.

See [docs/architecture.md](docs/architecture.md).

## Run

```bash
bun install          # or npm install
bun run dev          # http://localhost:8080  (camera needs localhost or HTTPS)
bun run test         # 37 tests
```

## Documents

- [Installation guide](docs/installation.md)
- [System architecture](docs/architecture.md)
- [TrustScore specification](docs/trustscore.md)
- [Scientific validation methodology](docs/validation-methodology.md)
- [Dataset integration guide](datasets/README.md)
- [Test report](docs/test-report.md)
- [3-minute demo script](docs/demo-script.md)
- [5-slide pitch deck](docs/pitch-deck.md)
- [Limitations & ethics](docs/limitations-ethics.md)
- Technical specification / research report PDF: generated in-app at **Reports → Full research report**.
