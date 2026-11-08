# Scientific validation methodology

1. **Data source labels.** Every result is tagged: Real · live camera, Real · dataset, Synthetic test data, or Simulated demonstration. They are never mixed in one metric.
2. **Pipeline parity.** Dataset videos are decoded in the browser and passed frame-by-frame (using `requestVideoFrameCallback` media timestamps) through the *same* `FrameProcessor` and `analyzeWindow` used live, with default configuration.
3. **Windowing.** Sliding windows (default 20 s, 1 s step). Reference HR = mean of synchronized reference HR samples inside the window.
4. **Abstention.** A window whose TrustScore is RED yields `est = null`. It counts as *rejected* — it reduces availability but is not included in error metrics.
5. **Metrics** (on windows with both est and ref): MAE, RMSE, bias = mean(est − ref), SD of error, Pearson r; plus availability % and valid-window %.
6. **Bland–Altman** only with ≥ 10 valid pairs: bias ± 1.96 SD limits of agreement.
7. **Grouping:** per subject, per condition label, per algorithm.
8. **Respiration** validation metrics are computed only when the reference contains a synchronized respiration column; no respiratory validation is reported in this submission.

**Status:** the code path is implemented and unit-tested. **No dataset evaluation has been run by the authors in this build** (UBFC-rPPG requires an access request). Results appear in the app only after a user loads data.
