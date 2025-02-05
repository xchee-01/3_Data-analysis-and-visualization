## Basic Level Questions

> [!TIP]
> You may find the Pandas cheat sheet [here](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf) useful.
> If something is missing, it's always worth searching it up online to find out.

#### 1. Given this simple patient dataframe:

```
patient_basic = pd.DataFrame({
    'patient_id': ['A1', 'A2', 'A3', 'A4'],
    'age': [45, 32, 67, 28],
    'gender': ['F', 'M', 'F', 'M'],
    'blood_type': ['A+', 'O-', 'B+', 'AB+']
})
```

**what code would you write to:**

**i. Display only the age column?**

**ii. Show the first 2 rows?**

**iii. Get the data types of all columns?**

  <details>
  <summary>Click to view answer</summary>

  ```
  i. print(patient_basic['age'])

  ii. print(patient_basic.head(2))

  iii. print(patient_basic.dtypes)
  ```
  
  </details>

#### 2. Using this biomarker dataframe:

```
biomarker_basic = pd.DataFrame({
    'patient_id': ['P1', 'P2', 'P3', 'P4', 'P5'],
    'glucose': [99, 105, 88, 92, 130],
    'cholesterol': [185, 220, 176, 200, 240],
    'blood_pressure': ['120/80', '130/85', '118/75', '125/82', '140/90']
})
```

**what code would you write to:**

**i. Find the average glucose level?**

**ii. Count how many patients are in the dataset?**

**iii. List all column names?**

  <details>
  <summary>Click to view answer</summary>

  ```
  i. print(biomarker_basic['glucose'].mean())

  ii. print(len(biomarker_basic))

  iii. print(biomarker_basic.columns)
  ```
  
  </details>

## Intermediate Level Questions

#### 3. Given this genetic test results dataframe:

```
genetic_results = pd.DataFrame({
    'sample_id': ['S1', 'S2', 'S3', 'S4'],
    'test_result': ['Positive', 'Negative', 'Positive', 'Negative'],
    'quality_score': [95, 87, 92, 88],
    'date_tested': ['2024-01-01', '2024-01-01', '2024-01-02', '2024-01-02']
})
```

**what code would you write to:**

**i. Count how many positive and negative results there are?**

**ii. Find the highest quality score?**

**iii. Show only samples with quality score above 90?**

  <details>
  <summary>Click to view answer</summary>

  ```
  i. print(genetic_results['test_result'].value_counts())

  ii. print(genetic_results['quality_score'].max())

  iii. print(genetic_results[genetic_results['quality_score'] > 90])
  ```
  
  </details>

#### 4. Using this medication tracking dataframe:

```
medication_data = pd.DataFrame({
    'patient_id': ['M1', 'M2', 'M3', 'M4', 'M5'],
    'medication': ['Drug A', 'Drug B', 'Drug A', 'Drug C', 'Drug B'],
    'dose_mg': [100, 250, 100, 500, 250],
    'taken': [True, True, False, True, True]
})
```

**How would you:**

**i. Find all patients taking Drug A?**

**ii. Count how many patients took their medication (True in 'taken' column)?**

  <details>
  <summary>Click to view answer</summary>

  ```
  i. print(medication_data[medication_data['medication'] == 'Drug A'])

  ii. print(medication_data['taken'].sum())
  ```
  
  </details>
