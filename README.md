# A Leakage-Audited, Regime-Robust Protocol for Evaluating Stock-Movement Prediction From Affective Text

Reproducibility package for the IEEE Access submission (2026).

## TL;DR
A leakage-audited, regime-stratified evaluation protocol for machine-learning models
trained on temporal, class-imbalanced affective-text streams. Demonstrated on
stock-movement prediction from ~3.4M social-media/news messages on seven U.S.
mega-cap companies (2015–2023, 2023 held out).

**Key result.** On identical data and features, validation AUC is 0.83 under a random
split but only 0.54 under a chronological split — a 0.286 gap that is look-ahead
leakage, not skill. Once audited, the sentiment ablation lift stays within the range
of a noise placebo in every regime, and no model beats a majority-class baseline.

## Contents
```
sentiment_pipeline/
├── data/            derived daily features and per-ticker probabilities (parquet)
├── models/          trained models (.joblib) and canonical metric files (.json)
└── RESULTS.txt      logged metrics for every run (AUC, CIs, ablation, backtest)
pipeline.ipynb       full pipeline, executed (with cell outputs)
requirements.txt     dependencies
figures/             figures 1–9
```

## Canonical metrics (please read)
The numbers reported in the paper are those **saved to disk** in
`models/*.json` (e.g. `test_metrics.json`, `ablation.json`, `backtest_summary.json`,
`abstention_curve.json`) and `RESULTS.txt`. These JSON/RESULTS files are the single
source of truth. The notebook's inline cell outputs may differ by a small margin
because a few models are re-fit at several points without a globally fixed seed; the
saved artifacts are the authoritative values and match the manuscript and figures.

## Reproduce
```bash
pip install -r requirements.txt
# then run pipeline.ipynb end-to-end (on Kaggle: Save & Run All, GPU T4x2)
```

## Cite / archive
Archived on Zenodo: https://doi.org/10.5281/zenodo.20945552

## License
Code under MIT. Raw third-party text data remain under their providers' licenses.

