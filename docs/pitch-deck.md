# Pitch deck (5 slides)

## 1 — RoomPulse AI: The Invisible Health Guardian
Contactless vital-sign intelligence from an ordinary camera. Research prototype · BioHack 2026.

## 2 — The Problem: Wearable Dependency
- Devices must be worn, charged and tolerated — adherence drops exactly where risk is highest (older adults, bed-bound, cognitive impairment).
- Skin irritation, discomfort, stigma; hospitals juggle cables.

## 3 — The Solution: Contactless Vital-Sign Intelligence
- Heart rate from skin colour micro-changes (POS / CHROM rPPG).
- Breathing from shoulder/chest motion (optical flow) — experimental.
- **TrustScore**: 9 transparent factors + hard gates. If it can't measure, it says so and why.

## 4 — Technical Architecture & Scientific Validation
- 100% on-device: MediaPipe face landmarks → skin ROIs → POS/CHROM/Green → Welch PSD.
- Identical pipeline for live and dataset evaluation; UBFC-rPPG adapter; MAE, RMSE, bias, Bland–Altman.
- 37 automated tests. Results reported only from data actually processed.

## 5 — Live Demonstration, Impact & Future Potential
- Live demo: stationary → reading; movement / photo → abstention.
- Impact: passive monitoring in homes, care facilities, observation wards.
- Next: multi-person, diverse-skin-tone validation, clinical study, exposure-locked capture.
