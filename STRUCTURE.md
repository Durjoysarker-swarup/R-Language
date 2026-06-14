# Repository Structure

This document provides a detailed overview of the R Language repository structure, explaining the purpose of each directory and file.

## 📁 Directory Tree

```
R-Language/
├── README.md                          # Main project documentation (start here!)
├── LICENSE                            # MIT License
├── CONTRIBUTING.md                    # Guidelines for contributors
├── CODE_OF_CONDUCT.md                 # Community standards
├── STRUCTURE.md                       # This file - directory guide
├── R-Language.Rproj                   # RStudio project file
├── _quarto.yml                        # Quarto configuration for documentation
├── Index.qmd                          # Main index page (Quarto)
│
├── 📚 Basic/                          # Part 1: Foundations & Exploratory Data Analysis
│   ├── 01_Directory_Management.R      # Working directory setup and file management
│   ├── 02_Programming_Basics.R        # Conditional logic, loops, functions
│   ├── 03_Data_Structures.R           # Vectors, data types, subsetting, casting
│   ├── 04_Descriptive_Statistics.R    # Summary functions, central tendency, spread
│   └── 05_Missing_Data_Handling.R     # NA detection, omission, imputation, VIM, mice
│
├── 📊 Data_Wrangling/                 # Part 2: Advanced Data Manipulation & Visualization
│   ├── 01_dplyr_Fundamentals.R        # filter, select, mutate, summarise, group_by
│   ├── 02_Data_Transformation.R       # case_when, rename, distinct, joins
│   ├── 03_BaseR_Visualization.R       # plot, lines, scatter, line plots, multi-series
│   └── 04_ggplot2_Advanced.R          # ggplot2, geometries, faceting, themes, aesthetics
│
├── 🔬 Experimental_Design/            # Part 3: Experimental Designs & Inferential Statistics
│   ├── 01_Design_Principles.R         # Replication, randomization, local control
│   ├── 02_CRD_Analysis.R              # Completely Randomized Design with ANOVA
│   ├── 03_RCBD_Analysis.R             # Randomized Complete Block Design
│   ├── 04_Factorial_Design.R          # Multi-factor designs, interactions
│   ├── 05_Split_Plot_Design.R         # Split-plot with nested error structures
│   ├── 06_Mixed_Effects_Models.R      # lmer, lmerTest, random effects
│   └── 07_Post_Hoc_Testing.R          # Tukey, Fisher's LSD, Duncan's, Dunn's tests
│
├── 📈 Predictive_Modeling/            # Part 4: Predictive Modeling & Advanced Regression
│   ├── 01_Linear_Regression.R         # Simple & multiple regression, R², variance
│   ├── 02_Multicollinearity.R         # VIF, PCA, Ridge regression, multicollinearity management
│   ├── 03_Model_Selection.R           # AIC, BIC, stepwise regression
│   └── 04_Model_Evaluation.R          # RMSE, predictions, model accuracy assessment
│
├── 🤖 Automated_Analysis/             # Part 5: Automated Agricultural Evaluation (AgroR)
│   ├── 01_AgroR_Introduction.R        # AgroR package overview and setup
│   ├── 02_CRD_Automation.R            # Automated CRD analysis with AgroR
│   └── 03_RCBD_Automation.R           # Automated RCBD analysis with AgroR
│
├── 💾 Data/                           # Sample Datasets for Learning & Practice
│   ├── wheat_yield.csv                # Wheat crop yield data with treatments
│   ├── field_trials.csv               # Multi-location field trial data
│   ├── crop_nutrients.csv             # Nutrient application and response data
│   ├── README_DATA.md                 # Data dictionary and source documentation
│   └── raw/                           # Raw unprocessed datasets
│       └── original_sources.txt       # Links to original data sources
│
├── 📋 Reports/                        # Generated Analysis Reports & Summaries
│   ├── 01_EDA_Report.Rmd              # Exploratory Data Analysis Report (Rmarkdown)
│   ├── 02_ANOVA_Summary.Rmd           # ANOVA Analysis Results & Interpretation
│   ├── 03_Model_Comparison.Rmd        # Model Comparison Report
│   ├── output/                        # Rendered report outputs
│   │   ├── EDA_Report.html            # HTML version of EDA report
│   │   ├── ANOVA_Summary.html         # HTML version of ANOVA summary
│   │   └── Model_Comparison.html      # HTML version of model report
│   └── templates/                     # Report templates for quick report generation
│       └── Analysis_Template.Rmd      # Template for custom reports
│
├── 📚 Self-Learning/                  # Practice Exercises & Solutions
│   ├── Exercises.Rmd                  # Exercise problems (5 parts)
│   │   ├── Part_1_Exercises.Rmd       # EDA and basic statistics problems
│   │   ├── Part_2_Exercises.Rmd       # Data wrangling visualization problems
│   │   ├── Part_3_Exercises.Rmd       # Experimental design problems
│   │   ├── Part_4_Exercises.Rmd       # Regression & prediction problems
│   │   └── Part_5_Exercises.Rmd       # AgroR automation problems
│   ├── Solutions/                     # Answer keys and worked solutions
│   │   ├── Part_1_Solutions.R         # Solutions to Part 1 exercises
│   │   ├── Part_2_Solutions.R         # Solutions to Part 2 exercises
│   │   ├── Part_3_Solutions.R         # Solutions to Part 3 exercises
│   │   ├── Part_4_Solutions.R         # Solutions to Part 4 exercises
│   │   └── Part_5_Solutions.R         # Solutions to Part 5 exercises
│   └── Checklists/                    # Self-assessment checklists
│       ├── Part_1_Checklist.md        # Skills checklist for Part 1
│       ├── Part_2_Checklist.md        # Skills checklist for Part 2
│       ├── Part_3_Checklist.md        # Skills checklist for Part 3
│       ├── Part_4_Checklist.md        # Skills checklist for Part 4
│       └── Part_5_Checklist.md        # Skills checklist for Part 5
│
├── 🛠️ Utilities/                       # Helper Scripts & Utility Functions
│   ├── package_installer.R            # Script to install all required packages
│   ├── data_loader.R                  # Centralized data loading functions
│   ├── custom_functions.R             # Custom utility functions used throughout
│   └── project_setup.R                # One-time project setup script
│
├── 📖 Cheatsheets/                    # Quick Reference Guides
│   ├── R_Basics_Cheatsheet.md         # R syntax quick reference
│   ├── dplyr_Cheatsheet.md            # dplyr functions quick reference
│   ├── ggplot2_Cheatsheet.md          # ggplot2 visualization quick reference
│   ├── ANOVA_Cheatsheet.md            # ANOVA workflow quick reference
│   └── AgroR_Cheatsheet.md            # AgroR package quick reference
│
├── 🔗 References/                     # External Resources & Citations
│   ├── Bibliography.md                # Full bibliography and citations
│   ├── Useful_Links.md                # Links to external learning resources
│   ├── Package_Documentation.md       # Links to R package documentation
│   └── Agricultural_Resources.md      # Links to agricultural research resources
│
├── 🎨 Assets/                         # Images, Diagrams, and Visual Resources
│   ├── diagrams/                      # Process flow diagrams
│   │   ├── ANOVA_Workflow.png         # ANOVA decision workflow diagram
│   │   └── Analysis_Pipeline.png      # Data analysis pipeline visualization
│   ├── screenshots/                   # Tutorial screenshots
│   │   ├── RStudio_Setup.png          # RStudio configuration screenshot
│   │   └── Package_Installation.png   # Package installation screenshot
│   └── logos/                         # Project and brand assets
│       └── R_Language_Logo.png        # Repository logo
│
├── 📋 _site/                          # Rendered Quarto Website Output
│   ├── index.html                     # Home page (auto-generated)
│   ├── search.json                    # Search index (auto-generated)
│   └── ... (other generated files)    # Quarto output directory
│
└── 🔄 .github/                        # GitHub Configuration Files
    ├── workflows/                     # CI/CD workflows
    │   └── tests.yml                  # Automated testing workflow
    ├── ISSUE_TEMPLATE/                # Issue templates
    │   ├── bug_report.md              # Bug report template
    │   └── feature_request.md         # Feature request template
    └── PULL_REQUEST_TEMPLATE.md       # Pull request template
```

---

## 📂 Directory Descriptions

### **📚 Basic/** - Part 1 Foundations
Contains foundational R programming and statistics concepts:
- Working directory management
- Control flow (if/else, loops)
- Data types and structures
- Descriptive statistics
- Missing data handling

**Suitable for**: Beginners, refresher on R basics

---

### **📊 Data_Wrangling/** - Part 2 Manipulation
Advanced data manipulation and visualization techniques:
- dplyr pipeline operations
- Data transformation workflows
- Base R and ggplot2 visualizations
- Multi-series plotting
- Publication-quality graphics

**Suitable for**: Data preparation, exploratory analysis

---

### **🔬 Experimental_Design/** - Part 3 Statistics
Comprehensive experimental design and statistical inference:
- Design principles and terminology
- ANOVA models (CRD, RCBD, Factorial, Split-Plot)
- Mixed-effects models
- Diagnostic testing
- Post-hoc comparisons
- Non-parametric alternatives

**Suitable for**: Research design, statistical analysis

---

### **📈 Predictive_Modeling/** - Part 4 Regression
Advanced regression and prediction techniques:
- Linear regression foundations
- Multicollinearity diagnosis and solutions
- Model selection criteria (AIC, BIC)
- Cross-validation
- Prediction and accuracy assessment

**Suitable for**: Predictive modeling, machine learning

---

### **🤖 Automated_Analysis/** - Part 5 AgroR
Streamlined agricultural analysis workflows:
- AgroR package introduction
- Automated ANOVA with diagnostics
- Automated post-hoc testing
- Publication-ready visualizations
- Dose-response curve fitting

**Suitable for**: Rapid analysis, agricultural research

---

### **💾 Data/**
Sample datasets for learning and practice:
- Real agricultural trial data
- Multiple crop types and treatments
- Includes metadata and documentation
- **raw/**: Original unprocessed data

**File Formats**: CSV (comma-separated values)

---

### **📋 Reports/**
Analysis reports and generated outputs:
- RMarkdown (.Rmd) source files
- HTML rendered versions
- Interpretation and conclusions
- Templates for custom reports

**Usage**: Reference for report structure, run examples

---

### **📚 Self-Learning/**
Practice problems and self-assessment materials:
- **Exercises.Rmd**: 5 parts, multiple problems each
- **Solutions/**: Worked solutions with explanations
- **Checklists/**: Skills assessment per section

**Usage**: Practice, self-study, skill verification

---

### **🛠️ Utilities/**
Helper scripts and utility functions:
- Automated package installation
- Centralized data loading
- Custom functions used throughout
- Project setup automation

**Usage**: Run once during setup, source in other scripts

---

### **📖 Cheatsheets/**
Quick reference guides for rapid lookup:
- Syntax reminders
- Function parameters
- Common workflows
- Troubleshooting tips

**Format**: Markdown for quick browsing

---

### **🔗 References/**
External resources and documentation:
- Bibliography and citations
- Links to official documentation
- Agricultural research resources
- Package documentation links

**Usage**: Looking up definitions, finding external resources

---

### **🎨 Assets/**
Visual resources and diagrams:
- Workflow diagrams
- Process flowcharts
- Screenshots for tutorials
- Project branding

**Format**: PNG, SVG

---

### **_site/**
Auto-generated Quarto website output:
- Read-only (auto-generated)
- Contains rendered HTML from .qmd files
- Search functionality
- Navigation structure

**Note**: Do not manually edit these files

---

### **.github/**
GitHub configuration and automation:
- CI/CD workflow definitions
- Issue and PR templates
- Automated testing
- Project automation

**Usage**: Ensure templates are up-to-date with guidelines

---

## 🎯 How to Use This Repository

### For Beginners
1. Start with **Basic/** directory
2. Follow exercises in **Self-Learning/**
3. Use **Cheatsheets/** for quick reference
4. Refer to **References/** for external help

### For Learning Data Wrangling
1. Review **Data_Wrangling/** scripts
2. Work through examples in order
3. Practice with datasets in **Data/**
4. Complete exercises in **Self-Learning/**

### For Statistical Analysis
1. Study **Experimental_Design/** thoroughly
2. Match your design to appropriate section
3. Review **Reports/** for example output
4. Use **Utilities/** helper functions

### For Contributing
1. Read **CONTRIBUTING.md**
2. Follow structure in appropriate directory
3. Use templates from **Assets/**
4. Submit pull request with tests

---

## 📝 File Naming Conventions

### R Scripts
```
{Part}_{Section}_{Topic}.R

Examples:
01_Basic_Programming.R
03_RCBD_Analysis.R
04_Linear_Regression.R
```

### Data Files
```
{Topic}_{Description}.csv

Examples:
wheat_yield.csv
field_trials.csv
crop_nutrients.csv
```

### Reports (RMarkdown)
```
{Number}_{Topic}_Report.Rmd

Examples:
01_EDA_Report.Rmd
02_ANOVA_Summary.Rmd
```

### Markdown Documentation
```
{Topic}.md or {Topic}_{Description}.md

Examples:
README.md
CONTRIBUTING.md
Package_Documentation.md
```

---

## 🚀 Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/Durjoysarker-swarup/R-Language.git
   cd R-Language
   ```

2. **Install packages**
   ```R
   source("Utilities/package_installer.R")
   ```

3. **Set up project**
   ```R
   source("Utilities/project_setup.R")
   ```

4. **Start learning**
   - Open `Basic/01_Directory_Management.R`
   - Follow scripts in sequence
   - Complete exercises as you go

---

## 📊 Statistics

| Component | Count |
|-----------|-------|
| Total Scripts | 20+ |
| Sample Datasets | 3+ |
| Exercise Sets | 5 |
| Cheatsheets | 5 |
| Documentation Files | 10+ |

---

## 🔄 Maintenance

- **Last Updated**: June 2026
- **Maintainer**: Durjoysarker-swarup
- **Update Frequency**: Ongoing
- **Contribution Status**: Open to contributions

---

## 📞 Support

For questions about repository structure:
- Check this file first
- Open a GitHub Issue
- Start a Discussion
- Review README.md

---

*Last updated: June 2026*
