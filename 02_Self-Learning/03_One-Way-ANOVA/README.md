# One-Way ANOVA & Post-Hoc Testing

**Focus:** Master single-factor experimental analysis with comprehensive statistical testing

---

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Understand ANOVA assumptions and diagnostic checks
- ✅ Execute one-way ANOVA and interpret results
- ✅ Perform post-hoc tests (Tukey, LSD, Duncan)
- ✅ Generate compact letter displays (CLD)
- ✅ Use non-parametric alternatives when assumptions violated

---

## 📚 What's Inside

### Files
- `One-Way-ANOVA.qmd` - Complete ANOVA workflow
- `Post_hoc.qmd` - Comprehensive post-hoc testing methods
- `fertilizer_yield_for_anova.csv` - Clean ANOVA dataset
- `agriculture_posthoc_data.csv` - Post-hoc examples
- `non_normal_yield_data.csv` - Data for non-parametric tests

---

## 📊 One-Way ANOVA Basics

### **What is ANOVA?**
ANOVA (Analysis of Variance) tests if means differ significantly across groups.

**Null Hypothesis:** All group means are equal
**Alternative:** At least one group mean differs

### **When to Use One-Way ANOVA**
- Single treatment/factor (e.g., fertilizer type)
- 3+ treatment levels
- Continuous response variable
- Independent observations

---

## 🔍 Assumption Checking

### **1. Normality (Shapiro-Wilk Test)**
```r
# Test overall residuals
shapiro.test(residuals(model))
# p > 0.05 → Normal ✓

# Test by group
data %>%
  group_by(Treatment) %>%
  summarise(p_value = shapiro.test(Yield)$p.value)
```

### **2. Homogeneity of Variance (Levene's Test)**
```r
library(car)

leveneTest(Yield ~ Treatment, data = data)
# p > 0.05 → Equal variances ✓
```

### **3. Independence**
- Observations independent by study design
- Durbin-Watson test for autocorrelation

### **Diagnostic Plots**
```r
model <- aov(Yield ~ Treatment, data = data)

par(mfrow = c(2, 2))
plot(model)
par(mfrow = c(1, 1))

# Interpret:
# 1. Residuals vs Fitted - check for patterns (should be random)
# 2. Q-Q Plot - check normality (should follow line)
# 3. Scale-Location - check homogeneity (spread should be constant)
# 4. Residuals vs Leverage - identify influential outliers
```

---

## 📈 Running One-Way ANOVA

### **Basic ANOVA**
```r
# Model specification
model <- aov(Yield ~ Treatment, data = data)

# Results
summary(model)

# Output interpretation:
# Df - degrees of freedom
# Sum Sq - sum of squares
# Mean Sq - mean square (Sum Sq / Df)
# F value - test statistic
# Pr(>F) - p-value
```

### **ANOVA with Blocks (RBD)**
```r
# Add block as factor
model <- aov(Yield ~ Treatment + Block, data = data)
summary(model)
```

### **Extracting Information**
```r
# Coefficients
coef(model)

# Predicted values
predicted(model)

# Residuals
residuals(model)

# R-squared (explained variation)
summary.lm(model)$r.squared
```

---

## 🔄 Post-Hoc Tests

If ANOVA p < 0.05, perform post-hoc tests to identify which pairs differ.

### **1. Tukey HSD (Tukey Honestly Significant Difference)**
Best for balanced designs with equal group sizes.

```r
library(agricolae)

result <- HSD.test(model, "Treatment", console = TRUE)

# Output:
# means - group means
# M - sorted means with letter groupings
# groups - compact letter display

# Save results
tukey_results <- result$groups
```

### **2. LSD (Least Significant Difference)**
More liberal than Tukey; use when sample sizes small.

```r
result <- LSD.test(model, "Treatment", console = TRUE)
```

### **3. Duncan Test**
Multiple range test; intermediate between LSD and Tukey.

```r
result <- duncan.test(model, "Treatment", console = TRUE)
```

### **4. emmeans (Estimated Marginal Means)**
Flexible approach for complex comparisons.

```r
library(emmeans)
library(multcompView)

# Pairwise comparisons
emm <- emmeans(model, ~ Treatment)
pairs(emm)

# Compact letter display
cld(emm)

# Custom contrasts
emm <- emmeans(model, ~ Treatment)
contrast(emm, "pairwise", adjust = "tukey")
```

---

## 🔤 Compact Letter Displays (CLD)

Letter groupings show which means differ significantly.

### **How to Read CLD:**
```
Treatment  Mean  Letter
A          45    a
B          58    ab
C          62    b
```

**Interpretation:**
- A has the lowest mean
- C has the highest mean
- B overlaps with both A and C
- A and C differ significantly (different letters)
- A and B don't differ significantly (shared 'a')
- B and C don't differ significantly (shared 'b')

### **Creating CLD**
```r
library(emmeans)
library(multcompView)

model <- aov(Yield ~ Treatment, data = data)
emm <- emmeans(model, ~ Treatment)

# Get compact letter display
cld(emm)
```

---

## 📊 Visualization with Letters

### **Add Letters to Bar Plot**
```r
library(ggplot2)
library(emmeans)
library(multcompView)

# Get summary with letters
model <- aov(Yield ~ Treatment, data = data)
emm <- emmeans(model, ~ Treatment)
cld_data <- as.data.frame(cld(emm))

# Plot
ggplot(cld_data, aes(x = Treatment, y = emmean, fill = Treatment)) +
  geom_col() +
  geom_errorbar(aes(ymin = emmean - SE, ymax = emmean + SE),
                width = 0.2) +
  geom_text(aes(label = .group, y = emmean + SE + 2), size = 5) +
  theme_classic() +
  labs(title = "Yield by Treatment (Letters indicate significance)",
       y = "Yield (kg/ha)", x = "Treatment")
```

---

## 🚫 When Assumptions Fail: Non-Parametric Tests

### **Kruskal-Wallis Test** (non-parametric alternative to ANOVA)
```r
# Use when normality assumption fails
kruskal.test(Yield ~ Treatment, data = data)
```

### **Dunn Test** (post-hoc for Kruskal-Wallis)
```r
library(FSA)

result <- dunnTest(Yield ~ Treatment, data = data, method = "bonferroni")
result
```

### **Friedman Test** (for repeated measures)
```r
friedman.test(Yield ~ Treatment | Block, data = data)
```

---

## 📋 Complete Workflow Example

### **Scenario:** Comparing 4 fertilizer types

```r
library(dplyr)
library(car)
library(agricolae)
library(ggplot2)

# 1. Load data
data <- read.csv("fertilizer_yield_for_anova.csv")

# 2. Descriptive statistics
data %>%
  group_by(Treatment) %>%
  summarise(
    Count = n(),
    Mean = mean(Yield),
    SD = sd(Yield),
    SE = SD / sqrt(Count),
    CV = (SD / Mean) * 100
  )

# 3. Check assumptions
shapiro.test(residuals(aov(Yield ~ Treatment, data = data)))
leveneTest(Yield ~ Treatment, data = data)

# 4. Run ANOVA
model <- aov(Yield ~ Treatment, data = data)
anova_summary <- summary(model)
print(anova_summary)

# 5. Post-hoc test
if (anova_summary[[1]]["Pr(>F)"][1,1] < 0.05) {
  result <- HSD.test(model, "Treatment", console = TRUE)
} else {
  print("No significant differences")
}

# 6. Visualize
ggplot(data, aes(x = Treatment, y = Yield, fill = Treatment)) +
  geom_boxplot(alpha = 0.7) +
  geom_jitter(width = 0.2, alpha = 0.3) +
  theme_classic() +
  labs(title = "Yield by Fertilizer Treatment")
```

---

## ✅ Reporting ANOVA Results

### **Academic Format:**
*"A one-way ANOVA revealed significant differences in yield across fertilizer treatments (F(3,20) = 8.45, p = 0.001). Post-hoc comparisons using Tukey's HSD test showed that treatment C (M = 62.3, SD = 4.2) produced significantly higher yields than treatment A (M = 45.1, SD = 3.8)."*

### **Table Format:**
```
Table 1. Yield by Fertilizer Treatment

Treatment    Mean (kg/ha)    SD      SE    Letter
A            45.1           3.8     1.3     a
B            58.2           5.4     1.9    ab
C            62.3           4.2     1.5     b
D            59.8           6.1     2.2    ab

F(3,20) = 8.45, p = 0.001
CV = 8.2%
```

---

## 🎓 Exercises

1. **Load & Explore** - Summary stats by treatment
2. **Check Assumptions** - Shapiro-Wilk and Levene tests
3. **Run ANOVA** - Interpret F-statistic and p-value
4. **Post-Hoc** - Apply Tukey test and generate CLD
5. **Visualize** - Create publication-ready plot with letters

---

## 📚 Resources

- [agricolae documentation](https://cran.r-project.org/web/packages/agricolae/)
- [emmeans documentation](https://cran.r-project.org/web/packages/emmeans/)
- [ANOVA assumptions](https://r-coder.com/assumptions-anova-r/)
- [Statistical Testing](https://www.scribbr.com/statistics/)

---

## Next Steps

1. Master all post-hoc test options
2. Move to **04_Two_Way_ANOVA/** for complex designs
3. Learn mixed models for hierarchical data
4. Apply to your own agricultural data

---

**Last Updated:** July 2, 2026
