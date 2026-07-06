# Week 1: R Fundamentals

Complete introduction to R programming with agricultural applications. This folder covers essential concepts from data types to hypothesis testing, establishing a solid foundation for advanced statistical analysis.

---

## 📚 Contents Overview

| File | Focus Area | Key Topics | Difficulty |
|------|-----------|-----------|------------|
| `01_R basics.qmd` | Core Language | Variables, vectors, data frames, loops, conditionals, functions | ⭐ Beginner |
| `02_Missing value.qmd` | Data Cleaning | NA detection, imputation, VIM & mice packages | ⭐ Beginner |
| `03_Data Exploration.qmd` | Descriptive Stats | EDA, summary statistics, quantiles, mode | ⭐ Beginner |
| `04_Vizualization.qmd` | Plotting | Base R plots, ggplot2 basics, layering | ⭐⭐ Intermediate |
| `05_Significance test.qmd` | Statistics | t-tests, ANOVA introduction, dplyr pipelines | ⭐⭐ Intermediate |

---

## 🎯 Learning Objectives

By completing Week 1, you will be able to:

✅ Write and run R code with proper syntax and best practices  
✅ Create and manipulate vectors, data frames, and matrices  
✅ Use conditional statements and loops for automation  
✅ Write custom functions for reusable code  
✅ Identify and handle missing data appropriately  
✅ Perform exploratory data analysis (EDA)  
✅ Create publication-quality visualizations with base R and ggplot2  
✅ Conduct hypothesis tests (t-test, one-way ANOVA)  
✅ Wrangle data using dplyr for analysis  

---

## 📖 Detailed Breakdown

### **1️⃣ R Basics** (`01_R basics.qmd`)

**What You'll Learn:**
- Setting up your working directory
- Data types: numeric, character, logical, integer, complex
- Vector creation and indexing
- Matrix and data frame operations
- Conditional statements (if/else)
- Loops (for, while, repeat)
- Writing custom functions
- Using apply family functions



### **2️⃣ Missing Data Handling** (`02_Missing value.qmd`)

**What You'll Learn:**
- Detecting missing values with `is.na()`
- Removing missing data with `na.omit()`
- Imputation strategies (mean filling, MICE)
- VIM package for visualizing missingness
- mice package for multiple imputation


**When to Use Each Method:**
- **Deletion:** < 5% missing, MCAR (Missing Completely At Random)
- **Mean filling:** Quick exploratory analysis, < 10% missing
- **MICE:** Complex missingness patterns, preserves relationships

---

### **3️⃣ Data Exploration** (`03_Data Exploration.qmd`)

**What You'll Learn:**
- Exploratory Data Analysis (EDA) workflow
- Descriptive statistics (mean, median, sd, var, quantiles)
- Creating custom statistics functions
- Identifying outliers and distributions


### **4️⃣ Visualization** (`04_Vizualization.qmd`)

**What You'll Learn:**
- Base R plotting functions
- ggplot2 grammar of graphics
- Common plots: scatter, line, box, bar
- Layering and customization
- Time series visualization


**Agricultural Examples:**
- Yield vs. fertilizer dose scatter plot
- Time series of crop growth
- Box plots comparing treatments
- Grouped bar charts by region/season

---

### **5️⃣ Significance Testing** (`05_Significance test.qmd`)

**What You'll Learn:**
- Hypothesis testing framework
- Two-sample t-tests
- One-way ANOVA basics
- Using dplyr for data summarization
- Interpreting p-values and effect sizes

---


## 🗂️ Working with `agri_dataset.csv`

Sample agricultural dataset included:
- Variables: Treatment, Yield, Region (sample)
- Use for practicing all Week 1 concepts
- ~10 observations (expandable for practice)



---

## 🚀 Quick Start Guide

### Step 1: Set Working Directory
```r
setwd("~/path/to/01_Basic")
getwd()
```

### Step 2: Load and Explore Data
```r
data <- read.csv("agri_dataset.csv")
head(data)
summary(data)
```

### Step 3: Practice Each Concept
```r
# Vectors
v <- c(10, 20, 30, 40, 50)
mean(v)
v[v > 25]

# Data frames
df <- data.frame(x = 1:5, y = 6:10)
df$x + df$y

# Plotting
plot(data$Treatment, data$Yield)
# Or with ggplot2
library(ggplot2)
ggplot(data, aes(x = Treatment, y = Yield)) + geom_boxplot()

# Statistics
t.test(data$Yield ~ data$Treatment)
model <- aov(Yield ~ Treatment, data = data)
summary(model)
```

### Step 4: Render Quarto Files
```r
# Install quarto if needed
install.packages("quarto")

# Render individual files
quarto::quarto_render("01_R basics.qmd")
```

---


## 🔗 Required Packages

```r
# Install all Week 1 packages
packages <- c("ggplot2", "dplyr", "tidyr", "VIM", "mice", "car")
install.packages(packages)

# Load as needed
library(ggplot2)
library(dplyr)
```

---

## 💡 Common Pitfalls to Avoid

1. **Forgetting `na.rm = TRUE`** when NAs are present
2. **Indexing confusion:** R uses 1-based indexing (unlike Python)
3. **Factor vs. character:** Categorical variables need careful handling
4. **Assuming normality:** Always check assumptions before tests
5. **Ignoring effect size:** p-values alone don't tell the full story
6. **Using wrong plot type:** Choose visualization that best shows your data

---


## ✅ What's Next?

After mastering Week 1, you're ready for:
- **Week 2:** Advanced data wrangling and visualization
- **Week 3:** One-way ANOVA and post-hoc tests
- **Week 4:** Two-way ANOVA and mixed models

---

**Last Updated:** July 2, 2026

---

> **Pro Tip:** Practice writing your own code rather than copying. Try modifying examples to work with different datasets or variables. The best way to learn R is by doing!
