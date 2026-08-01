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

## Repository contents
```
Pipeline.ipynb      full pipeline; the Canonical Results cells at the end
                    reproduce the paper's figures from the saved artifacts
figures/            figures 1–9
requirements.txt    dependencies
README.md           this file
CHANGELOG.md        version history
```

## Data and trained artifacts (hosted on Zenodo)
The derived features, trained models, and canonical metric files are **not stored in
this repository** (they are large binary artifacts). They are archived on Zenodo:

**https://doi.org/10.5281/zenodo.20945551** (concept DOI — always resolves to the
latest version).

To reproduce the results, download the archive from Zenodo and place the
`sentiment_pipeline/` folder at the root of this repository, so that the paths below
exist:
```
sentiment_pipeline/
├── data/            derived daily features and per-ticker probabilities (parquet)
├── models/          trained models (.joblib) and canonical metric files (.json)
└── RESULTS.txt      logged metrics for the definitive run
```
Then open `Pipeline.ipynb` and run the **Canonical Results** cells at the end. On
Kaggle, attach the equivalent dataset instead; the canonical cells auto-detect the
`sentiment_pipeline/` folder.

## Canonical metrics (please read)
The numbers reported in the manuscript are those **saved to disk** in
`sentiment_pipeline/models/*.json` (`test_metrics.json`, `ablation.json`,
`backtest_summary.json`) and in `RESULTS.txt`. **These JSON / RESULTS files are the
single source of truth.** Some inline cell outputs retained from earlier development
runs may differ; where they disagree, the saved artifacts and the Canonical Results
cells are authoritative. Definitive ablation values:

| Test year | Sentiment lift (real) | Noise-placebo lift |
|-----------|----------------------:|-------------------:|
| 2023 bull |                +0.71% |             −1.31% |
| 2022 bear |                −0.63% |             −1.53% |

Mean absolute same-day Pearson correlation between sentiment and returns is ≈ 0.196
at lag 0, falling to ≈ 0.030 at lag 1.

## Reproduce
```bash
pip install -r requirements.txt
# download sentiment_pipeline/ from Zenodo (see above), then:
# open Pipeline.ipynb and run the Canonical Results cells
```

## Cite
Please cite the concept DOI: https://doi.org/10.5281/zenodo.20945551

## License
Code under MIT (see LICENSE). Raw third-party text data remain under their providers'
licenses.

