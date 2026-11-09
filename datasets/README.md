# Dataset integration guide

No dataset files are included. Datasets stay on your machine and are processed in the browser.

## UBFC-rPPG (Dataset 2)
1. Request access: https://sites.google.com/view/ybenezeth/ubfcrppg
2. Each subject folder has `vid.avi` and `ground_truth.txt` (line 1 PPG, line 2 HR bpm, line 3 time s).
3. Browsers can't decode the AVI. Convert, keeping quality high (compression harms rPPG):
   ```bash
   ffmpeg -i vid.avi -c:v libx264 -crf 0 -pix_fmt yuv444p vid.mp4
   # if your browser can't play it:
   ffmpeg -i vid.avi -c:v libx264 -crf 4 -pix_fmt yuv420p vid.mp4
   ```
4. Validation Lab → adapter "UBFC-rPPG" → load `vid.mp4` + `ground_truth.txt` → set subject ID (e.g. `subject1`) → Run. Processing is real-time (a 1-minute video takes ~1 minute).

## Generic CSV
Any synchronized video plus a CSV:
```csv
time,hr,resp
0.0,72.1,14
0.5,72.4,14
```
`resp` is optional; time is seconds from video start.

## Adding a dataset
Implement `DatasetAdapter` in `src/lib/validation.ts` (`parse(text) → { t, hr, ppg?, resp? }`) and add it to `ADAPTERS`.
