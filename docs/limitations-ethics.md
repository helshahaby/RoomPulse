# Limitations and ethical considerations

## Limitations
- Not a medical device; no regulatory clearance; must not drive clinical or emergency decisions.
- Heart-rate accuracy on real people has **not** been measured in this build; no dataset results are claimed.
- rPPG is known to degrade with darker skin tones under low light, motion, makeup, beards, glasses glare, webcam auto-exposure/white balance, and video compression.
- Respiration is experimental: needs visible shoulders, a still subject, and is unvalidated.
- Browser frame timing is irregular; resampling mitigates but doesn't remove jitter.
- Single subject only. The skin mask is a fixed YCbCr rule, which may under-select some skin tones (visible as lower skin-visibility sub-score).
- The static-scene gate is a heuristic, not anti-spoofing.

## Ethics & privacy
- Video is processed locally and never uploaded; raw video is not stored unless the user opts in per session (kept only in the tab).
- No identity recognition; face landmarks are used only to locate skin regions.
- No diagnoses, no alerts. All stored data can be deleted with one click (History → Clear all data).
- Consent: anyone monitored must agree; camera-based monitoring in shared spaces needs clear signage and opt-out.
- Fairness: before any real use, validate across Fitzpatrick skin types, ages and lighting conditions and publish subgroup errors.
