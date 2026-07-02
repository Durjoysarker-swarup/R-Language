# Week 2-4: Advanced Agricultural Statistics & Experimental Design

This folder contains specialized training in data wrangling, advanced visualization, and experimental design methodology for agricultural research. Organized into focused modules, each with practical code examples and real agricultural datasets.

---

## 📚 Folder Structure

```
02_Self-Learning/
├── README.md (this file)
├── Agricultural_Experimental_Design.pdf     # Theoretical reference
├── 01_Data-Wrangling/                       # Week 2.1: dplyr & Data Manipulation
├── 02_ggplot/                               # Week 2.2: Advanced Visualization
├── 03_One-Way-ANOVA/                        # Week 3: One-Way ANOVA & Post-Hoc
└── 04_Two_Way_ANOVA/                        # Week 4: Two-Way ANOVA & Interactions
```

---

## 🎯 Learning Pathway

### **Week 2: Data Wrangling & Visualization**
Master the art of data transformation and creating publication-quality visualizations.

**Skills:**
- ✅ dplyr pipelines for data manipulation
- ✅ Advanced ggplot2 techniques
- ✅ Time series visualization
- ✅ Grouped comparisons and faceting

### **Week 3: One-Way ANOVA & Post-Hoc Analysis**
Deep dive into single-factor experiments with comprehensive statistical testing.

**Skills:**
- ✅ One-way ANOVA design and execution
- ✅ Assumption checking (normality, homogeneity)
- ✅ Multiple comparison procedures
- ✅ Compact letter displays (CLD)
- ✅ Non-parametric alternatives

### **Week 4: Two-Way ANOVA & Experimental Design**
Understanding interactions and complex experimental designs in agriculture.

**Skills:**
- ✅ Two-way ANOVA with interactions
- ✅ Design generators (CRD, RCBD, Factorial)
- ✅ Mixed models with random effects
- ✅ AgroR package for agricultural statistics

---

## 🗂️ Module Breakdown

### **01_Data-Wrangling/** 
**Focus:** Master dplyr for reproducible data transformation

📖 **What You'll Learn:**
- Pipe operators (`%>%`)
- Core verbs: `filter()`, `select()`, `mutate()`, `group_by()`, `summarise()`
- Advanced: `case_when()`, `across()`, `nest()` / `unnest()`
- Creating summary tables for reports

**Files:**
- `Wrangling_dplyr.qmd` - Hands-on dplyr examples with fertilizer data
- `fertilizer_yield_data.csv` - Multi-treatment fertilizer dataset
- `Summary table.csv` - Output example

**Key Code Pattern:**
```r
library(dplyr)

data %>%
  filter(Yield > 50) %>%
  group_by(Treatment, Region) %>%
  summarise(
    mean_yield = mean(Yield, na.rm = TRUE),
    sd_yield = sd(Yield, na.rm = TRUE),
    n = n(),
    se = sd_yield / sqrt(n),
    .groups = 'drop'
  ) %>%
  arrange(desc(mean_yield))
```

**Why This Matters:**
- Professional data reporting in research
- Reproducible workflows
- Easy to audit and modify
- Foundation for advanced analysis

---

### **02_ggplot/** 
**Focus:** Create publication-quality visualizations

📖 **What You'll Learn:**
- Grammar of graphics principles
- Layering and customization
- Statistical summaries within plots
- Time series and multi-variable visualizations
- Theme design and color palettes

**Files:**
- `Visualization.qmd` - Advanced ggplot2 techniques
- `agriculture_sample_dataset.csv` - Multi-variable agricultural data
- `time_series_agriculture.csv` - Temporal crop data

**Key Techniques:**

```r
library(ggplot2)

# 1. Faceted plots for comparison
ggplot(data, aes(x = Date, y = Yield, color = Treatment)) +
  geom_line(size = 1) +
  geom_point(size = 2) +
  facet_wrap(~Region, scales = "free") +
  theme_classic() +
  theme(axis.text.x = element_text(angle = 45))

# 2. Statistical summaries
ggplot(data, aes(x = Treatment, y = Yield, fill = Treatment)) +
  geom_boxplot(alpha = 0.7) +
  geom_jitter(width = 0.2, alpha = 0.5) +
  stat_summary(fun = mean, geom = "point", size = 3, color = "red") +
  facet_wrap(~Block)

# 3. Time series with smoothing
ggplot(data, aes(x = DayAfterPlanting, y = PlantHeight)) +
  geom_point() +
  geom_smooth(method = "loess", se = TRUE) +
  facet_wrap(~Variety)
```

**Why This Matters:**
- Visual communication is crucial for research
- Professional plots improve manuscript acceptance
- Exploratory visualization guides analysis
- Reproducible graphics for presentations

---

### **03_One-Way-ANOVA/** 
**Focus:** Master single-factor experimental analysis

📖 **What You'll Learn:**
- ANOVA assumptions and diagnostics
- Parametric post-hoc tests (Tukey, LSD, Duncan)
- Non-parametric alternatives (Kruskal-Wallis, Dunn)
- Compact letter displays (CLD)
- Interpreting results and reporting

**Files:**
- `One-Way-ANOVA.qmd` - Complete ANOVA workflow with fertilizer trials
- `Post_hoc.qmd` - Comprehensive post-hoc testing methods
- `fertilizer_yield_for_anova.csv` - Clean ANOVA dataset
- `agriculture_posthoc_data.csv` - Example post-hoc data
- `non_normal_yield_data.csv` - Data requiring non-parametric tests

**Complete Workflow:**

```r
# 1. Load and explore
data <- read.csv("fertilizer_yield_for_anova.csv")
str(data)
summary(data)

# 2. Check assumptions
library(car)

# Normality test
shapiro.test(data$Yield)  # p > 0.05 = normal

# Homogeneity of variance
leveneTest(Yield ~ Treatment, data = data)  # p > 0.05 = equal variances

# 3. Run ANOVA
model <- aov(Yield ~ Treatment, data = data)
summary(model)  # Check p-value

# 4. Post-hoc if p < 0.05
library(agricolae)

# Tukey test
result <- HSD.test(model, "Treatment", console = TRUE)

# Or using emmeans for letter grouping
library(emmeans)
library(multcompView)

emm <- emmeans(model, ~ Treatment)
pairs(emm)
cld(emm)  # Compact letter display
```

**Key Interpretation Points:**
- **F-statistic:** Ratio of treatment to error variance
- **p-value < 0.05:** Treatments significantly different
- **CV%:** Coefficient of variation (< 20% good)
- **Letters:** Same letters = not significantly different

---

### **04_Two_Way_ANOVA/** 
**Focus:** Understanding interactions in multi-factor experiments

📖 **What You'll Learn:**
- Two-way ANOVA main effects
- Interaction effects interpretation
- Visualization of interactions
- Experimental design principles (CRD, RCBD, Factorial)
- Mixed models with random effects

**Files:**
- `Two_way_anova.qmd` - Complete two-way ANOVA analysis
- `agriculture_two_way_anova.csv` - Fertilizer × Variety dataset

**Two-Way ANOVA Model:**

```r
# Scenario: Fertilizer (3 levels) × Variety (2 levels)
data <- read.csv("agriculture_two_way_anova.csv")

# Model with interaction
model <- aov(Yield ~ Fertilizer * Variety, data = data)
summary(model)

# Interpretation:
# - Fertilizer p-value: Main effect of fertilizer
# - Variety p-value: Main effect of variety
# - Fertilizer:Variety p-value: Interaction effect

# If interaction significant, effects depend on each other!
```

**Interaction Visualization:**

```r
library(ggplot2)

# Interaction plot
ggplot(data, aes(x = Fertilizer, y = Yield, color = Variety, group = Variety)) +
  geom_line(size = 1) +
  geom_point(size = 3) +
  theme_classic() +
  labs(title = "Interaction: Fertilizer × Variety",
       y = "Yield (kg/ha)", x = "Fertilizer Type")

# Parallel lines = no interaction
# Non-parallel lines = interaction present
```

**Experimental Design Context:**

```
CRD (Completely Randomized Design):
  - No blocks, random assignment only
  - Best for uniform environments (lab, greenhouse)
  - Model: aov(Y ~ Treatment)

RCBD (Randomized Complete Block Design):
  - Blocking to account for environmental variation
  - Each block contains all treatments
  - Model: aov(Y ~ Treatment + Block)

Factorial (CRD or RCBD):
  - Multiple factors tested simultaneously
  - Allows testing interactions
  - Model: aov(Y ~ Factor1 * Factor2) or aov(Y ~ Factor1 * Factor2 + Block)
```

---

## 📊 Integrated Example: Complete Analysis Pipeline

Here's how all pieces fit together for a real agricultural study:

### **Research Question:** 
*How do different fertilizer types and crop varieties affect yield?*

### **Step 1: Experimental Design** (Week 4)
```r
library(agricolae)

# Generate RCBD layout
design <- design.rcbd(
  trt = c("FertA", "FertB", "FertC"),
  r = 3,  # 3 blocks
  seed = 42
)

# Generates randomization for field layout
```

### **Step 2: Data Entry & Wrangling** (Week 2.1)
```r
library(dplyr)

# Load raw data
raw_data <- read.csv("field_observations.csv")

# Clean and summarize
clean_data <- raw_data %>%
  filter(!is.na(Yield)) %>%
  mutate(
    TreatmentGroup = case_when(
      Fertilizer == "A" ~ "Organic",
      Fertilizer == "B" ~ "Inorganic",
      Fertilizer == "C" ~ "Mixed"
    )
  ) %>%
  group_by(Block, Treatment, Variety) %>%
  summarise(
    mean_yield = mean(Yield),
    sd_yield = sd(Yield),
    n = n(),
    .groups = 'drop'
  )
```

### **Step 3: Visualization** (Week 2.2)
```r
library(ggplot2)

ggplot(clean_data, aes(x = Treatment, y = mean_yield, fill = Variety)) +
  geom_col(position = "dodge") +
  geom_errorbar(aes(ymin = mean_yield - sd_yield, 
                    ymax = mean_yield + sd_yield),
                width = 0.2, position = position_dodge(0.9)) +
  facet_wrap(~Block) +
  theme_classic() +
  labs(title = "Yield by Fertilizer and Variety",
       y = "Yield (kg/ha)", x = "Fertilizer Type")
```

### **Step 4: Statistical Analysis** (Week 3-4)
```r
# Check assumptions
library(car)
shapiro.test(clean_data$mean_yield)
leveneTest(mean_yield ~ Treatment, data = clean_data)

# Two-way ANOVA
model <- aov(mean_yield ~ Treatment * Variety + Block, data = clean_data)
summary(model)

# Post-hoc if significant
library(emmeans)
library(multcompView)

emm <- emmeans(model, ~ Treatment | Variety)
cld(emm)  # Compare treatments within each variety
```

### **Step 5: Reporting**
All visualizations and results are reproducible, publication-ready!

---

## 🔧 Package Requirements

Install all necessary packages at once:

```r
# Install from CRAN
packages <- c(
  # Core tidyverse
  "tidyverse",      # tidyr, dplyr, ggplot2, readr
  "dplyr",          # Data wrangling
  "tidyr",          # Data tidying
  "ggplot2",        # Visualization
  
  # Statistical testing
  "car",            # Levene's test, VIF, diagnostics
  "agricolae",      # Agricultural design generators & post-hoc tests
  "lme4",           # Mixed models
  "lmerTest",       # p-values for lmer models
  "AgroR",          # Agricultural ANOVA wrapper
  
  # Post-hoc & comparisons
  "multcomp",       # Multiple comparisons
  "multcompView",   # Compact letter displays
  "emmeans",        # Estimated marginal means
  "FSA",            # Dunn test, non-parametric methods
  
  # Data exploration
  "psych",          # pairs.panels for correlation matrices
  "VIM",            # Visualization of missing data
  "mice"            # Multiple imputation
)

install.packages(packages)
```

---

## 💡 Key Principles to Remember

### **Statistical Rigor**
1. Always check assumptions before running tests
2. Report effect sizes, not just p-values
3. Use appropriate alternatives for non-normal data
4. Multiple comparisons require adjustment (Tukey, Bonferroni)

### **Experimental Design**
1. **Randomization** - Eliminates bias
2. **Replication** - Enables error estimation
3. **Local Control** - Blocking reduces error
4. **Interaction Testing** - Understand factor relationships

### **Data Presentation**
1. Start with visualizations for exploration
2. Use plots to communicate findings
3. Include error bars (SD or SE)
4. Report CV% for experimental precision
5. Add compact letters for post-hoc comparisons

### **Reproducibility**
1. Document data sources and transformations
2. Version control all code
3. Include random seeds for reproducible sampling
4. Provide cleaned datasets alongside raw data

---

## 📈 Progression Checklist

**Week 2 (Data Wrangling & Visualization)**
- [ ] Master dplyr pipe workflows
- [ ] Create publication-quality ggplot2 visualizations
- [ ] Build summary tables for reports
- [ ] Practice with real agricultural datasets

**Week 3 (One-Way ANOVA)**
- [ ] Understand ANOVA assumptions
- [ ] Run Shapiro-Wilk and Levene tests
- [ ] Execute Tukey, LSD, Duncan post-hoc tests
- [ ] Generate compact letter displays
- [ ] Know when to use non-parametric alternatives

**Week 4 (Two-Way ANOVA & Design)**
- [ ] Interpret main effects and interactions
- [ ] Visualize interaction patterns
- [ ] Design experiments using agricolae
- [ ] Build mixed models with random effects
- [ ] Apply AgroR for quick agricultural ANOVA

---

## 🔗 Quick Navigation

| Need Help With? | Location |
|-----------------|----------|
| dplyr basics | `01_Data-Wrangling/Wrangling_dplyr.qmd` |
| ggplot2 advanced | `02_ggplot/Visualization.qmd` |
| One-way ANOVA | `03_One-Way-ANOVA/One-Way-ANOVA.qmd` |
| Post-hoc tests | `03_One-Way-ANOVA/Post_hoc.qmd` |
| Two-way ANOVA | `04_Two_Way_ANOVA/Two_way_anova.qmd` |
| Experimental design theory | `Agricultural_Experimental_Design.pdf` |

---

## 📚 Additional Resources

- **R for Data Science** by Hadley Wickham & Garrett Grolemund
- [ggplot2 official book](https://ggplot2-book.org/)
- [dplyr documentation](https://dplyr.tidyverse.org/)
- [Statistical Rethinking](https://xcelab.net/rethinking/) - Deep understanding of statistics
- [AgroR Package Documentation](https://cran.r-project.org/web/packages/AgroR/)
- [agricolae Guide](https://cran.r-project.org/web/packages/agricolae/)

---

## ✅ What's Next After Week 4?

**Recommended Advanced Topics:**
1. **Regression & Model Selection** - AIC/BIC, stepwise selection
2. **Multicollinearity** - VIF assessment, Ridge regression
3. **Machine Learning** - Predictive modeling for crop yield
4. **Time Series** - Phenological data analysis
5. **Bayesian Methods** - Prior specification for agricultural experiments

---

**Last Updated:** July 2, 2026

---

> **Remember:** The goal isn't just to run statistical tests, but to understand your data, ask meaningful questions, and communicate results clearly to agricultural stakeholders.
