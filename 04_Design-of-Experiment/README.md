# Design of Experiment

This folder contains applied R-based examples for experimental design analysis, especially for agricultural research data. The content focuses on how to analyze treatment effects and block effects using proper statistical methods.

## Folder structure

```text
04_Design-of-Experiment/
├── README.md
├── 01_CRD_Analysis/
│   ├── 01_CRD_Analylsis_normal_data.qmd
│   ├── 02_CRD_Analysis_non-normal_data.qmd
│   ├── crd_normal_data.csv
│   └── crd_non_normal_data.csv
└── 02_RBD_Analysis/
    ├── 01_RBD_Analysis_normal_data.qmd
    ├── 02_RBD_Mixed_Model_missing_data.qmd
    ├── 03_RBD_Analysis_non_normal_data.qmd
    ├── rbd_normal_data.csv
    ├── rbd_nonnormal_data.csv
    └── rbd_mixed_model_missing_data.csv
```

## What is included

### 01_CRD_Analysis

- Completely Randomized Design (CRD)
- Normal data analysis using ANOVA
- Non-normal data analysis and alternative thinking
- CSV datasets for practice

### 02_RBD_Analysis

- Randomized Complete Block Design (RBD / RCBD)
- Normal data analysis with blocking
- Mixed model approach with missing data
- Non-normal data analysis
- CSV datasets used in the examples

## Main statistical ideas

- Checking assumptions before ANOVA
- Testing normality and variance homogeneity
- Interpreting treatment effects
- Performing post-hoc comparisons
- Handling block effects in designed experiments
- Using R to analyze agricultural field trial data

## How to use these files

1. Open the `.qmd` file for the design you want to study.
2. Read the explanation and run the code chunk by chunk in R or RStudio.
3. Use the associated `.csv` file for data input.
4. Compare the normal and non-normal analysis examples to understand model choice.

## Relation to the repo

This folder is a practical continuation of the statistics learning materials in `03_Statistic-Note`. It applies the theoretical ideas to real experimental data and is an important part of the repository's agricultural statistics workflow.

---

This folder is part of the `R-Language` learning repository.
