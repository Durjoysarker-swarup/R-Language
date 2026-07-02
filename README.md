# R Language Learning: Agricultural Statistics & Data Science

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![R](https://img.shields.io/badge/R%20-276DC3?style=for-the-badge&logo=r&logoColor=white)](https://www.r-project.org/)
[![Status: Active](https://img.shields.io/badge/Status-Active-brightgreen.svg)](#)

A comprehensive, structured learning repository documenting **4 weeks of intensive R language training** focused on agricultural statistics, experimental design, and data science applications. This portfolio demonstrates proficiency in data manipulation, visualization, statistical modeling, and practical agricultural research methodology.

---

## 📚 Repository Overview

This repository is organized into two main learning tracks:

### **Track 1: Fundamentals** (`01_Basic`)
Core R programming concepts with agricultural applications, covering data types, visualization, and statistical testing.

### **Track 2: Advanced Analysis** (`02_Self-Learning`)
Specialized topics in agricultural experimentation: data wrangling, visualization, ANOVA designs, and experimental methodology.

**Total Coverage:** 4 weeks of structured, hands-on learning in R programming and agricultural statistics

---

## 🎯 Key Learning Outcomes

### Statistical Analysis
- ✅ **Hypothesis Testing:** t-tests, ANOVA, and non-parametric tests (Kruskal-Wallis, Friedman)
- ✅ **ANOVA Designs:** One-way, two-way, factorial, and mixed models with random effects
- ✅ **Post-hoc Testing:** Tukey HSD, LSD, Duncan tests with compact letter displays
- ✅ **Assumption Validation:** Normality (Shapiro-Wilk), homogeneity (Levene), independence (Durbin-Watson)

### Data Science Skills
- ✅ **Data Wrangling:** dplyr pipelines (filter, group_by, mutate, summarise)
- ✅ **Visualization:** ggplot2 advanced plots (faceting, time series, grouped comparisons)
- ✅ **Missing Data:** Imputation techniques (mean filling, MICE algorithm)
- ✅ **Model Selection:** AIC/BIC comparison, stepwise regression, RMSE accuracy metrics

### Experimental Design
- ✅ **Research Designs:** CRD, RCBD, Factorial, Split-Plot, Strip-Plot
- ✅ **Design Generators:** Using agricolae package for automated randomization
- ✅ **Agricultural Applications:** Fertilizer trials, treatment comparisons, yield optimization

### Advanced Topics
- ✅ **Regression Analysis:** Linear/multiple regression with diagnostics
- ✅ **Multicollinearity Handling:** VIF assessment and Ridge regression
- ✅ **Mixed Models:** lmer() for hierarchical data with random effects
- ✅ **AgroR Package:** Agricultural-specific ANOVA functions with built-in diagnostics

---

## 📁 Repository Structure

```
R-Language/
├── 01_Basic/                           # Week 1: Fundamentals
│   ├── README.md                       # Detailed guide for basics
│   ├── 01_R basics.qmd                # R syntax, vectors, data frames, functions
│   ├── 02_Missing value.qmd           # Missing data handling & imputation
│   ├── 03_Data Exploration.qmd        # Descriptive statistics & EDA
│   ├── 04_Vizualization.qmd           # Base R and ggplot2 plotting
│   ├── 05_Significance test.qmd       # t-tests and ANOVA introduction
│   └── agri_dataset.csv               # Sample agricultural dataset
│
├── 02_Self-Learning/                   # Weeks 2-4: Advanced Topics
│   ├── README.md                       # Detailed guide for advanced topics
│   ├── Agricultural_Experimental_Design.pdf
│   │
│   ├── 01_Data-Wrangling/             # Week 2.1: dplyr Data Manipulation
│   │   ├── README.md
│   │   ├── Wrangling_dplyr.qmd
│   │   ├── fertilizer_yield_data.csv
│   │   └── Summary table.csv
│   │
│   ├── 02_ggplot/                     # Week 2.2: Advanced Visualization
│   │   ├── README.md
│   │   ├── Visualization.qmd
│   │   ├── agriculture_sample_dataset.csv
│   │   └── time_series_agriculture.csv
│   │
│   ├── 03_One-Way-ANOVA/              # Week 3: One-Way ANOVA & Post-Hoc
│   │   ├── README.md
│   │   ├── One-Way-ANOVA.qmd
│   │   ├── Post_hoc.qmd
│   │   ├── fertilizer_yield_for_anova.csv
│   │   ├── agriculture_posthoc_data.csv
│   │   └── non_normal_yield_data.csv
│   │
│   └── 04_Two_Way_ANOVA/              # Week 4: Two-Way ANOVA & Interactions
│       ├── README.md
│       ├── Two_way_anova.qmd
│       └── agriculture_two_way_anova.csv
│
├── the plan.md                        # Consolidated learning progress summary
├── Index.qmd                          # Quarto index file
├── _quarto.yml                        # Quarto configuration
└── R-Language.Rproj                   # RStudio project file
```

---

## 🔬 Key Topics by Week

### **Week 1: R Fundamentals**
| Topic | Files | Key Concepts |
|-------|-------|--------------|
| R Basics | `01_R basics.qmd` | Variables, vectors, data frames, conditionals, loops, functions |
| Missing Data | `02_Missing value.qmd` | NA handling, imputation, VIM & mice packages |
| EDA | `03_Data Exploration.qmd` | summary(), mean, median, var, sd, quantiles, mode |
| Visualization | `04_Vizualization.qmd` | plot(), barplot(), ggplot2 basics |
| Hypothesis Testing | `05_Significance test.qmd` | t.test(), aov(), dplyr pipelines |

### **Week 2: Data Wrangling & Visualization**
| Topic | Subfolder | Skills |
|-------|-----------|--------|
| Data Wrangling | `01_Data-Wrangling/` | dplyr: filter, group_by, mutate, summarise, arrange |
| ggplot2 | `02_ggplot/` | geom_line, geom_bar, facet_wrap, time series plots |

### **Week 3: One-Way ANOVA & Post-Hoc Tests**
| Topic | Files | Methods |
|-------|-------|---------|
| ANOVA | `One-Way-ANOVA.qmd` | aov(), assumption checks (Shapiro, Levene) |
| Post-Hoc | `Post_hoc.qmd` | Tukey, LSD, Duncan, emmeans, cld letter displays |
| Non-Parametric | Included | Kruskal-Wallis, Dunn test alternatives |

### **Week 4: Two-Way ANOVA & Interactions**
| Topic | Files | Content |
|-------|-------|---------|
| Two-Way ANOVA | `Two_way_anova.qmd` | Main effects, interactions, visualization |
| Mixed Models | Included | lmer() with random effects for blocked designs |
| AgroR Package | Included | Pre-built ANOVA functions with agricultural focus |

---

## 🚀 Getting Started

### Prerequisites
- R (≥4.0) - [Download R](https://www.r-project.org/)
- RStudio - [Download RStudio](https://posit.co/download/rstudio-desktop/)
- Git (optional, for cloning)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Durjoysarker-swarup/R-Language.git
   cd R-Language
   ```

2. **Open the RStudio project:**
   ```bash
   # Open R-Language.Rproj in RStudio
   ```

3. **Install required packages:**
   ```r
   packages <- c("tidyverse", "ggplot2", "dplyr", "VIM", "mice", 
                 "car", "agricolae", "lme4", "lmerTest", "AgroR", 
                 "multcomp", "multcompView", "FSA", "psych")
   install.packages(packages)
   ```

### Rendering Files
Files are in **Quarto markdown (.qmd)** format. Render them as:

```r
# Install quarto if needed
install.packages("quarto")

# Render individual files
quarto::quarto_render("01_Basic/01_R basics.qmd")

# Or render all with Quarto CLI:
# quarto render
```

---

## 📊 Example Workflows

### Quick Start: One-Way ANOVA
```r
# Load data
data <- read.csv("02_Self-Learning/03_One-Way-ANOVA/fertilizer_yield_for_anova.csv")

# Run ANOVA
model <- aov(Yield ~ Treatment, data = data)
summary(model)

# Post-hoc test
agricolae::HSD.test(model, "Treatment", console = TRUE)
```

### Data Wrangling with dplyr
```r
library(dplyr)

data %>%
  filter(Yield > 50) %>%
  group_by(Treatment) %>%
  summarise(
    mean_yield = mean(Yield),
    sd_yield = sd(Yield),
    n = n()
  ) %>%
  arrange(desc(mean_yield))
```

### Visualization with ggplot2
```r
library(ggplot2)

ggplot(data, aes(x = Treatment, y = Yield, fill = Treatment)) +
  geom_boxplot() +
  geom_jitter(width = 0.2, alpha = 0.5) +
  theme_classic() +
  labs(title = "Yield by Treatment", y = "Yield (kg/ha)", x = "Treatment")
```

---

## 📖 Learning Resources Referenced

- **Quarto Documentation:** Dynamic R markdown reports
- **ggplot2 Book:** Advanced data visualization
- **Experimental Design Theory:** CRD, RCBD, Factorial, Split-Plot designs
- **Agricultural Statistics:** AgroR package & agricolae package documentation
- **Mixed Models:** lme4 and lmerTest for hierarchical data

---

## 🎓 Scholarship Portfolio Highlights

This repository demonstrates:

1. **Technical Proficiency**
   - Mastery of R programming fundamentals to advanced statistical modeling
   - Experience with industry-standard packages (tidyverse, ggplot2, lme4)
   - Hands-on implementation of complex experimental designs

2. **Statistical Rigor**
   - Complete workflow from hypothesis testing to diagnostics
   - Proper assumption validation and non-parametric alternatives
   - Publication-ready visualization and reporting

3. **Domain Expertise**
   - Applied understanding of agricultural experimental design
   - Practical experience with research methodologies (CRD, RCBD, Factorial)
   - Ability to handle real agricultural data and derive insights

4. **Self-Directed Learning**
   - Structured 4-week progression from basics to advanced topics
   - Independent mastery of specialized packages (AgroR, agricolae, lme4)
   - Clear documentation and reproducible research practices

---

## 📝 Progress Summary

**Current Status:** ✅ Week 4 Complete (All Major Topics Covered)

See [`the plan.md`](./the%20plan.md) for a detailed consolidated summary of all learning objectives, code examples, and key concepts covered in each week.

---

## 💡 Future Enhancements

- [ ] Regression diagnostics and model selection deep-dive
- [ ] Machine learning applications in agriculture (caret, randomForest)
- [ ] Bayesian statistics for experimental design
- [ ] Time series analysis for crop phenology
- [ ] Shiny app for interactive ANOVA visualizations
- [ ] Publication-ready templates for research reports

---

## 📧 Contact & Collaboration

- **Author:** Durjoysarker-swarup
- **GitHub:** [@Durjoysarker-swarup](https://github.com/Durjoysarker-swarup)
- **Repository:** [R-Language](https://github.com/Durjoysarker-swarup/R-Language)

Interested in collaboration on agricultural data science projects? Feel free to open an issue or discussion!

---

## 📄 License

This project is licensed under the **MIT License** - see [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Agricultural statistics community and open-source R package developers
- Quarto documentation and Posit community
- All contributors to agricolae, AgroR, and tidyverse ecosystems

---

**Last Updated:** July 2, 2026

> *"Data is the new oil, but agriculture feeds the world. Let's make them work together."*
