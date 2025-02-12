## Data cleaning with Panda

In a machine learning pipeline, it is very common to do data cleaning. Data cleaning in machine learning is the process of preparing raw data for analysis by fixing or removing incorrect, incomplete, irrelevant, duplicated, or improperly formatted data. Examples of data cleaning tasks include handling missing values, removing duplicates, fixing data types, handling outliers, standardization/normalization and handling inconsistent data.
This process is crucial because of **garbage in garbage out**. Machine learning models are only as good as their training data.

**1. Handling missing data in datasets**

1.1 Identifying missing values 

Missing data in medical research can significantly impact analysis quality and patient outcomes. Common scenarios include missing lab results, incomplete patient data or unavailable genetic markets. These are often represented as *None*

```
import pandas as pd

# Example clinical dataset
clinical_data = pd.DataFrame({
    'patient_id': [1, 2, 3, 4, 5],
    'age': [45, 62, None, 51, 73],
    'blood_pressure': [120, None, 135, None, 142],
    'hba1c': [6.2, 7.1, None, 6.8, None]
})

clinical_data # visualize the dataframe

# Check missing values
print("Missing value check:")
print(clinical_data.isna())

# Count missing values per column
print("\nMissing value counts:")
print(clinical_data.isna().sum())

# Identify complete cases
complete_records = clinical_data.notna().all(axis=1)
print("\nComplete records:")
print(clinical_data[complete_records])
```

1.2 Handling missing data

We can handle missing data using two basic methods:

(a) Filling missing values with fillna()

When you have None values in a pandas Series/DataFrame, they get automatically converted to NaN (Not a Number) for numeric columns. This can cause type inconsistencies since NaN is a float type. Besides, mathematical operations with None or NaN values will typically return NaN, which can propagate through your calculations. Lastly, many pandas operations like groupby() automatically exclude None/NaN values, which might not be what you want.

Therefore, using fillna) gives you control on how to handle missing data based on your specific needs - you could:

i. Basic fillna()
- Fill with zeros: fillna(0)
- Fill with the mean: fillna(df['column'].mean())
- Fill with the last valid value: fillna(method='ffill')
- Fill with the next valid value: fillna(method='bfill')

> [!NOTE]  
> Forward fill (ffill)
> 
> ```
> import pandas as pd
> series = pd.Series([1, None, None, 4, None])
> 
> # ffill fills missing values with the last valid value
> print(series.fillna(method='ffill'))
> ```
>
> Backward fill (bfill)
>
> ```
> # bfill fills missing values with the next valid value
> print(series.fillna(method='bfill'))
> # Output: [1, 4, 4, 4, nan]  # last value remains nan since no value follows it
> ```


ii. Statistical fillna()
- Fill with mean: fillna(df.mean())  
- Fill with median: fillna(df.median()) 
- Fill with mode: fillna(df.mode()[0])  

Coming back to the example above, you could

```
# Fill with medically relevant values
clinical_data['hba1c'].fillna(clinical_data['hba1c'].mean(), inplace=True)

# Forward fill for time-series patient data
vital_signs = pd.DataFrame({
    'time': ['08:00', '09:00', '10:00', '11:00'],
    'heart_rate': [72, None, 75, None],
    'temperature': [98.6, None, None, 98.8]
})
vital_signs.fillna(method='ffill', inplace=True)
```

(b) Removing missing data (dropna())

You can use the dataset below to try out:

```
import pandas as pd
import numpy as np

patient_ids = ['P1', 'P2', 'P3', 'P4', 'P5', 'P6', 'P7', 'P8', 'P9', 'P10']
genetic_marker_1 = ['A', 'B', None, 'A', 'C', 'B', None, 'A', 'B', 'C']
genetic_marker_2 = ['X', None, 'Y', 'Z', 'X', 'Y', 'Z', None, 'X', 'Y']
blood_pressure = [120, 135, None, 142, 118, None, 125, 130, 145, 122]
cholesterol = [200, None, 220, 180, 190, 210, None, 195, 230, None]
glucose = [90, 85, 95, None, 88, 92, 98, None, 85, 90]

clinical_data = pd.DataFrame({
    'patient_id': patient_ids,
    'genetic_marker_1': genetic_marker_1,
    'genetic_marker_2': genetic_marker_2,
    'blood_pressure': blood_pressure,
    'cholesterol': cholesterol,
    'glucose': glucose
})

print("Original DataFrame:")
print(clinical_data)
```

To remove missing data, you can:

```
# Remove patients with missing genetic markers
genetic_data = clinical_data.dropna(subset=['genetic_marker_1', 'genetic_marker_2'])

# Remove records missing critical values
clean_data = clinical_data.dropna(thresh=4)  # Keep rows with at least 4 non-null values
```

**2. Value replacement and standardization**

2.1 Replacing values

We can standardize or replace errors in the datasets using `replace()`. 

```
# Standardize medication names
medications = pd.DataFrame({
    'prescribed_med': ['Metformin', 'METFORMIN', 'Met', 'metformin_hcl']
})
medications['prescribed_med'].replace({
    'METFORMIN': 'Metformin',
    'Met': 'Metformin',
    'metformin_hcl': 'Metformin'
}, inplace=True)

# Replace error codes in lab results
lab_results = pd.DataFrame({
    'test_result': ['-999', '1.2', '2.3', 'ERROR']
})
lab_results['test_result'].replace(['-999', 'ERROR'], pd.NA, inplace=True)
```

2.2 Removing duplicates

We can use the `drop_duplicates()` method to remove any repeated data.

```
# Remove duplicate patient records
patient_records = pd.DataFrame({
    'patient_id': [1, 1, 2, 3, 3],
    'visit_date': ['2024-01-01', '2024-01-01', '2024-01-02', '2024-01-03', '2024-01-03'],
    'diagnosis': ['T2D', 'T2D', 'HTN', 'CAD', 'CAD']
})
unique_records = patient_records.drop_duplicates()

# Keep most recent record per patient
latest_records = patient_records.sort_values('visit_date').drop_duplicates(
    subset='patient_id', 
    keep='last'
)
```

**3. String cleaning and standardization**

String cleaning and standardization is crucial for data quality and consistency because raw text data often contains variations in formatting, capitalization, whitespace, special characters, and spelling that can cause matching problems and incorrect analysis. For example, "DNA", "dna", and "DNA " (note the space) would be treated as different values without standardization, leading to incorrect grouping, filtering, or aggregation results. By cleaning and standardizing strings (removing extra spaces, normalizing case, fixing typos, standardizing formats), you ensure accurate analysis, better data matching, and more reliable insights from your data.

3.1 String cleaning methods

```
# Clean diagnosis text
diagnosis_data = pd.DataFrame({
    'diagnosis': [' Type 2 Diabetes ', 'HYPERTENSION', 'Coronary Artery Disease  ']
})

# Apply string cleaning
diagnosis_data['diagnosis'] = diagnosis_data['diagnosis'].str.strip()  # Remove whitespace
diagnosis_data['diagnosis'] = diagnosis_data['diagnosis'].str.title()  # Standardize capitalization
```

3.2 Data Type Conversion

Data type conversion in programming is crucial because it ensures data is stored and processed efficiently while maintaining accuracy. Incorrect data types can lead to bugs, performance issues, or unexpected behavior in your code, especially when working with databases or performing mathematical operations.

```
# Convert string values to appropriate types
patient_data = pd.DataFrame({
    'age': ['45', '62', '51'],
    'blood_glucose': ['120.5', '95.2', '110.8'],
    'is_diabetic': ['True', 'False', 'True']
})

# Convert to appropriate types
patient_data['age'] = patient_data['age'].astype(int)
patient_data['blood_glucose'] = patient_data['blood_glucose'].astype(float)
patient_data['is_diabetic'] = patient_data['is_diabetic'].astype(bool)
```
