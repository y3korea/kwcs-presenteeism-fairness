# Predicting Presenteeism and Auditing Algorithmic Fairness in Korean Workers

Analysis code and outputs for the manuscript:

> **Predicting Presenteeism and Auditing Algorithmic Fairness in Korean Workers: An Explainable Machine-Learning Study of the 7th Korean Working Conditions Survey**
> Wansuk Choi et al., Department of Physical Therapy, Kyungwoon University, Gumi, Republic of Korea
> *(manuscript under journal submission; citation will be updated upon publication)*

## Overview

Using the 7th Korean Working Conditions Survey (KWCS, 2023; N = 36,574), we

1. train and calibrate presenteeism-prediction models (Logistic Regression, Random Forest, HistGradientBoosting; best test AUC 0.717),
2. explain predictions with SHAP, and
3. — centrally — perform an **algorithmic-fairness audit** (equalized-odds and demographic-parity differences, per-group recall/FPR) across sex, age, education, and employment type.

Headline finding: a model that looks good in aggregate is markedly unfair across age (EqOdds 0.776), education (0.796), and employment type (0.390), while sex (0.028) gives false reassurance.

## Repository structure

| Path | Contents |
|---|---|
| `KWCS7_presenteeism_fairness.ipynb` | Complete analysis notebook (data prep → models → SHAP → fairness audit → figures/tables) |
| `figures/` | Figures 1–6 as published-quality PNG + vector PDF |
| `tables/` | Result tables (model performance, fairness gaps, per-group metrics, SHAP importance) |
| `results/run_summary.txt` | Key numbers from the reference run (run_20260607_201144) |

## Data access (not redistributed here)

The KWCS microdata are **publicly available but not redistributable**: apply and download from the Occupational Safety and Health Research Institute (OSHRI, KOSHA) Korean Working Conditions Survey portal (https://oshri.kosha.or.kr). Place the 7th-wave CSV in an `input/` folder as referenced in the notebook. All data are de-identified public-use secondary data (IRB-exempt).

## How to run

The notebook is designed for Google Colab: upload, **Run all** — the first cell installs `shap` automatically; outputs are written to `output/run_<timestamp>/`. Locally, install requirements first:

```bash
pip install -r requirements.txt
```

## Funding

This research was supported by the Regional Innovation System & Education (RISE) program through the Gyeongbuk RISE Center, funded by the Ministry of Education (MOE) and Gyeongsangbuk-do, Republic of Korea (2026-RISE-15-102).

## License

Code is released under the MIT License (see `LICENSE`). Figures and tables are © the authors; please cite the paper when reusing them.
