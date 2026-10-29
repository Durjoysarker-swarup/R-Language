# CRD Analysis

This folder contains examples for analyzing a Completely Randomized Design (CRD) in R.

## What is included

- `01_CRD_Analylsis_normal_data.qmd` — CRD analysis for normally distributed data
- `02_CRD_Analysis_non-normal_data.qmd` — non-normal data analysis and alternative approach
- `crd_normal_data.csv` — sample dataset for normal-data CRD analysis
- `crd_non_normal_data.csv` — sample dataset for non-normal-data CRD analysis

## Main ideas

- One-way ANOVA for CRD
- Checking model assumptions
- Testing normality and variance homogeneity
- Interpreting treatment differences
- Post-hoc comparisons for mean separation
- Using non-parametric alternatives when assumptions fail

## Typical workflow

1. Load the data CSV file.
2. Fit the ANOVA model.
3. Check residual plots and assumption tests.
4. Interpret the treatment effect.
5. If needed, perform post-hoc tests to compare means.

## Relation to the repo

This folder is part of the experimental design section and applies the concepts introduced in the statistics notes to agricultural trial data.

---

This folder is part of the `R-Language` learning repository.
