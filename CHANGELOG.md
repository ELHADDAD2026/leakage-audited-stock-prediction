# Version notes

## v2 (this version)

This version corrects and harmonizes the reported ablation and placebo figures so
that the notebook, the figures, the saved artifacts, and the manuscript all agree.

Changes relative to the previous version:

- **Corrected the sentiment-ablation figure (fig4.png).** The earlier figure showed
  outdated values (+0.37% real / −1.02% placebo in 2022; −1.89% placebo in 2023). It
  now shows the definitive values computed with the exact ablation procedure of the
  causal-analysis cell on the frozen corpus: 2023 real +0.71% / placebo −1.31%;
  2022 real −0.63% / placebo −1.53%.

- **Updated the README** to state the definitive ablation values explicitly and to
  reaffirm that the saved `models/*.json` and `RESULTS.txt` files are the single
  source of truth.

- **Removed the venue name from the record title.** The title no longer names a
  specific journal, since the target venue may change during review.

- The correlation figures are reported as ≈ 0.196 (lag 0) and ≈ 0.030 (lag 1),
  matching `lag_correlations` in the saved artifacts.

The concept DOI (10.5281/zenodo.20945551) continues to resolve to this latest
version and is the DOI cited in the manuscript.
