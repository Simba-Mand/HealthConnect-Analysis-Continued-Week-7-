# Week 7 — HealthConnect Analytics Testing & Refinement

**AnalystLab Africa Experience Lab | Data Analytics Track**
**Author:** Simbarashe Mandiveyi

## Overview

Week 7 shifts from *building* analysis (Weeks 5–6) to *testing* it. The goal was to independently verify that the KPIs, dashboard, and validated findings from previous weeks are actually correct, robust across sub-segments, and safe to hand forward to the Data Science track and into Week 8's final deliverable — not to produce new analysis.

## What was tested

| Test | Method | Result |
|---|---|---|
| Data cleaning integrity | Compared raw vs. cleaned dataset outcome counts and record IDs | ✅ Identical — no rows or values altered |
| Interactive dashboard accuracy | Ran 4 independent filter scenarios (including a deliberate small-sample edge case, n=8) against the Week 5 Excel dashboard and cross-checked every KPI card and chart value against an independent pandas calculation | ✅ Matched exactly in all 4 scenarios |
| Lead-time finding robustness | Re-tested within 9 demographic subgroups (gender × age group) | ✅ Held in 7 of 9 — minor exceptions only in small/edge subgroups |
| Prior-no-show finding robustness | Re-tested within all 4 appointment types | ✅ Held with zero exceptions |
| Feature-ranking generalisation (cross-track test with Data Science) | Re-ran the Week 6 effect-size ranking on a 70/30 train/test split | ✅ Ranking fully stable — no feature changed relative position |

## Issue found and fixed

The Week 6 risk-matrix heatmap displayed a no-show rate for every lead-time × prior-no-show cell but gave no indication of sample size. Three cells in the "3+ prior no-shows" row were based on only 10–26 records, yet shown with the same visual weight as cells built on over 1,000 records — a real risk of a viewer over-trusting a small, noisy result.

**Fix:** the heatmap was rebuilt to show the record count per cell and flag any cell under 30 records with a dashed border and warning marker. Retested against the same underlying data to confirm it flags exactly the three problematic cells, with the validated rates themselves unchanged.

## Cross-track collaboration

**Data Analytics → Data Science:** the feature-recommendation file handed to the Data Science track in Week 6 was re-validated this week by testing whether its effect-size ranking holds on a held-out 30% data split, mirroring their own Week 7 train/test methodology. The ranking was fully stable, upgrading the file's status from "validated on the full sample" to "validated on the full sample and confirmed to generalise on unseen data."

## Files in this folder

- `S_Mandiveyi_HealthConnect_Week7_Testing_Refinement_Notebook.ipynb` — full executed testing notebook (all tests, code, and results)
- `S_Mandiveyi_HealthConnect_Week7_Testing_Refinement_Report.docx` — visual report version of the same testing and refinement work
- `S_Mandiveyi_HealthConnect_Week7_Project_Summary.docx` — concise Week 7 project summary
- `HealthConnect_DataScience_Feature_Recommendations.csv` — updated with a Week 7 generalisation-validation status column

## Key takeaway

The analytical foundation built in Weeks 5–6 is calculation-accurate and largely robust — and the one real weakness found (the heatmap) was caught and corrected within the same week, rather than carried forward into final integration.
