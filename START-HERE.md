# RoomPulse AI delivery package
Prepared for Hossam Elshahaby, 2026-11-09.

- README.md: product overview and installation.
- docs/: architecture, installation, TrustScore, methodology, test report, demo script, pitch outline, ethics.
- datasets/README.md: reference dataset integration.
- presentation/: editable five-slide PowerPoint and matching PDF.
- reports/: technical specification and fresh automated test log (40/40 passed).
- source/: application source and lockfile; no installed dependencies or build output.
- demo/roompulse-demo.mp4: 59.5-second walkthrough, Brian stock narration. Still-image camera demonstration; not real vital signs. Voice-command cues are illustrative only.

## Run
Extract the ZIP. In a terminal inside source/, run:
```
bun install
bun run dev
bun run test
```
Open the local URL printed by the development server. Camera needs localhost or HTTPS and user permission. Initial face-model loading requires internet.

## Evidence and limitations
40 automated tests passed on 2026-11-09. Synthetic tests do not establish human accuracy. No real-person accuracy or dataset benchmarks are claimed. Respiration is experimental. Front-facing light alone does not guarantee a usable optical signal. RED withholds estimates.

RoomPulse AI is an experimental research prototype. Measurements are not intended for medical diagnosis, treatment, or emergency decision-making.
