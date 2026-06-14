# 🌾 R Language: Agricultural Statistical Modeling & Analysis

> **A comprehensive guide to statistical modeling, experimental design, and data analysis in R with a focus on agricultural applications.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language](https://img.shields.io/badge/Language-R-blue.svg)](https://www.r-project.org/)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)](#)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-June%202026-orange.svg)](#)

## 📋 Table of Contents

- [Overview](#overview)
- [Course Structure](#course-structure)
- [Getting Started](#getting-started)
- [Repository Organization](#repository-organization)
- [Key Concepts](#key-concepts)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage Examples](#usage-examples)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

## 🎯 Overview

This repository provides a complete learning resource for agricultural data scientists and statisticians working with R. It covers fundamental R programming, exploratory data analysis, advanced statistical modeling, experimental design theory, and predictive modeling techniques—all contextualized for agricultural research and crop yield optimization.

### Key Features

- 📊 **Five-Part Structured Curriculum** - From basics to advanced modeling
- 🌱 **Agriculture-Focused** - Real-world applications in crop science
- 📈 **Hands-On Examples** - Practical code snippets and workflows
- 🔬 **Experimental Design** - CRD, RCBD, Factorial, Split-Plot designs
- 🤖 **Predictive Analytics** - Linear regression, multicollinearity handling, model selection
- 🛠️ **Automated Analysis** - Introduction to AgroR package for streamlined workflows

---

## 📚 Course Structure

### **Part 1: Foundations & Exploratory Data Analysis**

Master R fundamentals and prepare data for analysis:

- **Directory Management**
  - `getwd()` - Check active directory
  - `setwd()` - Set working directory
  - `list.files()` - Inspect files

- **Basic Programming Architecture**
  - Conditional logic (if/else statements)
  - Loops (for, while)
  - Custom functions

- **Data Structures & Attributes**
  - Atomic types (numeric, character, logical, integer, complex)
  - Vectors and subsetting
  - Type conversion (casting)

- **Descriptive & Summary Statistics**
  - Dimension inspection: `nrow()`, `ncol()`
  - Summary functions: `head()`, `tail()`, `summary()`
  - Central tendency: `mean()`, `median()`, `mode()`
  - Spread metrics: `var()`, `sd()`, `quantile()`

- **Missing Data Handling**
  - Detection with `is.na()`
  - Omission with `na.omit()`
  - Imputation strategies
  - VIM and mice packages for advanced handling

---

### **Part 2: Advanced Data Manipulation & Visualizations**

Transform and visualize agricultural data:

- **Data Wrangling with dplyr**
  - `filter()` - Select rows by condition
  - `group_by()` - Subdivide data
  - `summarise()` - Aggregate statistics
  - `mutate()` - Create/transform columns
  - `case_when()` - Vectorized conditions
  - `select()`, `rename()`, `distinct()` - Column operations

- **Visualization: Base R vs. ggplot2**
  - Base R plotting (`plot()`, `lines()`)
  - ggplot2 geometries (`geom_point()`, `geom_line()`, `geom_boxplot()`)
  - Distribution analysis (`geom_violin()`, `geom_jitter()`)
  - Bar chart aggregations (`geom_bar()`)
  - Advanced layouts (`facet_wrap()`)
  - Themes and color palettes

---

### **Part 3: Experimental Designs & Inferential Statistics**

Analyze agricultural experiments scientifically:

- **Foundational Design Principles**
  - Replication, Randomization, Local Control
  - Factors, Levels, Treatments
  - Degrees of Freedom

- **ANOVA Models**
  - **CRD (Completely Randomized Design)**
    ```R
    model <- aov(yield ~ treatment, data = data)
    ```
  - **RCBD (Randomized Complete Block Design)**
    ```R
    model <- aov(yield ~ treatment + block, data = data)
    ```
  - **Factorial Designs** - Multi-factor analysis with interactions
  - **Split-Plot Design** - Nested factor structures
    ```R
    aov(yield ~ irrigation * fertilizer + Error(block/irrigation), data = data)
    ```

- **Diagnostic Checks**
  - Normality: `shapiro.test()`
  - Homogeneity of Variance: `leveneTest()`
  - Visual inspections: Residuals, Q-Q plots, Scale-Location

- **Post-Hoc Testing**
  - Tukey HSD (standard, conservative)
  - Fisher's LSD (early screening)
  - Duncan's MRT (medium strictness)
  - Compact Letter Display (CLD) for results

- **Non-Parametric Alternatives**
  - Kruskal-Wallis Test
  - Friedman Test
  - Dunn's Test

- **Mixed-Effects Models**
  ```R
  model <- lmer(yield ~ treatment + (1|block), data = data)
  ```

---

### **Part 4: Predictive Modeling & Advanced Regression**

Build robust prediction models:

- **Linear Regression Analysis**
  - Simple and multiple regression
  - Variance components (SST, SSR, SSE)
  - R² and Adjusted R² interpretation

- **Multicollinearity Diagnostics**
  - VIF (Variance Inflation Factor)
  - Management strategies:
    - Variable dropping
    - Variable combination
    - Principal Component Analysis (PCA)
    - Ridge Regression (L2 penalty)

- **Model Selection Criteria**
  - AIC (Akaike Information Criterion)
  - BIC (Bayesian Information Criterion)
  - Stepwise regression

- **Model Accuracy & Predictions**
  - `predict()` for new data
  - RMSE (Root Mean Square Error)
  - Relative RMSE (rRMSE) interpretation

---

### **Part 5: Automated Agricultural Evaluation (AgroR)**

Streamline agricultural analysis workflows:

- **Key Parameters**
  - `trat` - Treatment variable
  - `resp` - Response variable (yield)
  - `bloco` - Blocking variable
  - `quali` - Qualitative (TRUE) or quantitative (FALSE)

- **Core Commands**
  - CRD: `DIC(trat, resp, quali = TRUE)`
  - RCBD: `DBC(trat, block, resp, quali = TRUE)`
  - Polynomial evaluation for dose-response curves

---

## 🚀 Getting Started

### Prerequisites

- **R** (version 4.0 or higher)
- **RStudio** (recommended IDE)
- Basic understanding of statistics and experimental design
- Familiarity with command-line operations

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Durjoysarker-swarup/R-Language.git
   cd R-Language
   ```

2. **Install required R packages**
   ```R
   # Base packages (usually pre-installed)
   packages <- c(
     "dplyr",        # Data wrangling
     "ggplot2",      # Visualization
     "car",          # Diagnostic tests
     "lmerTest",     # Mixed-effects models
     "emmeans",      # Post-hoc testing
     "multcomp",     # Comparisons
     "FSA",          # Non-parametric tests
     "VIM",          # Missing data visualization
     "mice",         # Multiple imputation
     "glmnet",       # Ridge regression
     "agricolae",    # Agricultural design
     "AgroR"         # Automated analysis
   )
   
   install.packages(packages)
   ```

3. **Open the R Project**
   ```R
   # In RStudio, File > Open Project > R-Language.Rproj
   ```

---

## 📁 Repository Organization

```
R-Language/
├── README.md                 # This file
├── LICENSE                   # MIT License
├── CONTRIBUTING.md           # Contribution guidelines
├── CODE_OF_CONDUCT.md        # Community standards
├── STRUCTURE.md              # Detailed repository structure
├── R-Language.Rproj          # RStudio project file
├── _quarto.yml               # Quarto configuration
├── Index.qmd                 # Main index page
│
├── Basic/                    # Part 1: Foundations & EDA
│   ├── 01_Directory_Management.R
│   ├── 02_Programming_Basics.R
│   ├── 03_Data_Structures.R
│   ├── 04_Descriptive_Statistics.R
│   └── 05_Missing_Data_Handling.R
│
├── Data_Wrangling/           # Part 2: Manipulation & Visualization
│   ├── 01_dplyr_Fundamentals.R
│   ├── 02_Data_Transformation.R
│   ├── 03_BaseR_Visualization.R
│   └── 04_ggplot2_Advanced.R
│
├── Experimental_Design/      # Part 3: ANOVA & Inferential Stats
│   ├── 01_Design_Principles.R
│   ├── 02_CRD_Analysis.R
│   ├── 03_RCBD_Analysis.R
│   ├── 04_Factorial_Design.R
│   ├── 05_Split_Plot_Design.R
│   ├── 06_Mixed_Effects_Models.R
│   └── 07_Post_Hoc_Testing.R
│
├── Predictive_Modeling/      # Part 4: Regression & Prediction
│   ├── 01_Linear_Regression.R
│   ├── 02_Multicollinearity.R
│   ├── 03_Model_Selection.R
│   └── 04_Model_Evaluation.R
│
├── Automated_Analysis/       # Part 5: AgroR Package
│   ├── 01_AgroR_Introduction.R
│   ├── 02_CRD_Automation.R
│   └── 03_RCBD_Automation.R
│
├── Data/                     # Sample datasets
│   ├── wheat_yield.csv
│   ├── field_trials.csv
│   └── crop_nutrients.csv
│
├── Reports/                  # Generated reports
│   ├── 01_EDA_Report.Rmd
│   ├── 02_ANOVA_Summary.Rmd
│   └── 03_Model_Comparison.Rmd
│
├── Self-Learning/            # Exercises and practice
│   ├── Exercises.Rmd
│   └── Solutions/
│
└── _site/                    # Rendered Quarto output
```

---

## 🎓 Key Concepts

### Agricultural Statistics Fundamentals

| Concept | Definition | Use Case |
|---------|-----------|----------|
| **Replication** | Repeating trials to estimate error | Validating treatment effects |
| **Randomization** | Random unit assignment to treatments | Removing bias, enabling valid inference |
| **Local Control** | Blocking homogeneous units | Reducing external variation |
| **CRD** | Completely randomized design | Uniform experimental units |
| **RCBD** | Randomized complete block design | Accounts for known field gradients |
| **Interaction** | Effect of one factor depends on another | Factorial designs, interpretation |
| **Post-Hoc Test** | Pairwise comparisons after ANOVA | Identifying specific group differences |

### Statistical Terms

- **p-value < 0.05** - Result is statistically significant at 5% level
- **R²** - Proportion of variance explained by predictors (0-1)
- **RMSE** - Average prediction error in original units
- **VIF > 5** - Significant multicollinearity concern
- **Degrees of Freedom** - Independent observations minus constraints (n-1)

---

## 📊 Usage Examples

### Example 1: Basic Summary Statistics

```R
# Load data
data <- read.csv("Data/wheat_yield.csv")

# Get dimensions
nrow(data)  # Number of rows
ncol(data)  # Number of columns

# Summary statistics
summary(data)
mean(data$yield, na.rm = TRUE)
sd(data$yield, na.rm = TRUE)
```

### Example 2: Data Wrangling with dplyr

```R
library(dplyr)

# Filter and summarize
data %>%
  filter(treatment != "Control") %>%
  group_by(region) %>%
  summarise(
    avg_yield = mean(yield, na.rm = TRUE),
    max_yield = max(yield, na.rm = TRUE),
    n = n()
  )
```

### Example 3: ANOVA - Completely Randomized Design

```R
# Fit CRD model
model <- aov(yield ~ treatment, data = data)

# Check assumptions
shapiro.test(residuals(model))  # Normality
leveneTest(yield ~ treatment, data = data)  # Homogeneity

# View results
summary(model)

# Post-hoc test
library(emmeans)
multcomp::cld(emmeans(model, ~ treatment), 
              adjust = "tukey", 
              Letters = letters)
```

### Example 4: Visualization with ggplot2

```R
library(ggplot2)

ggplot(data, aes(x = treatment, y = yield, fill = treatment)) +
  geom_boxplot() +
  geom_jitter(width = 0.2, alpha = 0.5) +
  facet_wrap(~region) +
  theme_minimal() +
  labs(title = "Crop Yield by Treatment and Region",
       x = "Treatment", y = "Yield (kg/ha)") +
  theme(legend.position = "bottom")
```

### Example 5: Mixed-Effects Model with Blocks

```R
library(lmerTest)

# Fit model with random block effect
model <- lmer(yield ~ treatment + (1|block), data = data)

# Get results with p-values
anova(model, type = 3)
summary(model)
```

---

## 🤝 Contributing

We welcome contributions from educators, students, and agricultural data scientists! 

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/YourFeature`)
3. **Add your improvements** (code examples, documentation, datasets)
4. **Commit changes** (`git commit -m 'Add: Clear description of changes'`)
5. **Push to branch** (`git push origin feature/YourFeature`)
6. **Open a Pull Request**

### Contribution Guidelines

- Follow R style guide (snake_case for variables/functions)
- Add comments for complex logic
- Include example output
- Test code before submitting
- Update documentation if needed

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📋 Code of Conduct

We are committed to providing a welcoming and inclusive environment. See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for details.

---

## 📚 Resources & References

### Official Documentation
- [R Project Official Site](https://www.r-project.org/)
- [RStudio IDE](https://www.rstudio.com/products/rstudio/)
- [Tidyverse (dplyr, ggplot2)](https://www.tidyverse.org/)

### Books & Guides
- *R for Data Science* - Hadley Wickham & Garrett Grolemund
- *Statistical Design and Analysis of Agricultural Experiments* - Hinkelmann & Kempthorne
- *ggplot2: Elegant Graphics for Data Analysis* - Hadley Wickham

### Agricultural Research Resources
- [Agronomy Journal](https://acsess.onlinelibrary.wiley.com/journal/10030196)
- [Crop Science Society of America](https://www.crops.org/)
- [Statistical Methods for Agricultural Research](https://www.cimmyt.org/)

---

## 📞 Support & Contact

- **Issues**: Report bugs or suggest features via [GitHub Issues](https://github.com/Durjoysarker-swarup/R-Language/issues)
- **Discussions**: Join community discussions at [GitHub Discussions](https://github.com/Durjoysarker-swarup/R-Language/discussions)
- **Email**: [contact@example.com](mailto:contact@example.com)

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### You are free to:
- ✅ Use for commercial purposes
- ✅ Modify the code
- ✅ Distribute the code
- ✅ Use for private purposes

### You must:
- 📋 Include the original license and copyright notice

---

## 🌟 Citation

If you use this repository in your research or teaching, please cite:

```bibtex
@repository{rLanguageAgriculture2026,
  author = {Durjoysarker-swarup},
  title = {R Language: Agricultural Statistical Modeling and Analysis},
  url = {https://github.com/Durjoysarker-swarup/R-Language},
  year = {2026}
}
```

---

## 👤 Author

**Durjoysarker Swarup**
- GitHub: [@Durjoysarker-swarup](https://github.com/Durjoysarker-swarup)
- Repository: [R-Language](https://github.com/Durjoysarker-swarup/R-Language)

---

## 🙏 Acknowledgments

- Agricultural research community for providing real-world use cases
- R development team and package maintainers
- Students and educators who provide feedback and suggestions

---

## 📈 Repository Statistics

- **Last Updated**: June 2026
- **Status**: Active Development
- **License**: MIT
- **Primary Language**: R
- **Focus**: Agricultural Statistics & Data Science

---

<div align="center">

**⭐ If you find this repository helpful, please consider giving it a star!** ⭐

[Report Issue](https://github.com/Durjoysarker-swarup/R-Language/issues) • [Request Feature](https://github.com/Durjoysarker-swarup/R-Language/discussions) • [View Profile](https://github.com/Durjoysarker-swarup)

</div>

---

*Last updated: June 2026*
