# System architecture

```text
Camera (getUserMedia) ──► FrameProcessor ─────────────► WindowFrame buffer (rolling, ≤ max(window, 30s))
                          │ MediaPipe Face Landmarker            │ every 1 s
                          │ ROIs: forehead(151), cheeks(117,346)  ▼
                          │ YCbCr skin mask → mean RGB      analyzeWindow()
                          │ chest box → 48×32 gray → LK dy   ├─ rppg.estimateHeartRate (POS|CHROM|Green → bandpass → Welch → peak)
                          └ luma, face box                   ├─ respiration.estimateRespiration (integrate dy → bandpass → Welch → autocorr)
                                                             └─ trust.computeTrust (9 weighted factors + hard gates)
                                                                       │
            UI (Monitor / Signals) ◄── MonitorEngine store ◄───────────┘──► Session records → localStorage → CSV/JSON/PDF
Dataset video ──► dataset-runner (same FrameProcessor + analyzeWindow) ──► Pairs(est, ref) ──► validation metrics
```

| Module | File | Role |
|---|---|---|
| DSP | `src/lib/dsp.ts` | detrend, z-score, resample, zero-phase bandpass, FFT, Welch, peak/SNR, autocorr |
| rPPG | `src/lib/rppg.ts` | POS (Wang 2017), CHROM (de Haan 2013), Green (Verkruysse 2008) |
| Respiration | `src/lib/respiration.ts` | LK vertical flow, respiratory rate, periodicity |
| TrustScore | `src/lib/trust.ts` | documented weighted score, gates, explanations |
| Analysis | `src/lib/analysis.ts` | one window → HR, resp, trust (shared by live + dataset) |
| Frame processing | `src/lib/frame-processor.ts` | detection, ROIs, skin mask, chest flow (browser only) |
| Live engine | `src/lib/monitor-engine.ts` | camera lifecycle, loop, overlay, session recording, disconnect handling |
| Validation | `src/lib/validation.ts`, `dataset-runner.ts` | adapters, MAE/RMSE/bias/SD/r, Bland–Altman |
| Storage/Reports | `src/lib/storage.ts`, `reports.ts` | localStorage, CSV/JSON, PDF |

**Real-time:** processing capped at ~30 fps on `requestAnimationFrame`, frames downscaled to ≤640 px, analysis once per second, UI state emitted at 5 Hz. Per-frame latency and actual FPS are displayed. Camera `ended` events stop the session with a clear message; tracking loss just records `face:false` frames and recovers automatically.

**Privacy:** no video leaves the browser; only numeric records are stored; optional raw recording is off by default and kept only as an in-tab blob. The MediaPipe model/WASM files are downloaded from Google/jsDelivr CDNs (code only — no user data).
