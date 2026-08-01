# A Leakage-Audited, Regime-Robust Protocol for Evaluating Stock-Movement Prediction From Affective Text

Reproducibility package (2026). Working paper, under review.

## TL;DR
A leakage-audited, regime-stratified evaluation protocol for machine-learning models
trained on temporal, class-imbalanced affective-text streams. Demonstrated on
stock-movement prediction from a corpus of 3.06 million cleaned social-media and news
messages (from approximately 3.4 million collected) on seven U.S. mega-cap companies
(2015–2023), with 2022 and 2023 held out as separate bear- and bull-market test years.

**Key result.** On identical data and features, validation AUC is 0.83 under a random
split but only 0.54 under a chronological split — a 0.286 gap that is look-ahead
leakage, not skill. Once audited, the sentiment ablation lift stays within the range
of a noise placebo in every regime (real +0.71% vs. placebo −1.31% in 2023; real
−0.63% vs. placebo −1.53% in 2022), and no model beats a majority-class baseline.

## Contents
```
sentiment_pipeline/
├── data/            derived daily features and per-ticker probabilities (parquet)
├── models/          trained models (.joblib) and canonical metric files (.json)
└── RESULTS.txt      logged metrics for the definitive run (AUC, CIs, ablation, backtest)
Pipeline.ipynb       full pipeline, executed (with cell outputs)
requirements.txt     dependencies
figures/             figures 1–9
```

## Canonical metrics (please read)
The numbers reported in the manuscript are those **saved to disk** in
`models/*.json` (`test_metrics.json`, `ablation.json`, `backtest_summary.json`,
`abstention_curve.json`) and in `RESULTS.txt`. **These JSON / RESULTS files are the
single source of truth.**

The notebook was executed several times during development, and some inline cell
outputs retained from earlier runs may show different ablation/placebo values than
the saved artifacts. Where they disagree, the saved `*.json` artifacts and
`RESULTS.txt` are authoritative and are the values that appear in the manuscript and
figures. The definitive ablation values are:

| Test year | Sentiment lift (real) | Noise-placebo lift |
|-----------|----------------------:|-------------------:|
| 2023 bull |                +0.71% |             −1.31% |
| 2022 bear |                −0.63% |             −1.53% |

Mean absolute same-day Pearson correlation between sentiment and returns is ≈ 0.196
at lag 0, falling to ≈ 0.030 at lag 1.

## Reproduce
```bash
pip install -r requirements.txt
# then run Pipeline.ipynb end-to-end (on Kaggle: Save & Run All, GPU T4x2)
```

## Cite / archive
Archived on Zenodo. Please cite the concept DOI, which always resolves to the latest
version: https://doi.org/10.5281/zenodo.20945551

## License
Code under MIT. Raw third-party text data remain under their providers' licenses.

