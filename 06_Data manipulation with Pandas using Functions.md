## Data manipulation with Functions

Finally, we can use three important Pandas functions to create new columns. `apply()`, `map()`, and `applymap()` are powerful pandas methods that let you transform data efficiently.

The main differences are:

- `apply()` works on entire rows/columns
- `map()` transforms individual values in a Series
- `applymap()` transforms every single element in a DataFrame

This is much cleaner than using loops and more performant since pandas optimizes these operations under the hood. Let's see how we can apply these in a healtcare dataset. 

(a) Using `apply()`
This method is used to apply functions to rows or columns of a dataframe. It can handle complex operations that need multiple rows columns (axis = 0) and rows (axis = 1)

```
# Simple example dataset
patient_data = pd.DataFrame({
    'name': ['John', 'Sarah', 'Mike'],
    'systolic': [120, 160, 130],
    'diastolic': [80, 95, 85]
})

# Simple apply() on a single column
# Convert systolic to risk category
def blood_pressure_category(value):
    if value < 120:
        return 'Normal'
    elif value < 140:
        return 'Elevated'
    else:
        return 'High'

patient_data['bp_category'] = patient_data['systolic'].apply(blood_pressure_category)
```

You can also create `apply()` with data from multiple columns

```
# apply() with multiple columns (row-wise operation)
def calculate_bp_status(row):
    if row['systolic'] >= 140 or row['diastolic'] >= 90:
        return 'Hypertensive'
    return 'Normal'

patient_data['status'] = patient_data.apply(calculate_bp_status, axis=1)
```

(b) Using `map()`

This method can be used for simple element-wise transformations. 

```
# Simple mapping of codes to descriptions
diagnosis_codes = {
    'A1': 'Diabetes',
    'B2': 'Hypertension',
    'C3': 'Asthma'
}

patient_data = pd.DataFrame({
    'name': ['John', 'Sarah', 'Mike'],
    'diagnosis_code': ['A1', 'B2', 'C3']
})

# Map codes to full names
patient_data['diagnosis'] = patient_data['diagnosis_code'].map(diagnosis_codes)
```

(c) Using `applymap()`

This method applies a function to every individual element in the dataframe. 

```
# Example with numeric data
vitals_data = pd.DataFrame({
    'temperature': [98.6, 99.2, 98.4],
    'heart_rate': [72.1, 68.7, 75.3],
    'spo2': [98.0, 97.5, 99.0]
})

# Round all numbers to 1 decimal place
vitals_rounded = vitals_data.applymap(lambda x: round(x, 1))
```

