# Advanced Visualization with ggplot2

**Focus:** Create publication-quality plots using the grammar of graphics

---

## 🎯 Learning Objectives

By the end of this module, you will:
- ✅ Understand the grammar of graphics principles
- ✅ Build plots layer-by-layer
- ✅ Create complex multi-variable visualizations
- ✅ Implement time series and faceted plots
- ✅ Customize themes and aesthetics for publications

---

## 📚 What's Inside

### Files
- `Visualization.qmd` - Complete ggplot2 tutorial with examples
- `agriculture_sample_dataset.csv` - Multi-variable agricultural data
- `time_series_agriculture.csv` - Temporal crop growth data

---

## 🏗️ Grammar of Graphics

Every ggplot2 plot has these components:

```
ggplot(data, aes(x, y)) +      # Data + Aesthetics
  geom_point() +               # Geometric layer
  facet_wrap(~Region) +        # Faceting
  scale_color_manual(...) +    # Scales
  theme_classic()              # Theme
```

### **Essential Layers**

1. **Data & Aesthetics** - `aes()`
```r
ggplot(data, aes(
  x = Treatment,
  y = Yield,
  color = Region,     # Color by region
  size = PlantHeight, # Size by height
  shape = Variety     # Shape by variety
))
```

2. **Geometric Objects** - `geom_*()`
```r
geom_point()      # Scatter plot
geom_line()       # Line plot
geom_boxplot()    # Box plot
geom_bar()        # Bar chart
geom_violin()     # Violin plot
geom_jitter()     # Jittered points
geom_smooth()     # Trend line
geom_histogram()  # Histogram
```

3. **Faceting** - `facet_*()`
```r
facet_wrap(~Region)           # Wrap by one variable
facet_grid(Treatment~Region)   # Grid by two variables
```

4. **Scales** - `scale_*()`
```r
scale_color_manual(values = c("A" = "red", "B" = "blue"))
scale_y_continuous(limits = c(0, 100))
scale_x_date(date_labels = "%Y-%m")
```

5. **Themes** - `theme_*()`
```r
theme_classic()      # Minimal background
theme_minimal()      # Even cleaner
theme_bw()           # Black & white
theme_dark()         # Dark background
```

---

## 📊 Common Plot Types

### **1. Scatter Plot**
```r
ggplot(data, aes(x = Temperature, y = Yield)) +
  geom_point(size = 3, alpha = 0.6) +
  geom_smooth(method = "lm", se = TRUE) +
  theme_classic() +
  labs(title = "Yield vs Temperature",
       x = "Temperature (°C)", y = "Yield (kg/ha)")
```

### **2. Line Plot (Time Series)**
```r
data$Date <- as.Date(data$Date)

ggplot(data, aes(x = Date, y = PlantHeight, color = Variety)) +
  geom_line(size = 1) +
  geom_point(size = 2) +
  facet_wrap(~Region) +
  theme_classic() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  labs(title = "Plant Growth Over Time",
       x = "Date", y = "Height (cm)")
```

### **3. Box Plot (Comparison)**
```r
ggplot(data, aes(x = Fertilizer, y = Yield, fill = Fertilizer)) +
  geom_boxplot(alpha = 0.7) +
  geom_jitter(width = 0.2, alpha = 0.3) +
  theme_classic() +
  labs(title = "Yield Distribution by Fertilizer",
       x = "Fertilizer Type", y = "Yield (kg/ha)")
```

### **4. Bar Plot (Grouped)**
```r
ggplot(data, aes(x = Fertilizer, y = Yield, fill = Region)) +
  geom_col(position = "dodge") +
  geom_errorbar(aes(ymin = Yield - SE, ymax = Yield + SE),
                width = 0.2, position = position_dodge(0.9)) +
  theme_classic() +
  labs(title = "Mean Yield by Fertilizer and Region",
       x = "Fertilizer", y = "Yield (kg/ha)")
```

### **5. Violin Plot (Distribution)**
```r
ggplot(data, aes(x = Treatment, y = Yield, fill = Treatment)) +
  geom_violin(alpha = 0.6) +
  geom_boxplot(width = 0.2, alpha = 0.8) +
  theme_minimal() +
  labs(title = "Yield Distribution by Treatment")
```

### **6. Faceted Plots (Comparison)**
```r
ggplot(data, aes(x = Dose, y = Response, color = Variety)) +
  geom_line() +
  geom_point() +
  facet_wrap(~Region, scales = "free_y") +
  theme_classic() +
  labs(title = "Dose-Response Curves by Region")
```

---

## 🎨 Customization

### **Colors**
```r
# Manual colors
scale_color_manual(values = c("A" = "#E69F00", "B" = "#56B4E9"))

# Palettes
scale_color_brewer(palette = "Set1")
scale_color_viridis_d()  # Colorblind-friendly
```

### **Themes**
```r
# Full customization
theme(
  plot.title = element_text(size = 14, face = "bold", hjust = 0.5),
  axis.title = element_text(size = 12, face = "bold"),
  axis.text = element_text(size = 10),
  legend.position = "bottom",
  panel.background = element_blank(),
  panel.grid.major = element_line(color = "gray90")
)
```

### **Labels & Titles**
```r
labs(
  title = "Main Title",
  subtitle = "Subtitle",
  caption = "Source: Field data 2024",
  x = "X Axis Label",
  y = "Y Axis Label",
  color = "Legend Title",
  fill = "Another Legend"
)
```

---

## 📈 Real Agricultural Examples

### **Example 1: Fertilizer Trial Summary**
```r
library(dplyr)
library(ggplot2)

summary <- data %>%
  group_by(Fertilizer, Region) %>%
  summarise(
    mean_yield = mean(Yield),
    se_yield = sd(Yield) / sqrt(n()),
    .groups = 'drop'
  )

ggplot(summary, aes(x = Fertilizer, y = mean_yield, fill = Region)) +
  geom_col(position = "dodge") +
  geom_errorbar(aes(ymin = mean_yield - se_yield,
                    ymax = mean_yield + se_yield),
                width = 0.2, position = position_dodge(0.9)) +
  scale_y_continuous(expand = expansion(mult = c(0, 0.1))) +
  theme_classic() +
  theme(legend.position = "top") +
  labs(title = "Crop Yield by Fertilizer Type",
       y = "Mean Yield (kg/ha)", x = "Fertilizer")
```

### **Example 2: Growth Curve Over Time**
```r
data$Date <- as.Date(data$Date)

ggplot(data, aes(x = Date, y = PlantHeight, color = Variety)) +
  geom_line(size = 1) +
  geom_smooth(method = "loess", se = TRUE, alpha = 0.2) +
  facet_wrap(~Region, scales = "free_y") +
  theme_classic() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  labs(title = "Plant Growth Trajectories",
       x = "Date", y = "Plant Height (cm)",
       color = "Variety")
```

### **Example 3: Treatment Comparison**
```r
ggplot(data, aes(x = Treatment, y = Yield, fill = Treatment)) +
  geom_boxplot(alpha = 0.7, outlier.shape = NA) +
  geom_jitter(width = 0.2, alpha = 0.4, size = 2) +
  stat_summary(fun = mean, geom = "point", size = 3, color = "red",
               aes(shape = "Mean")) +
  facet_wrap(~Block) +
  theme_minimal() +
  theme(
    legend.position = "bottom",
    plot.title = element_text(size = 14, face = "bold", hjust = 0.5)
  ) +
  labs(title = "Yield by Treatment Across Blocks",
       y = "Yield (kg/ha)", x = "Treatment")
```

---

## ✅ Best Practices for Publication

1. **Clear Titles & Labels**
   - Title should be informative, not just "Figure 1"
   - Units must be included (e.g., "Yield (kg/ha)")
   - Axis labels should be complete sentences

2. **Include Error Bars**
   - Show variability (SD, SE, or CI)
   - Critical for research plots

3. **Choose Appropriate Plots**
   - Scatter plot for relationships
   - Box plot for distributions and comparisons
   - Line plot for time series
   - Bar plot for group comparisons

4. **Use Colorblind-Friendly Palettes**
   ```r
   scale_color_viridis_d()  # Works for all color blindness types
   ```

5. **Consistent Themes**
   ```r
   theme_set(theme_classic())  # Apply to all plots
   ```

6. **Save in Vector Format**
   ```r
   ggsave("figure.pdf", width = 8, height = 6, dpi = 300)
   ```

---

## 🎓 Exercises

**Using provided datasets:**

1. Create a scatter plot of Temperature vs Yield with trend line
2. Make a time series plot of plant growth over days
3. Compare yield distributions across treatments with box plots
4. Create faceted plots by region
5. Customize colors, themes, and labels for publication

---

## 📚 Resources

- [ggplot2 official website](https://ggplot2.tidyverse.org/)
- [ggplot2 book online](https://ggplot2-book.org/)
- [R Graphics Cookbook](https://r-graphics.org/)
- [Color palettes for ggplot2](https://r-graph-gallery.com/ggplot2-color.html)

---

## Next Steps

1. Master faceting for complex comparisons
2. Learn statistical summaries within plots
3. Create custom themes for your organization
4. Use plots for exploratory data analysis (Week 1 → Week 2)
5. Apply to visualize statistical test results (Week 3-4)

---

**Last Updated:** July 2, 2026
