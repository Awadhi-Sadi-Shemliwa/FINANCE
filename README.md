# FINANCE — Credit Default Analysis

A portfolio project predicting next-month credit-card default using six months of customer repayment history from a Taiwanese bank dataset.

The analysis examines data-quality issues, compares predictive models, and illustrates how an intervention threshold can reflect business costs.

## Project files

- [Analysis notebook](finance_credit_default_analysis.ipynb)
- [Interactive walkthrough](finance_credit_default_animation.html)
- [Original project notes](finance_credit_default_README.md)

## Headline result

The project reports a ROC AUC of about 0.78 for a gradient-boosting model using repayment behavior. It illustrates a cost-based threshold under an explicitly assumed ratio of missed-default cost to contact cost.

## Data and scope

The dataset is from Yeh and Lien’s credit-card default study, distributed by the UCI Machine Learning Repository under CC BY 4.0. The data is historical and comes from one bank.

## Reproduction note

This starter repository contains the supplied notebook, HTML walkthrough, and project notes. Reproducing the analysis may also require the source dataset, data-download script, dependencies, and generated results and figures. The example cost ratio is an assumption, not a bank’s validated policy.
