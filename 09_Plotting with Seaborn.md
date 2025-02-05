# 9. Plotting with Seaborn 

## 9.1. Introduction to Seaborn.  

Seaborn is a powerful statistical data visualization library built on top of Matplotlib, offering a high-level interface for creating attractive and informative statistical graphics. 

We'll explore how Seaborn enhances Matplotlib's capabilities and why it's particularly valuable for data analysis.

## 9.2. How is Seaborn related to Matplotlib?

Seaborn works as a wrapper around Matplotlib, providing:

- Attractive default styles
- High-level functions for common statistical plots
- Built-in themes for professional-looking visualizations
- Integrated support for pandas DataFrames

> [!NOTE]
> A wrapper is like a layer that "wraps around" existing code to make it **easier to use or give it additional functionality**. In this case, matplotlib is the base code and seaborn is the wrapper by making it simpler to use and styling

## 9.3. Core concepts of Seaborn

As usual, we will normally set up like this

```
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

# Common convention
sns.set_theme()  # Set default theme
```

Similar to Matplotlib, a figure is the overall window or page, while axes are individual plots within the figure.

And to plot a graph, we can do this

```
# Creating a figure and axes
fig, ax = plt.subplots(figsize=(10, 6))

patient_data = pd.DataFrame({
    'Age': range(20, 80),
    'Blood_Pressure': range(100, 160)
})
sns.scatterplot(data=patient_data, x='Age', y='Blood_Pressure', ax=ax)
```

## 9.4. Basic plot types

**(a) Relational plots**

Relational plots show the relationship between two or more variables.

```
# Patient age vs. blood pressure
age = np.random.normal(60, 15, 100)
bp = age * 2 + np.random.normal(0, 10, 100)
df = pd.DataFrame({'Age': age, 'Blood_Pressure': bp})

sns.scatterplot(data=df, x='Age', y='Blood_Pressure')
plt.title('Age vs. Blood Pressure')
```

**(b) Distribution plots**

Distribution plots help understand the spread and shape of data.

```
# Distribution of cholesterol levels
cholesterol = np.random.normal(200, 30, 1000)
sns.histplot(cholesterol, kde=True)
plt.title('Distribution of Cholesterol Levels')
```

> [!NOTE]
> KDE (Kernel density estimation) is a smoothed version of a histogram. It creates a continuous line that shows the shape of your data's distribution.
> Try your code above with and without kde (i.e. kde = True or kde = False)

**(c) Categorical plots**

```
# Treatment response by group
treatments = ['Drug A', 'Drug B']
response = [np.random.normal(5, 1, 100),
           np.random.normal(7, 1.5, 100),
           ]

# Create a dataframe
df = pd.DataFrame({
    'Treatment': np.repeat(treatments, 100),
    'Response': np.concatenate(response)
})

print(df)

#Plot
sns.boxplot(data=df, x='Treatment', y='Response')
```

**(d) Regression plots**

Regression plots help visualize statistical relationships and trends.

```
# Create simple data
BMI = [22, 25, 28, 30, 33, 35, 27, 24, 29, 31]      
Glucose = [85, 92, 98, 105, 110, 115, 95, 88, 100, 108]

# Create DataFrame
df = pd.DataFrame({'BMI': BMI, 'Glucose': Glucose})  

# Create plot
sns.regplot(data=df, x='BMI', y='Glucose')         
plt.title('BMI vs. Blood Glucose Levels')
plt.show()
```

**(c) Matrix plots**

Matrix plots are excellent for visualizing correlations and patterns in multivariate data.

```
# Correlation matrix of vital signs
vital_signs = pd.DataFrame(np.random.randn(100, 4),
                          columns=['BP', 'HR', 'Temp', 'O2'])
sns.heatmap(vital_signs.corr(), annot=True, cmap='coolwarm')
```
