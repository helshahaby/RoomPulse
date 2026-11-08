# Test report

Run: `bun run test` (Vitest, jsdom). Result on 2026-11-08: **5 files, 37 tests, all passed.**

| Suite | Tests | Covers |
|---|---|---|
| `signal.test.ts` | 13 | Welch on known 1.2 Hz sine; Hz→BPM; bandpass rejection; invalid fs; POS/CHROM/Green recover 72 BPM; POS 96 BPM with noise; pure noise low SNR; insufficient duration; too-low frame rate; respiration 15 br/min synthetic; respiration insufficient duration |
| `trust-validation.test.ts` | 13 | TrustScore stable→GREEN, motion→RED with reason, poor lighting, missing face, low SNR→RED, short window; MAE/RMSE/bias; rejected windows; missing reference; Bland–Altman threshold; UBFC + CSV parsing; CSV export |
| `analysis.test.ts` | 6 | Window pipeline: clean→BPM, face leaves frame→withheld, head movement→withheld, static photo→withheld, no upper body→no respiration; session persistence |
| `camera.test.ts` | 4 | No camera API, permission denied, no hardware, success |
| `app-routing.test.tsx` | 1 | Home route resolves |

All signal tests use **synthetic** data and verify algorithm behaviour, not physiological accuracy.

## Manual / browser checks
- Headless Chromium + fake camera (no face): camera connects, ~27 fps, "no face", RED with reasons. ✅
- Headless Chromium + still face photo as camera: face box + 3 ROIs + chest box drawn, ~25 fps, ~17 ms/frame. Initially scored GREEN 68 BPM (a false reading) → fixed with SNR + pulsatile-amplitude gates → now RED "no pulsatile skin signal". ✅
- **Not tested:** live human subject accuracy, UBFC dataset run, PDF content visually, Safari/Firefox.
