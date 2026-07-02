---
title: "the plan"
output: html_document
---

# R Language Learning - Progress Summary

Consolidated notes across Weeks 1-4. Covers everything already practiced (basics, stats, ANOVA experimental designs, regression, AgroR package).

## Week 1: R Fundamentals

### Setup & Basics
* `getwd()` / `setwd("path") / `list.files()` - manage working directory
* **Conditional:** `if (a > b) { ... } else if (a == b) { ... } else { ... }`
* **Loop:** `for (x in 1:10) { print(x) }`
* **Custom function:** `function(x, y, z) { ... return/print(result) }`

### Data Types & Vectors
* `typeof()` → double, character, logical, integer (`10L`), complex (`5i`)
* Vectors with `c()`; `length()`; indexing `v[c(1,3)]`
* Sequences: `1:100`, `seq(1, 99, by=2)`, `seq(100, 1, -1)`
* Subsetting/logical filter: `v[10:20]`, `v[v > 20]`, boolean masks
* Type conversion: `as.integer()`, `as.character()`, `as.logical()`

### Data Frames & Matrices
* `data.frame(col1, col2, ...)`; `plot(df)`; `plot(y ~ x, df)`
* Add column: `df$new <- expression` (e.g., `BMI = weight / (height * 0.01)^2`)
* Categorize with nested `ifelse()` (e.g., BMI health level)
* `matrix(vals, nrow, ncol, byrow=TRUE)`; `is.data.frame()`; `length()`
* `rep()` to build repeated-group data frames

### Reading, Filtering & Exploring Data
* `read.csv("file")`; `head()`; `tail()`; `summary()`; `names()`; `nrow()`; `ncol()`
* `df[df$col == value, ]` - row filtering
* Grading with nested `ifelse()` on a Marks column

### Descriptive Statistics
* `mean()`, `median()`, `var()`, `sd()` - use `na.rm=TRUE` for missing data
* Custom `getmode()` function via `table()` / `which.max()`
* `quantile(x, probs=c(0.25, 0.5, 0.75))` for quartiles

### Missing Data
* `is.na()`, `sum(is.na())`, `na.omit()`, fill NA with column mean
* **VIM package:** `aggr()` to visualize missingness
* **mice package:** `mice()` + `complete()` to impute missing values

### Base R & ggplot2 Plotting
* `plot(v, type="p"/"l"/"o")` points/line/both; add title/labels/col
* `lines()` to overlay multiple series on one plot
* `barplot()` with matrix data, months/colors, plus `legend()`
* **ggplot2:** `geom_line`, `geom_point`, `geom_violin`, `geom_boxplot`, `geom_jitter`, `labs()`, `theme_classic()`

### Hypothesis Testing & Data Wrangling
* `t.test(y ~ group, data=df)` - two-sample t-test
* `aov(Score ~ Method, data=df) + summary()`
* One-way ANOVA; $p < 0.05 
ightarrow$ reject $H_0$
* **dplyr Data Wrangling:** Pipe `%>%` chains: `filter()`, `group_by()`, `summarise()`, `mutate()`, `arrange(desc())`
* `select()`, `rename()`, `distinct()`, `case_when()` (cleaner alternative to nested `ifelse`)
* `write.csv(df, "name.csv", row.names=FALSE)` to export

### ggplot2 - Applied
* `geom_bar(stat="summary")` for aggregated bar charts; `facet_wrap(~Region)`
* `position="dodge"` for grouped bars vs `facet_wrap` for separated panels
* Time series: `as.Date()`, `geom_line(aes(colour=Region))`
* Multi-variable plots combining color + `facet_wrap`

---

## Week 2: ANOVA & Experimental Designs

### One-Way/Two-Way ANOVA
* `model <- aov(Yield ~ Treatment, data=df); summary(model)` → check p-value
* Two-way: `aov(Yield ~ FactorA * FactorB, data=df)` - main effects + interaction
* `interaction.plot(FactorA, FactorB, Yield)` to visualize interaction

### Assumption Checks
* **Normality:** `shapiro.test(residuals(model))` - $p > 0.05 =$ normal
* **Homogeneity:** `leveneTest(y ~ group, data=df)` (car package) - $p > 0.05 =$ equal variances
* Diagnostic plots: `plot(model)` → Residuals vs Fitted, Q-Q, Scale-Location, Residuals vs Leverage

### Post-Hoc Tests (after significant ANOVA)
* `LSD.test()` / `HSD.test()` / `duncan.test()` - agricolae package
* `emmeans(model, pairwise ~ factor, adjust="none"/"tukey")`
* `cld()` with multcomp/multcompView adds compact letter groupings
* **Non-parametric:** `kruskal.test()` then `dunnTest()` (FSA, bonferroni)
* With blocks + non-normal: `friedman.test(y ~ treatment | block)`

### Experimental Design Theory
* Core principles: Replication, Randomization, Local control
* **CRD (Completely Randomized):** no blocking, lab/greenhouse only
* **RBD/RCBD:** single factor with blocks; `model: aov(y ~ treatment + block)`
* **Factorial RBD (FatRBD):** 2+ factors with interaction study
* Split-Plot (main plot + sub plot), Split-Split-Plot (3 factors), Strip-Plot designs
* agricolae design generators: `design.crd()`, `design.rcbd()`, `design.split()`

### Mixed Models (random effects, e.g., blocks)
* `lme4::lmer(y ~ treatment + (1|block)) + lmerTest` for p-values
* `anova(model, type=3)` for ANOVA-style output
* Split-plot: `lmer(y ~ A * B + (1|block/irrigation))`

---

## Week 3: Regression & Model Diagnostics

### Linear Regression
* `lm(y ~ x1 + x2, data=df); summary()` → coefficients, p-values, $R^2$, Adj $R^2$, F-stat
* $R^2 = SSR / SST$ (explained/total variation)
* Adjusted $R^2$ penalizes extra variables
* `geom_smooth(method="lm")` to visualize fitted trend + confidence band

### Correlation & Multicollinearity
* `cor(df)` / `cor(df[, c("a", "b")])` - correlation matrix
* `psych::pairs.panels()` - combined histogram/correlation/scatter matrix
* `car::vif(model)` - Variance Inflation Factor; VIF > 5-10 = problematic
* Fixes: remove a variable, combine variables, or PCA (`prcomp`) on scaled predictors

### Ridge Regression (glmnet)
* Adds L2 penalty $\lambda \sum  eta^2$ to shrink coefficients; handles multicollinearity/overfitting
* `cv.glmnet(x, y, alpha=0)` finds best $\lambda$ via cross-validation; `alpha=1` = Lasso
* `predict(model, s=best_lambda, newx=matrix)` for predictions

### Regression Assumptions & Diagnostics
* Independence, Linearity, Normality, Constant variance (homoscedasticity), no influential outliers
* `par(mfrow=c(2,2)); plot(model)` - 4-panel diagnostic plots
* `car::qqPlot(model)` and `car::ncvTest(model)` ($p > 0.05 =$ homoscedastic)

### Model Selection & Accuracy
* `AIC()` / `BIC()` to compare models (lower is better; BIC penalizes complexity more)
* `step(full_model, direction="both")` - automatic stepwise selection
* $RMSE = \sqrt{	ext{mean}((	ext{actual} - 	ext{predicted})^2)}$ - lower = better prediction accuracy
* Relative RMSE (%): <10% good, 10-20% moderate, >20% poor

---

## Week 4: AgroR Package (Agricultural Statistics)

### Package & Data Access
* `install.packages("AgroR"); library(AgroR); data(package="AgroR")` to list datasets

### Key Functions

| Function | Purpose | Design |
| :--- | :--- | :--- |
| `CRD()` | ANOVA + plot, single treatment | Completely Randomized |
| `DIC()` | ANOVA + plot, single treatment | CRD (Portuguese naming) |
| `DBC()` | ANOVA + plot with blocks | Randomized Block (RBD) |
| `FAT2DIC()` | Two-factor factorial ANOVA | Factorial CRD |
| `pol()` | Polynomial regression | Dose-response |
| `mcomp()` | Mean comparison (Tukey/LSD) | All designs |

### Usage Example & Key Argument
* `with(data, DIC(trat, resp, addmean=TRUE, ylab="resp", fill="trat", quali=TRUE))`
* `quali=TRUE` → treatment is categorical (names/types, e.g., A/B/C)
* `quali=FALSE` → treatment is numeric (doses/levels) - for trend/regression fitting

### Output Interpretation
* Auto-runs Shapiro-Wilk (normality), Bartlett (variance equality), Durbin-Watson (independence)
* Reports CV%, mean response, ANOVA table, and Tukey grouping letters directly on the bar chart

---

### Notes & Next Steps
* Sections above reflect material already practiced and understood (previously highlighted).
* Two-factor/Split-Plot post-hoc letter output via `lmer()`, and AgroR's `FAT2DIC()` / `DBC()` with blocks still need hands-on implementation and further practice.