# 8 More on Matplotlib

## 8.1. Creating multi-panel figures in Python 

In data visualization, creating multiple panels allows us to compare different aspects of our data side by side, making it easier to spot patterns and relationships.

```
import matplotlib.pyplot as plt
import numpy as np

# Creating the figures
fig = plt.figure(figsize=(10, 4))
ax1 = fig.add_subplot(1, 2, 1) # axes 1
ax2 = fig.add_subplot(1, 2, 2) # axes 2

# Generate sample data
x = np.linspace(0, 10, 100)
y1 = np.sin(x)
y2 = np.cos(x)

# Plot in each subplot
ax1.plot(x, y1)
ax2.plot(x, y2)
plt.show()
```

## 8.2. Creating multi-panel figures in Python 

```
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(1, 1, 1)

x = np.linspace(0, 10, 20)
y1 = 2 * x + 1
y2 = x ** 2

ax.plot(x, y1, 'b-', label='Linear')
ax.scatter(x, y2, color='red', label='Quadratic')
ax.legend()
```

> [!TIP]
> You can actually condense
> 
> ```
> fig = plt.figure(figsize=(8, 6))
> ax = fig.add_subplot(1, 1, 1)
> ```
>
> into
>
> ```
> fig, ax = plt.subplots(figsize=(8, 6))
>
> The reason you can do this is because of Python's tuple unpacking frature.
> `plt.subplots()` return two objects:
> - A figure object
> - An axes object
>
> You can check this effect out
>
> ```
> result = plt.subplots()
> fig = result[0]  # Get figure object
> ax = result[1]   # Get axes object
> ```
>
> This is similar as how you would unpack a tuple
>
> ```
> point = (10,20)
> x, y = point
> ``` 

## 8.3. Customizing figure elements

Proper customization of figure elements helps in creating clear, professional-looking visualizations that effectively communicate your data.
For example, 

```
import matplotlib.pyplot as plt
import numpy as np

# Create basic data
x = np.linspace(0, 10, 50)
y = np.sin(x)

# Create figure and axis objects
fig, ax = plt.subplots(figsize=(10, 6))

# Plot with various line customizations
ax.plot(x, y,
        color='blue',          # Color can be name, hex code, or RGB tuple
        linestyle='--',        # Line style: '-', '--', ':', '-.'
        linewidth=2,           # Width of the line
        marker='o',            # Marker style: 'o', 's', '^', 'v', '*', '+'
        markersize=8,          # Size of markers
        markerfacecolor='red', # Color inside markers
        markeredgecolor='black',# Color of marker edges
        markeredgewidth=1,     # Width of marker edges
        alpha=0.7)             # Transparency (0 to 1)

# Customize the rest of the plot
ax.set_title('Customized Line Plot', fontsize=14, fontweight='bold')
ax.set_xlabel('X-axis', fontsize=12)
ax.set_ylabel('Y-axis', fontsize=12)
ax.grid(True, linestyle='--', alpha=0.7)
ax.tick_params(axis='both', labelsize=10)

# Show plot
plt.show()
```

