# 10_More on Seaborn 

Let's learn more on what seaborn can do.

For all our examples, we'll use a simple medical dataset with 10 patients, recording their age (years) and systolic blood pressure (mmHg). This will help us understand how different visualizations can be applied in medical contexts.

## 10.1. Setup
Let's set up seaborn

```
import seaborn as sns
import pandas as pd
import numpy as np
```

Let's generate the dataset

```
# Simple medical dataset
age = [25, 30, 35, 40, 45, 50, 55, 60, 65, 70]
blood_pressure = [115, 118, 125, 130, 135, 138, 142, 145, 150, 155]
data = pd.DataFrame({'Age': age, 'Blood_Pressure': blood_pressure})
```

## 10.2. Working with colour palettes

Color palettes in data visualization are crucial for effectively communicating patterns and relationships in medical data while maintaining accessibility for all viewers.

```
# Sequential palette (good for continuous data)
sns.scatterplot(data=data, x='Age', y='Blood_Pressure', hue='Age', palette='Blues')

# Diverging palette (good for data with a meaningful midpoint)
sns.scatterplot(data=data, x='Age', y='Blood_Pressure', hue='Age', palette='RdBu')

# Qualitative palette (good for categorical data)
sns.scatterplot(data=data, x='Age', y='Blood_Pressure', hue='Age', palette='Set2')
```

> [!NOTE]
> `hue` determines what to colour by (the variable that will be used for colouring)
> `palette' determinw how to colour (what colours to use) 

## 10.3. Setting themes

Themes provide consistent styling across all visualizations in your analysis, ensuring professional and readable outputs.

```
# Setting different built-in themes
sns.set_theme(style="whitegrid")  # Clean, professional look
sns.set_theme(style="darkgrid")   # Good for presentations
sns.set_theme(style="ticks")      # Minimal, publication-ready
```

## 10.4. Customizing elements

You can also fine tune each individual plot elements allows for precise control over your visualization's appearance.

```
# Comprehensive plot customization
plt.figure(figsize=(10, 6))
sns.scatterplot(data=data, x='Age', y='Blood_Pressure')
plt.title('Blood Pressure vs. Age', fontsize=14, pad=15)
plt.xlabel('Age (years)', fontsize=12)
plt.ylabel('Systolic Blood Pressure (mmHg)', fontsize=12)
plt.grid(True, linestyle='--', alpha=0.7)
```
