# Research problem

> **Do case-history features improve prediction of a future recorded policy change beyond a persistence baseline when every feature is restricted to information available at the prediction date?**

**Why it matters:** Visually aligned time series do not establish forecasting ability. A reproducible retrospective test would clarify whether the data contain useful advance information.

**Central tension:** Smoothing reduces reporting noise, but can leak future observations or blur the timing of a rare policy change. Correlation also does not identify why a government changed policy.

**Current evidence and gap:** [README.md](README.md) documents joining archived policy and case series and plotting their trends. Those exploratory figures do not establish out-of-time forecasting or causal policy effects.

**Decisive verification:** Define a forecast horizon and change label before evaluation. Use rolling-origin splits, trailing-only features and publication availability dates where recorded. Compare persistence and a simple historical-rate baseline with a small predictive model under a fixed feature budget. Report rare-event precision/recall, calibration and variation across periods. If gains vanish under date-correct features or cannot be separated from reporting artifacts, retain the project as exploratory visualization.

This proposes a historical forecasting study; it adds no public-health advice or new result.
