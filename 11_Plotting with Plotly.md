# 11. Plotting with Plotly

Plotly is a Python library for creating interactive, web-based visualizations. The library excels at creating interactive dashboards and web-ready visualizations, making it particularly useful for data exploration and sharing results.

# 11.1. Setup

Let's first set up all the necessary libraries

```
import plotly.express as px
import plotly.graph_objects as go
import numpy as np
```

and generate the dataset that we will need 

```
# Sample patient data
patient_ids = list(range(1, 11))
glucose_levels = [95, 105, 88, 92, 130, 135, 87, 89, 115, 125]
bmi_values = [24, 26, 22, 28, 32, 30, 25, 23, 27, 29]
cholesterol = [180, 210, 170, 190, 240, 230, 175, 185, 200, 220]
age = [45, 52, 38, 41, 60, 55, 42, 39, 48, 50]
```

# 11.2. Basic plot types 

**(a) Scatter plots**

Scatter plots are fundamental for visualizing relationships between variables and tracking trends over time.

```
# Scatter plot
fig = px.scatter(x=bmi_values, y=glucose_levels, 
                 labels={'x': 'BMI', 'y': 'Glucose Levels'},
                 title='BMI vs Glucose Levels')
fig.show()
```


**(b) Line charts**

Line charts are equally useful to show relationships between variables. 

```
fig = px.line(x=patient_ids, y=glucose_levels,
              labels={'x': 'Patient ID', 'y': 'Glucose Levels'},
              title='Glucose Levels Trend')
fig.show()
```

**(c) Bar charts**

Bar charts compare categorical data. 

```
fig = px.bar(x=patient_ids, y=glucose_levels,
             labels={'x': 'Patient ID', 'y': 'Glucose Levels'},
             title='Glucose Levels by Patient')
fig.show()
```

**(d) Histograms**

Histograms show the distribution of continuous variables.

```
fig = px.histogram(x=glucose_levels,
                  labels={'x': 'Glucose Levels'},
                  title='Distribution of Glucose Levels')
fig.show()
```

**(e) Boxplots**

Box plots is a tool for visualizing data distribution. It is more traditional and straightforward, showing key statistical measures like the median, quartiles, and outliers through a compact rectangular box with whiskers. 

```
fig = px.box(y=glucose_levels,
             title='Glucose Levels Distribution')
fig.show()
```

**(f) Violin plots**

Violin plots offer a more comprehensive view of the data distribution by showing the full shape of the data, similar to a smoothed histogram that's been mirrored. While they take up more visual space, violin plots are superior at revealing features like multiple peaks (multimodal distributions) and subtle changes in data density that box plots might miss.

```
fig = px.violin(y=glucose_levels,
                title='Glucose Levels Density Distribution')
fig.show()
```

# 11.3. Interactive features 

The benefit of using Plotly is its interactivity. Here are some examples of interaction that you can with Plotly. 

**(a) Hover Tooltips and Click Events**

```
# Scatter plot with hover data
fig = px.scatter(x=bmi_values, y=glucose_levels,
                 labels={'x': 'BMI', 'y': 'Glucose Levels'},
                 title='BMI vs Glucose Levels',
                 hover_data=[age, cholesterol])
fig.show()
```

**(b) Range Selectors and Sliders**

```
# Line chart with range slider
fig = go.Figure()
fig.add_trace(go.Scatter(x=patient_ids, y=glucose_levels,
                        name='Glucose Levels'))
fig.update_layout(
    title='Glucose Levels with Range Slider',
    xaxis=dict(rangeslider=dict(visible=True))
)
fig.show()
```


