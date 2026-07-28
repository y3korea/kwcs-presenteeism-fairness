# Predicting Presenteeism and Auditing Algorithmic Fairness in Korean Workers

Analysis code and outputs for the manuscript:

> **Predicting Presenteeism and Auditing Algorithmic Fairness in Korean Workers: An Explainable Machine-Learning Study of the 7th Korean Working Conditions Survey**
> *(manuscript under journal submission; citation and author list will be completed upon publication)*

## Overview

Using the 7th Korean Working Conditions Survey (KWCS, 2023; N = 36,574; presenteeism prevalence 6.69%), we

1. train and calibrate presenteeism-prediction models (Logistic Regression, Random Forest, HistGradientBoosting; best test AUC **0.716**, PR-AUC 0.206, Brier 0.058),
2. explain predictions with SHAP, and
3. — centrally — perform an **algorithmic-fairness audit** (equalized-odds and demographic-parity differences, per-group recall/FPR/selection rate) across sex, age, education, and employment type.

Headline finding: a model that looks good in aggregate is markedly unfair across **age (equalized-odds difference 0.802)**, **education (0.774)** and **employment type (0.362)**, while **sex (0.019)** gives false reassurance.

| Attribute | k | AUC gap | Recall gap | FPR gap | Equalized odds | Demographic parity |
|---|---:|---:|---:|---:|---:|---:|
| Sex | 2 | 0.013 | 0.002 | 0.018 | **0.019** | 0.018 |
| Age group | 5 | 0.061 | 0.454 | 0.348 | **0.802** | 0.369 |
| Employment type | 3 | 0.078 | 0.181 | 0.181 | **0.362** | 0.187 |
| Education | 3 | 0.026 | 0.348 | 0.425 | **0.774** | 0.439 |

## Reproducibility

The notebook is deterministic. Seeds are fixed for the train–test split, the cross-validation folds and every estimator, and linear-algebra threading is pinned to a single thread.

**Verified:** the notebook was executed twice from a clean state in the environment pinned in `requirements.txt`; the two runs produced **byte-identical result tables and figure files**. Every number in the manuscript is taken from that run (`results/run_summary.txt`).

Results are environment-sensitive: a different scikit-learn version changes the fitted forest slightly, which shifts the Youden-J operating threshold and therefore every threshold-dependent fairness metric. Install the pinned versions to reproduce the published numbers exactly.

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute KWCS7_presenteeism_fairness.ipynb
```

Outputs are written to `output/run_<timestamp>/`.

## Repository structure

| Path | Contents |
|---|---|
| `KWCS7_presenteeism_fairness.ipynb` | Complete analysis notebook (data prep → models → SHAP → fairness audit → figures/tables) |
| `figures/` | Figures 1–6 as publication-quality PNG + vector PDF |
| `tables/` | Result tables (model performance, fairness gaps, per-group metrics, SHAP importance) |
| `results/run_summary.txt` | Key numbers from the reference run |
| `requirements.txt` | Pinned environment that produced the reported results |

Figure filenames follow the notebook's internal numbering; the manuscript renumbers them in citation order:

| Manuscript | File | Content |
|---|---|---|
| Fig. 1 | `fig1_performance` | ROC + calibration |
| Fig. 2 | `fig5_decision_curve` | Decision-curve analysis |
| Fig. 3 | `fig2_shap` | SHAP beeswarm |
| Fig. 4 | `fig3_fairness_dumbbell` | Recall / selection-rate disparity |
| Fig. 5 | `fig4_group_roc` | Per-group ROC |
| Fig. 6 | `fig6_disparity_heatmap` | Fairness-metric matrix |

## Data access (not redistributed here)

The KWCS microdata are **publicly available but not redistributable**: apply and download from the Occupational Safety and Health Research Institute (OSHRI, KOSHA) Korean Working Conditions Survey portal — https://oshri.kosha.or.kr/eoshri/resources/KWCSDownload.do. Place the 7th-wave CSV in an `input/` folder as referenced in the notebook. All data are de-identified public-use secondary data (IRB-exempt).

## Funding

This research was supported by the ANCHOR program through the Gyeongbuk ANCHOR Center, funded by the Ministry of Education (MOE) and Gyeongsangbuk-do, Republic of Korea (2026-ANCHOR-15-102).

## License

Code is released under the MIT License (see `LICENSE`). Figures and tables are © the authors; please cite the paper when reusing them.
