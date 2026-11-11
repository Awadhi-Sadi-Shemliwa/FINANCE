# Which credit-card customers will default next month?

30,000 customers of a Taiwanese bank in 2005, six months of repayment history each, and a model that decides whom the collections team should contact.

**Business question.** With limited capacity to intervene, which customers should be contacted before they default, and at what probability threshold?

**Answer in one paragraph.** A gradient-boosting model using repayment behaviour only ranks customers with a ROC AUC of 0.78 (KS 0.42) on 6,000 held-out customers; adding sex, education, marital status and age adds 0.002. If a missed default costs five times an unnecessary contact, the best threshold is 0.17, not the habitual 0.5: it catches 971 of 1,327 defaulters and cuts total cost by 25% against 0.5 and by half against doing nothing.

![Threshold and cost](figures/fig6_threshold_cost.png)

## What is in this repository

| Path | Contents |
|---|---|
| `src/get_data.py` | Downloads the original UCI spreadsheet into `data/` |
| `src/analysis.py` | The whole analysis with `# %%` cells |
| `analysis.ipynb` | The same analysis as an executed notebook |
| `figures/`, `results/metrics.json` | Figures and every number quoted in the paper |
| `paper/paper.md` | Write-up in research-paper format with references |
| `animation.html` | Step-through explanation of the project, with a live threshold slider |

## Run it

```bash
pip install -r requirements.txt
python src/get_data.py
python src/analysis.py
```

## Data and credit

Yeh, I.-C. (2016). *Default of credit card clients*. UCI Machine Learning Repository, CC BY 4.0. https://doi.org/10.24432/C55S3H

## Method in brief

1. **Clean**: the file has no empty cells, but 399 undocumented category codes and two undocumented repayment states used by 58% of rows. A two-row header makes every column text unless read with `header=1`. Thirty-five apparent duplicates are different customers and are kept.
2. **Explore**: default rate by latest repayment status and by credit limit; skewed amounts turned into ratios.
3. **Split**: stratified 80/20 (one snapshot in time, so no time split is possible; stated as a limitation).
4. **Model**: baseline, one-rule benchmark, logistic regression, gradient boosting; behaviour-only by design, protected characteristics tested separately.
5. **Evaluate**: cross-validated and test ROC AUC, KS, Brier, calibration.
6. **Decide**: expected cost at every threshold for a stated cost ratio.
