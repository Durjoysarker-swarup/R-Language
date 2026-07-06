# Advanced Visualization with ggplot2

Create publication-quality plots using the grammar of graphics. Effective visualization is essential for both exploring data and communicating research findings to diverse audiences.

---

## 🎯 Learning Objectives

By the end of this module, you will:
- Understand the grammar of graphics principles
- Build plots layer-by-layer
- Create complex multi-variable visualizations
- Implement time series and faceted plots
- Customize themes and aesthetics for publications
- Choose appropriate plot types for different data

---

## 📚 What's Inside

### Files
- `Visualization.qmd` - Complete ggplot2 tutorial with examples
- `agriculture_sample_dataset.csv` - Multi-variable agricultural data
- `time_series_agriculture.csv` - Temporal crop growth data

---

## 📖 Core Concepts

### **Grammar of Graphics**
ggplot2 is built on the philosophy that plots have consistent components. Every visualization consists of:

1. **Data** - The dataset being visualized
2. **Aesthetics** - Visual properties (x, y, color, size, shape)
3. **Geometries** - How data is displayed (points, lines, bars, boxes)
4. **Scales** - How data maps to visual properties
5. **Facets** - How to split into multiple subplots
6. **Themes** - Overall visual design

Building plots layer-by-layer allows flexibility and professional control over visualization.

---

### **Essential Layers**

**Data & Aesthetics Mapping**
Specify which variables go on axes and how to encode other dimensions through color, size, shape.

**Geometric Objects**
Choose visualization type: scatter (points), line plot, bar chart, box plot, violin plot, histogram, etc.

**Statistical Layers**
Add computed summaries like trend lines, means, or confidence intervals.

**Faceting**
Split plot into multiple subplots by categorical variables for easy comparison.

**Scales**
Control how data values map to visual properties (colors, axis limits, legends).

**Themes**
Customize overall appearance including backgrounds, grid lines, text formatting.

---

## 📊 Common Plot Types

### **Scatter Plot**
Shows relationship between two continuous variables. Ideal for identifying correlations and patterns.

### **Line Plot**
Displays trends over time or continuous variables. Essential for time series and growth curves.

### **Box Plot**
Compares distributions across groups. Shows median, quartiles, and outliers for group comparison.

### **Bar Chart**
Compares values across categories. Grouped or stacked versions compare multiple factors.

### **Violin Plot**
Shows full distribution shape within groups. More informative than box plots alone.

### **Time Series**
Line plot with temporal x-axis. Ideal for crop growth, phenological data, or yield trends.

### **Faceted Plots**
Multiple subplots split by categorical variables for systematic comparison across regions, blocks, or treatments.

---

## 🎨 Customization

### **Color & Aesthetics**
- Manual color assignment for consistency
- Color-blind friendly palettes (viridis)
- Semantic color usage (red for bad, green for good)
- Consistency across figures

### **Themes**
- Minimal themes for clean publication-ready plots
- Classic themes with gray background
- Black & white themes
- Custom theme creation for organization branding

### **Labels & Legends**
- Descriptive axis labels with units
- Informative plot titles
- Clear legend titles
- Appropriate text sizing

### **Error Bars**
- Standard deviation showing spread
- Standard error for precision
- Confidence intervals for formal inference
- Consistent across multiple plots

---

## 📊 Agricultural Applications

### **Fertilizer Trials**
Compare yield across fertilizer types with error bars and grouped displays.

### **Variety Comparisons**
Show performance differences across crop varieties with error visualization.

### **Growth Curves**
Display plant development over time, potentially split by variety or region.

### **Treatment Interactions**
Visualize how treatments perform at different levels of another factor.

### **Regional Analysis**
Faceted plots comparing patterns across growing regions or environmental conditions.

---

## 📈 Learning Path

### Beginner
- Basic scatter plots and line plots
- Simple color mapping
- Axis labels and titles

### Intermediate
- Multiple geometries in one plot
- Faceting for group comparison
- Error bar addition
- Theme customization

### Advanced
- Complex multi-variable visualizations
- Statistical layers (trend lines, confidence bands)
- Interactive layering
- Custom theme development

---



## 🎯 Exercises

See `Visualization.qmd` for hands-on exercises using included agricultural datasets.

---

## Next Steps

After mastering ggplot2 visualization:
1. Apply to exploratory data analysis before formal testing
2. Create plots for statistical test results (Week 3-4)
3. Develop consistent visualization style
4. Integrate with dplyr for data preparation
5. Create professional publication figures

---

**Last Updated:** July 6, 2026

---

> **Tip:** Start with the basic plot types, then layer additional components. The modular nature of ggplot2 allows building complexity step-by-step.
