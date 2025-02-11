## Data visualization with Panda
Pandas is a powerful data visualization, manipulation and analysis library for Python. You can visualize your data in table form using dataframe and series. 

DataFrame: A two-dimensional table-like structure with labeled rows and columns. Think of it as a spreadsheet or SQL table in Python. It can hold different types of data (numbers, text, dates, etc.) and allows for powerful operations across rows and columns.

Series: A one-dimensional labeled array that can hold data of any type. You can think of it as a single column from a DataFrame.


### **1. Pandas Data Structures**
A **Pandas Series** is a one-dimensional labeled array that can hold data of any type (integer, float, string, objects, etc.). Think of it like a column in a spreadsheet or a single column from a table. It has two main components:

Data - The actual values
Index - Labels for each value

```
import pandas as pd

#Temperature reading of a patient
temperature_readings = pd.Series([36.6, 35.9, 37.1, 38.7, 38.5],
                               index=['9:00', '10:00', '11:00', '12:00', '13:00'],
                               name='Body Temperature')

temperature_readings
```

You can do some basic operations on a series. 

```
# Returns boolean mask showing which temperatures are above 37.0
print(temperature_readings > 37.0)

# Calculates average/mean of all temperature readings
print(temperature_readings.mean())

# Provides statistical summary including:
print(temperature_readings.describe())

# Returns tuple showing dimensions (number of readings)
print(temperature_readings.shape)

# Shows data type of the Series
print(temperature_readings.dtypes)

#Displays Series information including:
print(temperature_readings.info())
```

A **Dataframe** is a two-dimensional data structure in Python - think of it like a spreadsheet or a SQL table. It's one of the most important tools in Python for data analysis and manipulation. 

```
# Patient medical records
data = {
    'patient_id': ['P001', 'P002', 'P003', 'P004'],
    'age': [45, 52, 35, 67],
    'blood_pressure': ['120/80', '140/90', '115/75', '160/95'],
    'diabetes': [False, True, False, True],
    'medication': ['aspirin', 'metformin', None, 'metformin']
}

df = pd.DataFrame(data)
df
```

Similarly, you can also view the elements and the associated information of the dataframe using the codes below

```
# Basic DataFrame Views (default is 5)
print(df.head(2))
print(df.tail(2))

# Get random sample of rows
print(df.sample(2))

# Get dimensions (rows, columns)
print(df.shape)

# Get column data types
print(df.dtypes)

# Get comprehensive DataFrame info (non-null counts, data types)
print(df.info())

# Get statistical summary of numerical columns
print(df.describe())
```

You can also do some basic operations with dataframes

```
# Select single column (returns Series)
print(df['age'])

# Select multiple columns (returns DataFrame)
print(df[['patient_id', 'age', 'diabetes']])

# Boolean indexing (patients with diabetes)
print(df[df['diabetes'] == True])

# Value counts (count unique values in medication column)
print(df['medication'].value_counts())

# Check for null values
print(df.isnull().sum())
```

### **2. Pandas Data Export**
Let's start with how to export data, as this will create the files we'll later import. You can write dataframes to CSV files. 

```
import pandas as pd

# Pandas can take a dictionary and convert it to a dataframe
patient_data = {
    'patient_id': ['P001', 'P002', 'P003', 'P004'],
    'age': [45, 62, 35, 51],
    'biomarker_a': [125.7, 98.3, 156.2, 112.8],
    'mutation_status': ['BRCA1+', 'BRCA2-', 'BRCA1-', 'BRCA2+'],
    'treatment_response': [1, 0, 1, 1]
}

# Create DataFrame
df = pd.DataFrame(patient_data)

# Visualize the dataframe
df

# Export to CSV
df.to_csv('patient_biomarkers.csv', index=False)

# Export with specific separator 
df.to_csv('patient_biomarkers_semicolon.csv', sep=';', index=False)
```

You can also write the dataframe to Excel format
```
df.to_excel('clinical_data.xlsx', index=False)
```

Now, if you would like to write to multiple sheet, you would need to use the ExcelWrite() class. 
```
# Export to Excel with multiple sheets
with pd.ExcelWriter('clinical_data.xlsx') as writer:
    df.to_excel(writer, sheet_name='Biomarker_Data', index=False)
    
    # Adding summary statistics to another sheet
    summary_stats = df[['biomarker_a']].describe()
    summary_stats.to_excel(writer, sheet_name='Summary_Statistics')
```

> [!NOTE]  
> How can i decide when do i use CSV or Excel?
> 
> CSV: Simple text file format that's lightweight and universally compatible with all systems and programming languages, best for automated data processing and large datasets.
> 
> Excel (.xlsx): Feature-rich format that supports formatting, multiple sheets, formulas, and visualizations, best when humans need to interact with or present the data.

### **3. Pandas Data Import**
Now let's work with importing the files we just created.

```
# Basic CSV reading
biomarker_data = pd.read_csv('patient_biomarkers.csv')

# Reading CSV with specific parameters
biomarker_data_semicolon = pd.read_csv('patient_biomarkers_semicolon.csv',
                                      sep=';',  # Separator used in file
                                      header=0,  # First row is header
                                      na_values=['NA', 'missing'])  # Define missing value markers

biomarker_data_semicolon # visualize the dataframe
```

We can also read back Excel files

```
# Reading specific sheet
biomarker_data_excel = pd.read_excel('clinical_data.xlsx',
                                    sheet_name='Biomarker_Data')

biomarker_data_excel # visualize the dataframe

# Reading multiple sheets
all_sheets = pd.read_excel('clinical_data.xlsx',
                          sheet_name=None)  # Returns dict of DataFrames

all_sheets # visualize the dataframe
```

### **4. Indexing and Slicing**

Let's see how we can do indexing and slicing in dataframes. First, let's create a sample dataframe. 

```
import pandas as pd

# Creating a patient dataset
patient_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003'],
    'age': [45, 62, 33],
    'blood_pressure': ['120/80', '140/90', '118/75'],
    'glucose_level': [95, 142, 88],
    'medication': ['metformin', 'lisinopril', 'none']
})

# Setting patient_id as index
patient_data.set_index('patient_id', inplace=True)
```

There are two main methods to access columns: 
(a) Using the dot notation

```
# Get all glucose levels
glucose_readings = patient_data.glucose_level

# Calculate mean age
average_age = patient_data.age.mean()
```

(b) Using the bracket notation

```
# Get blood pressure readings
bp_readings = patient_data['blood_pressure']

# Select multiple columns
vital_signs = patient_data[['blood_pressure', 'glucose_level']]
```

### **5. Boolean indexing and masking**
Boolean Indexing and Masking in pandas is a powerful way to filter data using True/False conditions. 

```
# Example DataFrame
df = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie', 'David'],
    'age': [25, 30, 35, 40],
    'score': [85, 92, 78, 95]
})

# Boolean mask - creates array of True/False values
mask = df['age'] > 30

# Apply mask to filter DataFrame
older_people = df[mask]  # Shows only rows where age > 30

# You can also write it in one line
high_scorers = df[df['score'] >= 90]  # Shows only rows where score >= 90

# Multiple conditions using & (and) or | (or)
good_young_students = df[(df['age'] < 30) & (df['score'] > 80)]
```

This acts as a sort of sieve: you create a pattern of True/False values (the mask) and only the data matching "True" gets through. It's particularly useful because you can combine multiple conditions and the syntax is very readable compared to traditional SQL-style filtering.

### **6. Label-based indexing using loc[]**

This is normally used when working with named indices (like patient IDs) or column labels. Let's go back to our original dataframe

```
patient_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003'],
    'age': [45, 62, 33],
    'blood_pressure': ['120/80', '140/90', '118/75'],
    'glucose_level': [95, 142, 88],
    'medication': ['metformin', 'lisinopril', 'none']
})

patient_data.set_index('patient_id', inplace=True)
```

We can use loc[] as such:

```
# Get specific patient data
patient_p001 = patient_data.loc['P001']
patient_p001

# Get specific measurements for certain patients
specific_readings = patient_data.loc[['P001', 'P003'], ['blood_pressure', 'glucose_level']]
specific_readings

# Conditional selection with labels
elderly_glucose = patient_data.loc[patient_data['age'] > 60,'glucose_level']
```

### **7. Label-based indexing using iloc[]**

This is normally used when working with numerical positions.

```
# Get first patient's data
first_patient = patient_data.iloc[0]
first_patient

# Get first two patients' vital signs
first_two_vitals = patient_data.iloc[0:2, 1:3] #iloc[rows, columns]
first_two_vitals

# Get alternate rows of specific columns
alternate_readings = patient_data.iloc[::2, [1, 2]]
alternate_readings
```


