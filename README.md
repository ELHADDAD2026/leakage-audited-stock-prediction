# A Leakage-Audited, Regime-Robust Protocol for Evaluating Stock-Movement Prediction From Affective Text

Code and reproducible pipeline for the paper *"A Leakage-Audited, Regime-Robust
Protocol for Evaluating Machine-Learning Models on Affective Text"*
(A. El Haddad, S. Achchab, Y. Lahrichi), submitted to **IEEE Access**.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20945552.svg)](https://doi.org/10.5281/zenodo.20945552)

## Overview

This project tests whether affective features — FinBERT sentiment, sarcasm, six
emotion dimensions, and emoji scores — extracted from roughly 3.06 million
social-media and news messages improve machine-learning prediction of the daily
and ten-day movement of seven U.S. mega-cap stocks (AAPL, MSFT, NVDA, GOOGL,
AMZN, META, TSLA).

Under a leakage-audited, regime-stratified evaluation, the apparent gains do
**not** survive: sentiment co-moves with the market regime rather than
anticipating it. This repository provides the full evaluation protocol so the
analysis can be reproduced and reused on other temporal, class-imbalanced
affective-text problems.

## Method / pipeline

1. **Multi-source data collection** (see *Data sources* below)
2. **NLP scoring:** FinBERT sentiment, sarcasm, six emotion dimensions, emoji sentiment
3. **Feature engineering:** 49 features per stock-day (31 technical + 18 NLP), all lagged one day
4. **Leakage audit** + strict chronological split (train ≤ 2021 / validation 2022 / test 2023)
5. **Models:** LightGBM, XGBoost, CatBoost, and a bidirectional GRU
6. **Evaluation:** AUC vs. majority-class baseline, noise placebo, walk-forward
   re-estimation, ablation, SHAP attribution, Granger causality, abstention curves

## Data sources

Kaggle datasets, FNSPID, Finnhub, Alpha Vantage, a Hugging Face financial-news
set, and RSS feeds. Price data from Yahoo Finance.

> Raw third-party text data are under their respective providers' licenses and
> are **not** redistributed here. The derived daily features used in the paper
> are available from the corresponding author upon reasonable request.

## Reproduce

The full pipeline runs on Kaggle:

- **Kaggle notebook:** `<PASTE YOUR KAGGLE NOTEBOOK URL HERE>`

To run locally (optional):

```bash
pip install -r requirements.txt
# then run the notebook cells in order (data collection -> NLP scoring ->
# features -> leakage audit -> training -> evaluation/robustness)
```

Requirements: Python 3.10+, and the packages listed in `requirements.txt`.

## Key results

| Test | Result |
|---|---|
| Daily direction | No better than chance (AUC ≈ 0.51) |
| Ten-day direction (best model, 2023 bull) | AUC 0.687 — never beats the majority-class baseline (0.683) |
| Sentiment lift by regime (10-day) | +2.68% (2021) / **−0.01% (2022 bear)** / +3.37% (2023 bull) |
| Noise placebo | Lift collapses from +3.37% to +0.58% |
| Lag structure | \|r\| ≈ 0.18 same-day vs 0.03 next-day → contemporaneous, not predictive |
| Random vs chronological split | Validation AUC 0.828 vs 0.543 (gap 0.285 = look-ahead leakage) |

**Conclusion:** sentiment follows the market regime; it does not lead it.

## Citation

If you use this code, please cite:

```bibtex
@article{elhaddad2026leakage,
  author  = {El Haddad, Abdelkhaleq and Achchab, Said and Lahrichi, Younes},
  title   = {A Leakage-Audited, Regime-Robust Protocol for Evaluating
             Machine-Learning Models on Affective Text},
  journal = {IEEE Access},
  year    = {2026},
  note    = {To appear},
  doi     = {10.5281/zenodo.20945552}
}
```

## License

Code: MIT (see `LICENSE`). Data: under the original providers' licenses.

## Contact

Abdelkhaleq El Haddad — abdelkhaleq_elhaddad@um5.ac.ma
ENSIAS, Mohammed V University, Rabat, Morocco

