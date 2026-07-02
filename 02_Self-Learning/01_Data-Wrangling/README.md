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

# Select by pattern
data %>% select(starts_with("Y"))  # Yield columns
data %>% select(contains("temp"))   # Temperature columns
```

### 3. **mutate()** - Create/modify columns
```r
# Create new variable
data %>% mutate(Yield_per_ha = Yield * 10)

# Multiple mutations
data %>% mutate(
  Yield_scaled = scale(Yield),
  Treatment_group = case_when(
    Fertilizer %in% c("A", "B") ~ "Organic",
    TRUE ~ "Inorganic"
  )
)

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
    sd_yield = sd(Yield, na.rm = TRUE),
    n = n()
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

### **distinct()** - Remove duplicates
```r
# Unique treatments
data %>% distinct(Treatment)

# Unique combinations
data %>% distinct(Fertilizer, Region)
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

### **across()** - Apply to multiple columns
```r
# Scale all numeric columns
data %>%
  mutate(across(where(is.numeric), scale))

# Round specific columns
data %>%
  mutate(across(contains("Yield"), ~round(., 2)))
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

## 📊 Practical Example: Complete Workflow

### **Scenario:** Analyze fertilizer effects on crop yield by region

```r
library(dplyr)
library(ggplot2)

# Load data
data <- read.csv("fertilizer_yield_data.csv")

# 1. Clean and prepare
cleaned <- data %>%
  filter(!is.na(Yield)) %>%  # Remove missing
  mutate(
    Yield_kg_ha = Yield * 100,  # Convert units
    Treatment_type = case_when(
      Fertilizer %in% c("A", "B") ~ "Organic",
      TRUE ~ "Synthetic"
    )
  )

# 2. Create summary table
summary_table <- cleaned %>%
  group_by(Fertilizer, Region) %>%
  summarise(
    Count = n(),
    Mean = mean(Yield_kg_ha, na.rm = TRUE),
    SD = sd(Yield_kg_ha, na.rm = TRUE),
    SE = SD / sqrt(Count),
    CV = (SD / Mean) * 100,
    .groups = 'drop'
  ) %>%
  arrange(Region, desc(Mean))

# 3. Save for reporting
write.csv(summary_table, "summary_output.csv", row.names = FALSE)

# 4. Visualize
ggplot(summary_table, aes(x = Fertilizer, y = Mean, fill = Region)) +
  geom_col(position = "dodge") +
  geom_errorbar(aes(ymin = Mean - SE, ymax = Mean + SE),
                width = 0.2, position = position_dodge(0.9)) +
  theme_minimal() +
  labs(title = "Mean Yield by Fertilizer and Region",
       y = "Yield (kg/ha)", x = "Fertilizer Type")
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

## 🎓 Exercises

**Dataset:** `fertilizer_yield_data.csv`

1. **Filter:** Select only fertilizer A treatments with Yield > 50
2. **Select:** Keep only Fertilizer, Region, and Yield columns
3. **Mutate:** Create new column for Yield category (Low/Medium/High)
4. **Group & Summarise:** Mean and SD yield by fertilizer type
5. **Chain:** Complete workflow with filter → mutate → group → summarise

---

## 📚 Resources

- [dplyr official documentation](https://dplyr.tidyverse.org/)
- [R for Data Science - Data Transformation Chapter](https://r4ds.had.co.nz/transform.html)
- [dplyr cheat sheet](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf)

---

## Next Steps

After mastering dplyr:
1. Move to **02_ggplot/** for visualizing your transformed data
2. Learn **pivot_wider/pivot_longer** for reshaping
3. Combine with **ggplot2** for exploratory data analysis
4. Use summaries as input for **statistical tests** (Week 3-4)

---

**Last Updated:** July 2, 2026
