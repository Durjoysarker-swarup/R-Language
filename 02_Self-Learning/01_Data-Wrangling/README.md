# Data Wrangling with dplyr

**Focus:** Master data transformation using dplyr pipelines for reproducible research workflows

---

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Use pipe operators (`%>%`) for readable data workflows
- ✅ Master the 5 core dplyr verbs: filter, select, mutate, group_by, summarise
- ✅ Create grouped summaries and aggregations
- ✅ Build publication-ready summary tables
- ✅ Handle complex transformations with multiple operations

---

## 📚 What's Inside

### Files
- `Wrangling_dplyr.qmd` - Complete hands-on tutorial with fertilizer data
- `fertilizer_yield_data.csv` - Multi-treatment dataset (Fertilizer × Crop × Yield)
- `Summary table.csv` - Example output showing expected results

---

## 🚀 The 5 Core Verbs

### 1. **filter()** - Select rows
```r
library(dplyr)

# Select fertilizer treatment A only
data %>% filter(Fertilizer == "A")

# Multiple conditions
data %>% filter(Yield > 50, Region == "North")

# Negation
data %>% filter(!is.na(Yield))
```

### 2. **select()** - Choose columns
```r
# Keep specific columns
data %>% select(Treatment, Yield, Region)

# Drop columns
data %>% select(-SoilType)

```

### 3. **mutate()** - Create/modify columns
```r
# Create new variable
data %>% mutate(Yield_per_ha = Yield * 10)

# Multiple mutations
data %>% mutate(
  Yield_scaled = scale(Yield),
  Yield_per_ha = Yield * 10)

# Conditional mutations
data %>% mutate(
  Quality = ifelse(Yield > 60, "High", "Low")
)
```

### 4. **group_by()** - Group rows
```r
# Group by single variable
data %>% group_by(Treatment)

# Multiple grouping variables
data %>% group_by(Treatment, Region)
```

### 5. **summarise()** - Aggregate data
```r
# Basic aggregation
data %>%
  group_by(Fertilizer) %>%
  summarise(
    mean_yield = mean(Yield, na.rm = TRUE),
    sd_yield = sd(Yield, na.rm = TRUE)
  )

# Multiple summary statistics
data %>%
  group_by(Treatment, Region) %>%
  summarise(
    count = n(),
    mean = mean(Yield),
    median = median(Yield),
    min = min(Yield),
    max = max(Yield),
    cv = (sd(Yield) / mean(Yield)) * 100,
    .groups = 'drop'
  )
```

---

## 🔗 The Pipe Operator: `%>%`

The pipe takes the output of one function and passes it as the first argument to the next.

### Without pipes (nested, hard to read):
```r
summarize(
  group_by(
    filter(data, Yield > 50),
    Treatment
  ),
  mean_yield = mean(Yield)
)
```

### With pipes (readable, left-to-right):
```r
data %>%
  filter(Yield > 50) %>%
  group_by(Treatment) %>%
  summarise(mean_yield = mean(Yield))
```

**Much clearer!**

---

## 💡 Advanced Techniques

### **arrange()** - Sort rows
```r
# Ascending (default)
data %>% arrange(Yield)

# Descending
data %>% arrange(desc(Yield))

# Multiple sort levels
data %>% arrange(Treatment, desc(Yield))
```


### **case_when()** - Conditional assignment (cleaner than nested ifelse)
```r
data %>% mutate(
  Yield_category = case_when(
    Yield < 40 ~ "Low",
    Yield < 60 ~ "Medium",
    Yield < 80 ~ "High",
    TRUE ~ "Very High"
  )
)
```

### **pivot_wider()** & **pivot_longer()** - Reshape data
```r
# Wide format (for regression)
data %>%
  pivot_wider(
    names_from = Fertilizer,
    values_from = Yield
  )

# Long format (for plotting)
data %>%
  pivot_longer(
    cols = starts_with("Week"),
    names_to = "Week",
    values_to = "Growth"
  )
```


---

## ✅ Common Mistakes to Avoid

1. **Forgetting `.groups = 'drop'`** in summarise after group_by
   - Leaves groups active, causing problems downstream

2. **Using `=` instead of `==` in filter()**
   - `filter(Treatment = "A")` ❌ (assignment)
   - `filter(Treatment == "A")` ✅ (comparison)

3. **Forgetting `na.rm = TRUE`** when NAs present
   - `mean(Yield)` returns NA if any missing values
   - `mean(Yield, na.rm = TRUE)` ✅

4. **Not saving output of pipe chain**
   - `data %>% filter(Yield > 50)` runs but discards result
   - `result <- data %>% filter(Yield > 50)` ✅

5. **Pipe chain too long without intermediate checks**
   - Break into steps to debug

---


## 📚 Resources

- [dplyr official documentation](https://dplyr.tidyverse.org/)
- [R for Data Science - Data Transformation Chapter](https://r4ds.had.co.nz/transform.html)
- [dplyr cheat sheet](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf)

---

## Next Steps

After mastering dplyr:
1. Move to **02_ggplot/** for visualizing your transformed data
3. Combine with **ggplot2** for exploratory data analysis

---

**Last Updated:** July 6, 2026
