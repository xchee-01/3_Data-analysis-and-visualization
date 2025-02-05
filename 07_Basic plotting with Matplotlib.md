# 7. Matplotlib

## 7.1. Matplotlib architecture and core concepts

The foundation of data visualization in Python lies in understanding Matplotlib's architecture. This section covers the hierarchical structure of Matplotlib and how different components work together to create visualizations.

## 7.2. Understanding Figure and Axes Objects
A Figure in Matplotlib serves as the top-level container that holds all plot elements, while Axes objects are the actual plotting areas where data is visualized. This relationship is fundamental to creating well-structured visualizations.

**Key Components**

- **Figure: The overall window or page that contains everything**
- **Axes: The actual plotting area with data, axis lines, labels, etc.**
- **Axis: The number-line-like objects that define plot boundaries**
- **Artist: Everything visible in the figure (lines, text, legends)**

<p align="center">
  <img width="690" height="450" src="https://miro.medium.com/v2/resize:fit:669/1*zxvxtqmcl9rFVj5yN4pNjA.png">
</p>
_Image adapted from [here](https://www.skytowner.com/explore/getting_started_with_matplotlib)_

```
# Basic Figure and Axes creation
import matplotlib.pyplot as plt

# Create a new figure
fig = plt.figure(figsize=(10, 6))

# Add an axes to the figure
ax = fig.add_subplot(111)
```

Here is an example of how you can plot medical data.

```
# Creating a figure for visualizing gene expression data
fig = plt.figure(figsize=(12, 6))    #What happens if you change these numbers?
ax = fig.add_subplot(111)

# Example gene expression data
gene_names = ['BRCA1', 'TP53', 'EGFR']
expression_levels = [45.2, 67.8, 23.4] #What happens if you change these numbers?

ax.bar(gene_names, expression_levels) #What happens if you change these?
ax.set_title('Gene Expression Levels in Tumor Sample') #What happens if you change these?
```

> [!NOTE]
> Instead of following the codes linearly, try playing around with the different parameters to get a sense of what each line of code does.

## 7.3. pyplot vs Object-Oriented Interface

Matplotlib offers two main approaches to creating visualizations: the pyplot interface (stateful, MATLAB-style) and the object-oriented interface (explicit, more flexible). Understanding both helps in choosing the right approach for different scenarios.

**(a) pyplot interface**

```
# pyplot interface example
plt.plot([1, 2, 3], [1, 2, 3])
plt.title('Simple Plot')
plt.xlabel('X axis')
plt.ylabel('Y axis')
```
**(b) Object-oriented interface**

```
# Object-oriented interface example
fig, ax = plt.subplots()
ax.plot([1, 2, 3], [1, 2, 3])
ax.set_title('Simple Plot')
ax.set_xlabel('X axis')
ax.set_ylabel('Y axis')
```

## 7.4. Creating your first plots

Let's see how we can set up your environment and creating basic visualizations. We'll explore common plotting methods and how to save your work.

**Setting up the development environment**

Before creating visualizations, you need to set up your Python environment with the necessary libraries. Here's a standard setup. We will normally put in this line of code before we start plotting 

```
import matplotlib.pyplot as plt
import numpy as np
```

**(a) Line Plots**

Here is a simple line plot

```
# Simple line plot
x = np.linspace(0, 10, 100)
y = np.sin(x)
plt.plot(x, y)
plt.title('Simple Sine Wave')
```

and you can see how this is applied in a medical context

```
# Patient temperature monitoring over time
times = np.arange(0, 24, 0.5)  # 24 hours with readings every 30 min
temperature = 37 + np.sin(times/24 * 2*np.pi) + np.random.normal(0, 0.1, len(times))

plt.plot(times, temperature)
plt.axhline(y=37, color='r', linestyle='--', label='Normal Temperature')
plt.title('Patient Temperature Monitoring')
plt.xlabel('Time (hours)')
plt.ylabel('Temperature (°C)')
plt.legend()
```

**(b) Line Plots**

```
# Basic scatter plot
x = np.random.rand(50)
y = np.random.rand(50)
plt.scatter(x, y)
```

and you can see how this is applied in a medical context

```
# Gene expression correlation
gene1_expression = np.random.normal(10, 2, 30)
gene2_expression = gene1_expression * 0.5 + np.random.normal(0, 1, 30)

plt.scatter(gene1_expression, gene2_expression)
plt.xlabel('Gene A Expression')
plt.ylabel('Gene B Expression')
plt.title('Gene Co-expression Analysis')
```

**(c) Bar Plots**

```
# Simple bar plot
categories = ['A', 'B', 'C']
values = [4, 3, 2]
plt.bar(categories, values)
```

and you can see how this is applied in a medical context

```
# Drug efficacy comparison
drugs = ['Drug A', 'Drug B', 'Control']
efficacy = [75, 62, 23]

plt.bar(drugs, efficacy)
plt.ylabel('Efficacy (%)')
plt.title('Drug Treatment Efficacy Comparison')
```

**Saving figures**

Finally, if you want to save the figures, you can use the code below:

```
# Save in different formats
plt.savefig('plot.png', dpi=300, bbox_inches='tight')  # For web/screen
plt.savefig('plot.pdf', bbox_inches='tight')  # For publications
plt.savefig('plot.svg', bbox_inches='tight')  # For vector graphics
```
