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

**Key Code Patterns:**
```r
# Working directory
getwd()
setwd("path/to/directory")

# Data types
typeof(x)
class(x)

# Vectors & indexing
v <- c(1, 2, 3, 4, 5)
v[c(1, 3, 5)]        # Select specific indices
v[v > 3]             # Logical subsetting

# Data frames
df <- data.frame(col1 = 1:5, col2 = letters[1:5])
df$col1              # Access by name
df[1, ]              # First row
df[, 2]              # Second column

# Functions
my_func <- function(x, y) {
  result <- x + y
  return(result)
}

# Conditionals
if (x > 0) {
  print("Positive")
} else if (x == 0) {
  print("Zero")
} else {
  print("Negative")
}

# Loops
for (i in 1:10) {
  print(i)
}
```

**Agricultural Example:**
```r
# Calculate BMI for agricultural workers
height <- c(165, 170, 175)  # cm
weight <- c(65, 72, 80)     # kg

BMI <- weight / (height/100)^2

# Categorize health status
health_status <- ifelse(BMI < 18.5, "Underweight",
                        ifelse(BMI < 25, "Normal",
                               ifelse(BMI < 30, "Overweight", "Obese")))
```

---

### **2️⃣ Missing Data Handling** (`02_Missing value.qmd`)

**What You'll Learn:**
- Detecting missing values with `is.na()`
- Removing missing data with `na.omit()`
- Imputation strategies (mean filling, MICE)
- VIM package for visualizing missingness
- mice package for multiple imputation

**Common Tasks:**

```r
# Detect missing data
is.na(x)
sum(is.na(df))
colSums(is.na(df))

# Visualize missingness
library(VIM)
aggr(df)  # Show proportion of missing per column

# Remove missing
df_clean <- na.omit(df)

# Impute with mean
df$col[is.na(df$col)] <- mean(df$col, na.rm = TRUE)

# Multiple Imputation by Chained Equations (MICE)
library(mice)
imputed <- mice(df, m = 5, method = 'pmm')
df_complete <- complete(imputed, action = 1)
```

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

**Essential Functions:**

```r
# Basic exploration
head(df)           # First 6 rows
tail(df)           # Last 6 rows
nrow(df)           # Number of rows
ncol(df)           # Number of columns
names(df)          # Column names
str(df)            # Structure overview
summary(df)        # Statistical summary

# Descriptive statistics
mean(x, na.rm = TRUE)
median(x, na.rm = TRUE)
sd(x, na.rm = TRUE)
var(x, na.rm = TRUE)
quantile(x, probs = c(0.25, 0.5, 0.75))

# Custom mode function
getmode <- function(x) {
  freq <- table(x)
  names(freq)[which.max(freq)]
}

# Correlation matrix
cor(df[, c("col1", "col2", "col3")])
```

**Agricultural Example:**
```r
# Analyze yield data
yield_data <- read.csv("agri_dataset.csv")

# Quick overview
summary(yield_data)

# By treatment group
tapply(yield_data$Yield, yield_data$Treatment, mean)
tapply(yield_data$Yield, yield_data$Treatment, sd)
```

---

### **4️⃣ Visualization** (`04_Vizualization.qmd`)

**What You'll Learn:**
- Base R plotting functions
- ggplot2 grammar of graphics
- Common plots: scatter, line, box, bar
- Layering and customization
- Time series visualization

**Base R Plotting:**

```r
# Scatter plot
plot(x, y, main = "Title", xlab = "X", ylab = "Y", 
     col = "blue", pch = 16)

# Line plot
plot(x, y, type = "l", col = "red", lwd = 2)

# Overlaying multiple series
plot(x, y1, type = "l", col = "blue")
lines(x, y2, col = "red")
legend("topright", c("Series 1", "Series 2"), 
       col = c("blue", "red"), lty = 1)

# Bar plot
barplot(table(data$category), col = "steelblue")

# Box plot
boxplot(Value ~ Group, data = df, col = "lightblue")
```

**ggplot2 Approach:**

```r
library(ggplot2)

# Basic structure
ggplot(data, aes(x = var1, y = var2)) +
  geom_point() +
  geom_smooth(method = "lm", se = TRUE) +
  theme_classic() +
  labs(title = "Main Title", 
       x = "X Label", 
       y = "Y Label")

# Multiple geometries
ggplot(data, aes(x = Treatment, y = Yield, fill = Treatment)) +
  geom_boxplot() +
  geom_jitter(width = 0.2, alpha = 0.5) +
  facet_wrap(~ Region) +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Time series
data$Date <- as.Date(data$Date)
ggplot(data, aes(x = Date, y = Value, color = Region)) +
  geom_line() +
  geom_point() +
  facet_wrap(~ Region) +
  theme_classic()
```

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

**Hypothesis Testing Workflow:**

```r
# 1. Check assumptions
library(car)
shapiro.test(data$yield)      # Normality (p > 0.05 = normal)
leveneTest(yield ~ group)     # Homogeneity (p > 0.05 = equal variances)

# 2. Perform test
result <- t.test(group1, group2, var.equal = TRUE)
result <- aov(value ~ group, data = data)

# 3. Interpret results
summary(result)                # Get p-value and statistics
```

**t-Test Example:**
```r
# Compare fertilizer types A vs B
fert_A <- c(45, 48, 42, 50, 46)
fert_B <- c(52, 55, 50, 58, 54)

t.test(fert_A, fert_B, var.equal = TRUE)
# p-value < 0.05 → significant difference

# Using formula notation
t.test(Yield ~ Fertilizer, data = data, var.equal = TRUE)
```

**One-Way ANOVA Example:**
```r
# Compare 3 fertilizer types
model <- aov(Yield ~ Treatment, data = data)
summary(model)

# If p < 0.05, treatments significantly different
# Post-hoc test needed to identify which pairs differ
```

**Data Wrangling with dplyr:**
```r
library(dplyr)

data %>%
  filter(Region == "North") %>%
  group_by(Treatment) %>%
  summarise(
    mean_yield = mean(Yield),
    sd_yield = sd(Yield),
    n = n(),
    se_yield = sd_yield / sqrt(n)
  ) %>%
  arrange(desc(mean_yield))
```

---

## 🗂️ Working with `agri_dataset.csv`

Sample agricultural dataset included:
- Variables: Treatment, Yield, Region (sample)
- Use for practicing all Week 1 concepts
- ~10 observations (expandable for practice)

```r
# Load and explore
data <- read.csv("agri_dataset.csv")
head(data)
summary(data)

# Practice t-test
t.test(Yield ~ Treatment, data = data)

# Practice visualization
ggplot(data, aes(x = Treatment, y = Yield)) +
  geom_boxplot(fill = "lightblue") +
  geom_jitter(width = 0.2)
```

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

## 📋 Checklist: Master Week 1

- [ ] Create and manipulate vectors
- [ ] Understand data frames and subsetting
- [ ] Write and run custom functions
- [ ] Use if/else and loops correctly
- [ ] Detect and handle missing data
- [ ] Calculate descriptive statistics
- [ ] Create visualizations with base R
- [ ] Create visualizations with ggplot2
- [ ] Conduct t-tests and ANOVA
- [ ] Use dplyr for data manipulation

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

## 📚 Additional Resources

- **R for Data Science** by Hadley Wickham
- [ggplot2 Documentation](https://ggplot2.tidyverse.org/)
- [dplyr Cheat Sheet](https://dplyr.tidyverse.org/)
- [R Graphics Cookbook](https://r-graphics.org/)
- [Statistical Rethinking](https://xcelab.net/rethinking/) - Understanding statistics deeply

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
