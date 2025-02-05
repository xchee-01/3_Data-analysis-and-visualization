## Basic Level Questions

#### 1. Given the following patient dataframe, write a code to count how many missing values are there in total.

```
patient_df = pd.DataFrame({
    'patient_id': [1, 2, 3, 4],
    'age': [45, None, 51, None],
    'biomarker_A': [0.5, 0.7, None, 0.6],
    'genetic_variant': ['rs123', None, 'rs789', 'rs456']
})
```

  <details>
  <summary>Click to view answer</summary>

  ```
  patient_df.isna().sum().sum()
  ```
  
  </details>

#### 2. In the dataset below, replace all missing HbA1c values with the mean HbA1c value:

```
diabetes_df['hba1c'] = diabetes_df['hba1c'].fillna(diabetes_df['hba1c'].mean())
```

  <details>
  <summary>Click to view answer</summary>

  ```
  diabetes_df['hba1c'] = diabetes_df['hba1c'].fillna(diabetes_df['hba1c'].mean())
  ```
  
  </details>
  
#### 3. Clean the following gene names by removing whitespace and converting to uppercase:

```
gene_df = pd.DataFrame({
    'gene_name': [' BRCA1 ', 'tp53', ' KRAS', 'EGFR ']
})
```

  <details>
  <summary>Click to view answer</summary>

  ```
  gene_df['gene_name'] = gene_df['gene_name'].str.strip().str.upper()
  ```
  
  </details>
