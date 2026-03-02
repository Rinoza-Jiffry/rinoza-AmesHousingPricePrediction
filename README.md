# OLS vs Ridge vs Lasso: A Practical Regularization Study on the Ames Housing Dataset

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3%2B-orange?logo=scikit-learn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.0%2B-150458?logo=pandas&logoColor=white)
![statsmodels](https://img.shields.io/badge/statsmodels-0.14%2B-4051b5)

---

## Overview

Most tutorials explain *what* Ridge and Lasso are. This project asks a more grounded question: **does regularization actually make a measurable difference on real data, and if so, when and why?**

Using the Ames Housing dataset — detailed records on 2,930 residential home sales in Ames, Iowa — this project runs OLS, Ridge and Lasso end-to-end and compares them not just on predictive performance, but on coefficient stability and model interpretability.

---

## What This Project Covers

- **Baseline OLS regression** — establish a reference point before regularization
- **Multicollinearity diagnostics** — Variance Inflation Factor (VIF) to identify redundant or linearly dependent features
- **Ridge regression** — observe how L2 regularization shrinks coefficients and stabilizes the model under multicollinearity
- **Lasso regression** — explore how L1 regularization performs automatic feature selection by zeroing out less informative features
- **Model comparison** — evaluate all three approaches on the same test set with consistent metrics

---

## Dataset

The **Ames Housing Dataset** covers 82 features per property including structural details, quality ratings, and sale conditions.

After preprocessing — keeping only numerical features, dropping columns with more than 30% missing values, and imputing remaining gaps with column medians — the analysis uses **38 features** across **2,930 samples**.

The dataset and notebook are included in this repository.

---

## Key Results

| Model | Test R² | RMSE ($) | Features Removed |
|---|---:|---:|---:|
| OLS (baseline) | 0.8372 | 36,132 | 0 |
| Ridge (α = 100) | 0.8379 | 36,054 | 0 — coefficients shrunk |
| Lasso (α = 5) | 0.8372 | 36,133 | 3 |

Ridge at α = 100 produced the best generalization in our scan. Lasso at α = 5 matched OLS accuracy while removing three redundant features (see the notebook cell that prints dropped features for the exact names).

All three models performed similarly on raw metrics. The larger differences are in **coefficient stability** (Ridge) and **model simplicity** (Lasso).

---

## Main Findings

**Multicollinearity is real and measurable.** Several floor-area related features showed infinite VIF values, indicating near‑perfect linear dependencies (e.g., gross living area vs. floor area components). Basement area features showed extremely large VIF values as well. This is expected: total area is effectively the sum of component areas.

**Ridge handles multicollinearity well.** By penalizing large coefficients, Ridge distributes influence more evenly across correlated features. The result is a more stable model with slightly better generalization performance.

**Lasso confirms redundant features.** At sufficient regularisation strength, Lasso zeroed out a few features that were already captured by other variables. This embedded feature selection is helpful when interpretability matters.

**Regularisation adds discipline, not just performance.** The lesson: constraining a model can be more valuable than making it more complex.

---

## Repository Contents

```
Multiple Regression Demonstration/
│
├── AmesHousing.csv            # Dataset
├── HousePricePrediction.ipynb # Full analysis notebook
└── README.md
```

---

## Requirements

- Python 3.10+
- pandas
- numpy
- scikit-learn
- statsmodels
- matplotlib *(optional — used only for visualisations/diagnostics if you run plotting cells)*

Install dependencies with:

```bash
pip install -r requirements.txt
```

---

## Reproducibility & Next Steps

- To choose an optimal `alpha` for production, run `LassoCV` or `GridSearchCV` over a wide range of alphas and select the value that minimizes cross‑validated error.
- Consider removing or combining perfectly redundant features (e.g., specific floor-area breakdowns) when building a final, interpretable model.
- For model documentation, paste the output of the notebook cell that lists dropped features (the README currently refers to that cell rather than hard‑coding column names).

---

## Blog

Find the detail Explanation on my LinkedIn : https://www.linkedin.com/pulse/ols-vs-ridge-lasso-practical-regularization-study-ames-rinoza-jiffry-xba0c
