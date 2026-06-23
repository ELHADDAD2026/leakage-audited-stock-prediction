# leakage-audited-financial-sentiment
Replication code for "A leakage-audited, regime-robust protocol for evaluating learning models on financial sentiment text" — Neurocomputing (under review)
# Leakage-audited, regime-robust evaluation of affective-text stock prediction

Code accompanying the paper:

> **A leakage-audited, regime-robust protocol for evaluating learning models on affective financial text** — *When emotion- and sarcasm-based stock-movement prediction reflects regime co-movement, not skill.*
> [Authors]. Submitted to *Neurocomputing*, 2025. DOI: [to be added on acceptance].

This repository contains the full pipeline used to extract affective features
(FinBERT sentiment, sarcasm, emotions, emoji) from ~3.06 million social-media and
news messages, combine them with technical indicators, train gradient-boosted
ensembles (LightGBM, XGBoost, CatBoost) and a BiGRU, and evaluate them under a
**leakage-audited, regime-robust protocol** for seven U.S. mega-cap stocks
(AAPL, MSFT, GOOGL, AMZN, META, TSLA, NVDA), 2015–2023.

---

## 1. Data sources and licenses

Raw data are **not redistributed** here; they originate from third parties under
their own licenses and must be obtained from the original providers:

| Source | Content | How to obtain |
|---|---|---|
| Yahoo Finance (via `yfinance`) | Daily OHLCV prices | `yfinance` package |
| FNSPID | Financial news + prices | Public dataset (see provider) |
| Finnhub | News / market data | API key required (free tier) |
| Hugging Face datasets | Social-media / news text | `datasets` library |

The **derived daily features** (the modeling table) are available from the
corresponding author on reasonable request.

---

## 2. Environment

```bash
python >= 3.10
pip install -r requirements.txt
```

`requirements.txt` (minimum):

```
pandas
numpy
scikit-learn
lightgbm>=3.3
xgboost
catboost
transformers
torch
datasets
yfinance
matplotlib
shap
statsmodels
pyarrow
```

A GPU is recommended for the FinBERT (Cell 7) and BiGRU (Cell 13b) steps.

---

## 3. Secrets (API keys)

Do **not** hard-code credentials. Set them as environment variables before running:

```bash
export FINNHUB_KEY="your_key"
export HF_TOKEN="your_token"   # if needed
```

The notebook reads them via `os.environ[...]`.

---

## 4. How to run (execution order)

The notebook (`notebook.ipynb`) is organized as a linear pipeline. Run the cells
in order:

| Step | Cell | Produces |
|---|---|---|
| Setup | 1, 2 | config + helpers (checkpoint system) |
| Prices | 4 | market data |
| Text collection | 5 | raw corpus |
| Cleaning + sarcasm score | 6 | cleaned text |
| FinBERT sentiment | 7 | sentiment scores |
| Sarcasm ML + emotion | 8 | affective features |
| Daily aggregation | 9 | daily panel |
| Technical indicators | 10 | technical features |
| Merge + targets | 11 | merged table |
| Feature engineering + split | 12 | `08_features.parquet`, train/val/test |
| Models (trees) | 13 | LightGBM / XGBoost / CatBoost |
| **Leakage figure** | **13d** | **Figure 10** |
| Sequential model | 13b | BiGRU |
| Stacking / ensemble | 13c, 14 | ensemble + backtest |
| Causal / robustness | 15 | Pearson, Granger, SHAP, ablation, noise placebo |
| Real-time snapshot | 16 | live prediction figure |
| Figures | 17 | manuscript figures |

### Checkpoints

The pipeline caches every heavy step as a `.parquet` checkpoint (see Cell 2,
`ckpt`). If a checkpoint exists, its cell **skips recomputation and reloads it**.
This lets you reproduce downstream results without re-running the slow steps
(text collection 5, cleaning 6, FinBERT 7).

---

## 5. Reproducing Figure 10 (leakage demonstration)

Figure 10 shows that random (shuffled) validation inflates AUC by **0.285**
relative to chronological evaluation, for the same model and features.

1. Run **Cells 1–12** (or place the provided `08_features.parquet` checkpoint in
   the output directory so Cell 12 loads it directly).
2. Run **Cell 13d**.
3. Output: `fig5_learning_behavior.png` plus the printed numbers (random vs.
   chronological validation AUC and the leakage gap).

---

## 6. Repository structure

```
notebook.ipynb        Full pipeline (Cells 1–17)
requirements.txt      Python dependencies
README.md             This file
LICENSE               MIT (code)
figures/              Generated figures 
```

---

## 7. License

Code is released under the **MIT License** (see `LICENSE`). Data remain under the
licenses of their original providers (Section 1).

---

## 8. Citation

If you use this code, please cite the paper (Section above). BibTeX will be added
upon publication.

## 9. Contact

Abdelkhaleq EL HADDAD, abdelkhaleq_elhaddad@um5.ac.ma, Issues and questions: please open a GitHub issue.

