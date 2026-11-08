# TrustScore specification

TrustScore is a **measurement-reliability score**, not a medical confidence or probability of accuracy.

Each factor maps to a 0–1 sub-score via a linear ramp (clamped). Score = 100 × Σ wᵢ·sᵢ / Σ wᵢ.

| Factor | Ramp (0 → 1) | Default weight |
|---|---|---|
| Face detection stability (fraction of frames with face) | 0.5 → 1.0 | 1.5 |
| Skin-region visibility (skin pixel fraction in ROIs) | 0.2 → 0.7 | 1.0 |
| Motion interference (80th-pct face speed, face-widths/s) | 0.4 → 0.05 | 1.5 |
| Lighting level (mean ROI luma) | 40 → 100 | 0.75 |
| Lighting consistency (luma CV) | 8% → 1% | 0.75 |
| Signal-to-noise ratio (dB, de Haan definition) | −6 → +3 | 2.0 |
| Spectral peak prominence (peak / band median) | 3 → 12 | 1.0 |
| Frequency stability (SD of last 5 estimates, BPM) | 10 → 2 | 1.0 |
| Valid observation duration | min → 2×min s | 0.5 |

**Hard gates (force RED):** face in < 80% of frames · motion > 0.6 fw/s · window < minimum (10 s) · luma < 35 · SNR < 0 dB · pulsatile green amplitude < 0.0002 (static scene / photo).

**States:** GREEN ≥ 70 · AMBER ≥ 50 · else RED. RED never displays a number. All weights, thresholds and gates are editable in **Signals → TrustScore configuration**.

The SNR and amplitude gates were added after testing showed a still photo could otherwise score GREEN — a concrete example of why every gate exists.
