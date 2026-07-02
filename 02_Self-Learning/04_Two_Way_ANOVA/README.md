# Two-Way ANOVA & Interactions

**Focus:** Understanding multi-factor experiments and interaction effects

---

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Understand main effects and interaction effects
- ✅ Conduct two-way ANOVA analysis
- ✅ Visualize and interpret interactions
- ✅ Design complex agricultural experiments
- ✅ Use mixed models for blocked designs

---

## 📚 What's Inside

### Files
- `Two_way_anova.qmd` - Complete two-way ANOVA tutorial
- `agriculture_two_way_anova.csv` - Fertilizer × Variety dataset

---

## 📊 Two-Way ANOVA Concepts

### **When to Use Two-Way ANOVA**
- Two treatment factors (e.g., Fertilizer × Variety)
- Want to test both factors AND their interaction
- Continuous response variable
- Balanced design (equal replicates per combination)

### **Model Structure**
```
Yield = Grand Mean + Fertilizer Effect + Variety Effect + Interaction + Error
```

### **Key Effects**
- **Main Effect:** Effect of one factor averaging across other factor
- **Interaction Effect:** Combined effect that's more than additive

---

## 🔍 Understanding Interactions

### **No Interaction (Parallel Lines)**
```
Fertilizer A works better than B at all varieties
        |
        |  B
        | /
   Yield|/  A
        |
        |____Variety
```

### **Interaction (Non-Parallel Lines)**
```
Fertilizer A better for Variety 1, but B better for Variety 2
        |
        |    A (for Var 2)
   Yield|   / \ 
        |  /   \
        | /      B (for Var 2)
        |____Variety
```

---

## 📈 Running Two-Way ANOVA

### **Basic Model**
```r
model <- aov(Yield ~ Fertilizer * Variety, data = data)
summary(model)

# Output includes:
# Fertilizer - main effect of fertilizer
# Variety - main effect of variety
# Fertilizer:Variety - interaction effect
```

### **With Blocks (RCBD)**
```r
# Randomized Complete Block Design
model <- aov(Yield ~ Fertilizer * Variety + Block, data = data)
summary(model)
```

### **Interpreting Output**
```
                 Df Sum Sq Mean Sq F value Pr(>F)
Fertilizer        2  450.2  225.1   8.50 0.002 **
Variety           1  280.5  280.5  10.60 0.001 **
Fertilizer:Variety 2   89.3   44.6   1.69 0.189
Residuals        42 1112.3   26.5
```

**Interpretation:**
- Fertilizer: Significant (p = 0.002)
- Variety: Significant (p = 0.001)
- Interaction: NOT significant (p = 0.189)
  → Effects of fertilizer don't depend on variety

---

## 📊 Visualizing Interactions

### **Interaction Plot (Line Plot)**
```r
library(ggplot2)

ggplot(data, aes(x = Fertilizer, y = Yield, 
                 color = Variety, group = Variety)) +
  geom_line(size = 1) +
  geom_point(size = 3) +
  theme_classic() +
  labs(title = "Interaction: Fertilizer × Variety",
       y = "Yield (kg/ha)", x = "Fertilizer")

# Parallel lines = no interaction
# Non-parallel/crossing = interaction present
```

### **Mean Comparison (Bar Plot)**
```r
library(dplyr)

summary <- data %>%
  group_by(Fertilizer, Variety) %>%
  summarise(mean_yield = mean(Yield),
            se = sd(Yield) / sqrt(n()),
            .groups = 'drop')

ggplot(summary, aes(x = Fertilizer, y = mean_yield, fill = Variety)) +
  geom_col(position = "dodge") +
  geom_errorbar(aes(ymin = mean_yield - se, ymax = mean_yield + se),
                width = 0.2, position = position_dodge(0.9)) +
  theme_classic() +
  labs(title = "Mean Yield by Fertilizer and Variety",
       y = "Yield (kg/ha)", x = "Fertilizer")
```

### **Heatmap (For Many Combinations)**
```r
ggplot(summary, aes(x = Fertilizer, y = Variety, fill = mean_yield)) +
  geom_tile() +
  geom_text(aes(label = round(mean_yield, 1)), color = "white", size = 4) +
  scale_fill_viridis_c() +
  theme_minimal() +
  labs(title = "Yield Across Treatment Combinations")
```

---

## 🔬 Experimental Designs

### **CRD (Completely Randomized Design)**
```r
library(agricolae)

# Design for 3 fertilizers × 2 varieties, 4 reps each
design <- design.crd(
  trt = paste(rep(c("F1", "F2", "F3"), 2),
              rep(c("V1", "V2"), each = 3), sep = "_"),
  r = 4,
  seed = 42
)

design$book  # Randomization layout
```

### **RCBD (Randomized Complete Block Design)**
```r
# Factorial RBD: Fertilizer × Variety in blocks
design <- design.rcbd(
  trt = c("F1_V1", "F1_V2", "F2_V1", "F2_V2", "F3_V1", "F3_V2"),
  r = 3,
  seed = 42
)
```

### **Factorial RBD**
```r
# More explicit
library(agricolae)

design <- design.factorial(
  trt = list(
    Fertilizer = c("F1", "F2", "F3"),
    Variety = c("V1", "V2")
  ),
  r = 3,
  seed = 42
)
```

---

## 🎯 Post-Hoc Analysis for Two-Way ANOVA

### **Main Effect Comparisons**
```r
library(emmeans)
library(multcompView)

model <- aov(Yield ~ Fertilizer * Variety, data = data)

# Compare fertilizers (averaging over variety)
emm_fert <- emmeans(model, ~ Fertilizer)
cld(emm_fert)  # Compact letter display

# Compare varieties (averaging over fertilizer)
emm_var <- emmeans(model, ~ Variety)
cld(emm_var)
```

### **Simple Effects (One Factor at Each Level of Other)**
```r
# Effect of fertilizer within each variety
emm_simple <- emmeans(model, ~ Fertilizer | Variety)
cld(emm_simple)  # Letters for each variety separately
```

### **Pairwise Comparisons**
```r
# All combinations
emm_all <- emmeans(model, ~ Fertilizer * Variety)
pairs(emm_all)  # Pairwise comparisons of all 6 combinations
```

---

## 🔄 Mixed Models for Complex Designs

When blocks/subjects are random effects:

```r
library(lme4)
library(lmerTest)

# Random blocks
model <- lmer(Yield ~ Fertilizer * Variety + (1|Block), data = data)
anova(model, type = 3)  # Get p-values

# Random blocks nested in region
model <- lmer(Yield ~ Fertilizer * Variety + (1|Region/Block), data = data)
```

---

## 📋 Complete Workflow

### **Research Question:** 
*Do fertilizer and variety independently affect yield, or is there an interaction?*

```r
library(dplyr)
library(ggplot2)
library(car)
library(emmeans)
library(multcompView)

# 1. Load and explore
data <- read.csv("agriculture_two_way_anova.csv")

summary_table <- data %>%
  group_by(Fertilizer, Variety) %>%
  summarise(Mean = mean(Yield),
            SD = sd(Yield),
            n = n(),
            .groups = 'drop')
print(summary_table)

# 2. Check assumptions
model_temp <- aov(Yield ~ Fertilizer * Variety, data = data)
shapiro.test(residuals(model_temp))
leveneTest(Yield ~ Fertilizer * Variety, data = data)

# 3. Run two-way ANOVA
model <- aov(Yield ~ Fertilizer * Variety, data = data)
summary(model)

# 4. Visualize interaction
ggplot(data, aes(x = Fertilizer, y = Yield, 
                 color = Variety, group = Variety)) +
  geom_line(stat = "summary", fun = mean, size = 1) +
  geom_point(stat = "summary", fun = mean, size = 3) +
  geom_jitter(width = 0.1, alpha = 0.3) +
  theme_classic() +
  labs(title = "Fertilizer × Variety Interaction",
       y = "Yield (kg/ha)", x = "Fertilizer")

# 5. Post-hoc tests
emm <- emmeans(model, ~ Fertilizer * Variety)
pairs(emm)  # All pairwise comparisons

# 6. Simple effects if interaction significant
if (summary(model)[[1]]["Pr(>F)"][3,1] < 0.05) {
  emm_simple <- emmeans(model, ~ Fertilizer | Variety)
  cld(emm_simple)
}
```

---

## ✅ Reporting Two-Way ANOVA

### **Typical Results Section:**
*"A two-way ANOVA revealed main effects of fertilizer (F(2,24) = 12.3, p < 0.001) and variety (F(1,24) = 8.7, p = 0.007), but no significant interaction (F(2,24) = 1.69, p = 0.189). Fertilizer F3 produced the highest yields across varieties, while Variety V1 outperformed V2 across fertilizer types."*

---

## 🎓 Exercises

1. Load two-way dataset and calculate summary statistics by treatment combination
2. Run ANOVA and interpret main effects and interaction
3. Create interaction plot (parallel vs non-parallel lines)
4. Perform post-hoc comparisons with compact letters
5. Design a factorial experiment using agricolae

---

## 📚 Advanced Topics

- **Split-Plot Designs:** 2+ levels of randomization
- **Strip-Plot Designs:** Factors applied in different patterns
- **Repeated Measures:** Same subjects measured over time
- **Bayesian Two-Way ANOVA:** Prior specifications

---

## 📚 Resources

- [emmeans documentation](https://cran.r-project.org/web/packages/emmeans/)
- [agricolae design generators](https://cran.r-project.org/web/packages/agricolae/)
- [lme4 mixed models](https://cran.r-project.org/web/packages/lme4/)
- [Two-way ANOVA guide](https://www.scribbr.com/statistics/two-way-anova/)

---

**Last Updated:** July 2, 2026
