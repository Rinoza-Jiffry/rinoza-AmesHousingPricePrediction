# OLS vs Ridge vs Lasso: A Practical Regularization Study on the Ames Housing Dataset

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3%2B-orange?logo=scikit-learn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.0%2B-150458?logo=pandas&logoColor=white)
![statsmodels](https://img.shields.io/badge/statsmodels-0.14%2B-4051b5)
![License](https://img.shields.io/badge/license-MIT-green)

---

## Overview

Most tutorials explain *what* Ridge and Lasso are. This project asks a more grounded question: **does regularization actually make a measurable difference on real data, and if so, when and why?**

Using the Ames Housing dataset — detailed records on 2,930 residential home sales in Ames, Iowa — this project runs all three regression approaches end-to-end and compares them not just on predictive performance, but on coefficient stability and model interpretability.

---

## What This Project Covers

- **Baseline OLS regression** — establishing a reference point before adding any regularization
- **Multicollinearity diagnostics** — using Variance Inflation Factor (VIF) to identify features that are redundant or linearly dependent
- **Ridge regression** — observing how L2 regularization shrinks coefficients and stabilizes the model under multicollinearity
- **Lasso regression** — exploring how L1 regularization performs automatic feature selection by zeroing out less informative features
- **Model comparison** — evaluating all three approaches on the same test set with consistent metrics

---

## Dataset

The **Ames Housing Dataset** is a well-known regression benchmark originally compiled by Dean De Cock. It covers 82 features per property including structural details, quality ratings, and sale conditions.

After preprocessing — keeping only numerical features, dropping columns with more than 30% missing values, and imputing remaining gaps with column medians — the analysis works with **38 features** across **2,930 samples**.

The dataset and notebook are included in this repository.

---

## Key Results

| Model | Test R² | RMSE ($) | Features Removed |
|---|---|---|---|
| OLS (baseline) | 0.8372 | 36,132 | 0 |
| Ridge (α = 100) | 0.8379 | 36,054 | 0 — shrinks all |
| Lasso (α = 5) | 0.8372 | 36,133 | 3 |

Ridge at α = 100 produced the best generalisation performance. Lasso at α = 5 matched OLS accuracy while removing three redundant features — `Bsmt Unf SF`, `Low Qual Fin SF`, and `Full Bath` — with no meaningful cost to predictive performance.

All three models performed similarly in raw metrics. The more significant difference lies in **coefficient stability** (Ridge) and **model simplicity** (Lasso).

---

## Main Findings

**Multicollinearity is real and measurable.** Several floor-area related features exhibited infinite VIF, indicating perfect linear dependencies within the dataset. Basement area features showed VIF values above 10,000. This is expected in housing data — total area is just the sum of its parts — but it makes OLS coefficient estimates unreliable.

**Ridge handles multicollinearity well.** By penalising large coefficients, Ridge redistributes influence more evenly across correlated features. The result is a more stable model with slightly better generalisation performance — not a dramatic improvement, but a consistent one.

**Lasso confirms which features are redundant.** At sufficient regularisation strength, Lasso zeroed out three features that were already captured by other variables. This kind of embedded feature selection is useful when model interpretability matters as much as raw accuracy.

**Regularisation adds discipline, not just performance.** The core lesson from this project is that improving a regression model isn't always about increasing complexity. Sometimes it's about constraining it — and Ridge and Lasso do exactly that.

---

## Repository Contents

```
ames-housing-regression/
│
├── AmesHousing.csv            # Dataset
├── regression_analysis.ipynb  # Full analysis notebook
└── README.md
```

---

## Requirements

- Python 3.10+
- pandas
- numpy
- scikit-learn
- statsmodels
- matplotlib *(for visualisations)*

Install dependencies with `pip install -r requirements.txt`

---

## Related

📝 Full write-up on LinkedIn: **

---

## License

This project is licensed under the MIT License.
