# RBD Analysis

This folder contains examples for analyzing a Randomized Complete Block Design (RBD / RCBD) in R.

## What is included

- `01_RBD_Analysis_normal_data.qmd` — RBD analysis for normal data
- `02_RBD_Mixed_Model_missing_data.qmd` — mixed model approach with missing data
- `03_RBD_Analysis_non_normal_data.qmd` — non-normal data analysis for RBD data
- `rbd_normal_data.csv` — dataset for standard RBD analysis
- `rbd_nonnormal_data.csv` — dataset for non-normal RBD analysis
- `rbd_mixed_model_missing_data.csv` — dataset for mixed-model and missing-data example

## Main ideas

- Randomized complete block design
- Blocking to reduce environmental variation
- ANOVA with treatment and block effects
- Assumption checking for residuals
- Post-hoc mean comparison
- Mixed model handling for missing or complex data
- Alternative analysis when data are non-normal

## Typical workflow

1. Load the relevant CSV dataset.
2. Convert factors (treatment, block) properly.
3. Fit the model with block and treatment effects.
4. Check assumptions using residual plots and tests.
5. Interpret the treatment effect and block effect.
6. Use post-hoc tests when needed.

## Relation to the repo

This folder is a practical continuation of the statistics and experimental design materials in the repository, focused on agricultural field-trial analysis.

---

This folder is part of the `R-Language` learning repository.
