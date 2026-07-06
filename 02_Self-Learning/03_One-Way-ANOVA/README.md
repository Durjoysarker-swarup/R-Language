# One-Way ANOVA & Post-Hoc Testing

Master single-factor experimental analysis with comprehensive statistical testing. This module covers the complete workflow from study design through result interpretation and reporting.

---

## 🎯 Learning Objectives

By the end of this module, you will:
- Understand ANOVA assumptions and diagnostic procedures
- Execute and interpret one-way ANOVA
- Perform post-hoc tests (Tukey, LSD, Duncan, emmeans)
- Generate compact letter displays for comparisons
- Use non-parametric alternatives appropriately
- Report results in academic format

---

## 📚 What's Inside

### Files
- `One-Way-ANOVA.qmd` - Complete ANOVA workflow tutorial
- `Post_hoc.qmd` - Comprehensive post-hoc testing methods
- `fertilizer_yield_for_anova.csv` - Clean ANOVA dataset
- `agriculture_posthoc_data.csv` - Post-hoc comparison examples
- `non_normal_yield_data.csv` - Data for non-parametric tests

---

## 📖 Core Concepts

### **What is One-Way ANOVA?**
Analysis of Variance tests whether means differ significantly across three or more treatment groups. It answers the question: "Do treatments produce different average responses?"

**Null Hypothesis:** All group means are equal  
**Alternative Hypothesis:** At least one group mean differs from others

### **When to Use**
- Single treatment factor with 3+ levels
- Continuous response variable
- Independent observations
- Balanced or nearly-balanced designs

---

## 🔍 Assumption Checking

### **1. Normality**
Test if residuals follow a normal distribution. Procedures like Shapiro-Wilk test assess this.

**What it means:** Deviations from mean should be symmetrically distributed.  
**When violated:** Consider non-parametric alternatives (Kruskal-Wallis test).

### **2. Homogeneity of Variance**
Test whether groups have equal variability. Levene's test is standard for this.

**What it means:** Spread around group means should be similar across all groups.  


### **3. Independence**
Ensure observations are independent (not repeated measures or spatial clusters).

**What it means:** Each observation should be independent of others.  
**Ensured by:** Proper experimental design and randomization.

### **Diagnostic Plots**
Visual inspection of residuals reveals:
- Whether spread is constant across fitted values (homogeneity)
- Whether points follow normal distribution (Q-Q plot)
- Which observations are influential outliers
- Overall model fit quality

---

## 📊 ANOVA Output Interpretation

**F-statistic:** Ratio of treatment variance to error variance. Larger F indicates stronger evidence of differences.

**p-value:** Probability of observing these results if null hypothesis (no differences) were true. p < 0.05 typically indicates significant differences.

**Coefficient of Variation (CV):** Standardized measure of experimental precision. Lower CV% indicates better experimental control.

**R-squared:** Proportion of total variation explained by treatments.

---

## 🔄 Post-Hoc Testing

When ANOVA indicates significant differences (p < 0.05), post-hoc tests identify which specific group pairs differ.

### **Tukey HSD (Honestly Significant Difference)**
Conservative test controlling family-wise error rate. Best for balanced designs and equal sample sizes.

### **LSD (Least Significant Difference)**
More liberal than Tukey. Use when making few comparisons or sample sizes are small.

### **Duncan Test**
Multiple range test with intermediate stringency between LSD and Tukey.

### **Emmeans Approach**
Flexible method allowing custom contrasts, adjustments, and visualization with statistical inference.

---

## 📋 Compact Letter Displays (CLD)

Letter groupings show which means differ significantly:
- Same letter = not significantly different
- Different letter = significantly different
- Overlapping letters = intermediate relationships

This visual format is standard in agricultural research publications.

---

## 📈 Non-Parametric Alternatives

When assumptions are violated:

**Kruskal-Wallis Test** - Non-parametric alternative to ANOVA when normality fails

**Dunn Test** - Post-hoc test following Kruskal-Wallis

These tests don't assume normal distributions but are less powerful if normality holds.

---

## 📊 Complete Workflow Steps

1. **Descriptive Statistics** - Summarize each group
2. **Check Assumptions** - Normality and homogeneity tests
3. **Run ANOVA** - Test for overall differences
4. **Interpret Results** - Is p-value significant?
5. **Post-Hoc Testing** - If significant, identify specific differences
6. **Visualization** - Create plots with letters
7. **Report Results** - Write in academic format

---

## 📝 Academic Reporting

Results should include:
- ANOVA test statistics (F-value, degrees of freedom, p-value)
- Mean values for each treatment
- Standard deviations or standard errors
- Post-hoc test method and results with letters
- Coefficient of variation
- Overall conclusion about treatment differences

Example: *"A one-way ANOVA revealed significant differences in yield across fertilizer treatments (F(3,20) = 8.45, p = 0.001), with treatment C producing significantly higher yields than treatment A by Tukey's HSD test."*

---

## 📚 Datasets Included

**fertilizer_yield_for_anova.csv**
Clean dataset with fertilizer treatments and yield responses. Suitable for basic ANOVA introduction.

**agriculture_posthoc_data.csv**
Example data demonstrating post-hoc testing scenarios.

**non_normal_yield_data.csv**
Data violating normality assumptions for non-parametric testing practice.

---

## 🎓 Learning Path

### Understanding ANOVA
- Conceptual basis of variance partitioning
- F-statistic as signal-to-noise ratio
- p-value interpretation
- Why post-hoc testing is necessary

### Executing Analysis
- Running ANOVA in R
- Extracting results and coefficients
- Checking diagnostic assumptions
- Performing post-hoc tests

### Interpretation & Reporting
- Making biological sense of results
- Academic format reporting
- Visualization with statistical annotations
- Communicating to different audiences

---

## 💡 Best Practices

**Always check assumptions first** - Protects validity of conclusions

**Don't rely on p-values alone** - Report effect sizes and confidence intervals

**Use appropriate post-hoc test** - Different tests for different situations

**Visualize results** - Plots communicate better than tables

---


## 🎯 Exercises

See `One-Way-ANOVA.qmd` and `Post_hoc.qmd` for hands-on practice with included datasets.

---

## Next Steps

After mastering one-way ANOVA:
1. Move to `04_Two_Way_ANOVA/` for multi-factor designs
2. Learn about interaction effects in experiments
3. Apply to your own research data

---

**Last Updated:** July 6, 2026

---

> **Remember:** Statistical tests answer "what" but not "why". Understanding biological context is essential for meaningful research conclusions.
