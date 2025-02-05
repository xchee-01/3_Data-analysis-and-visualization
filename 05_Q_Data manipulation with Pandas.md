## Basic Level Questions

**The questions below would be using these dataframes. You may copy these dataframes directly**

```
patient_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003', 'P004', 'P005'],
    'age': [45, 62, 33, 58, 41],
    'gender': ['F', 'M', 'F', 'M', 'F'],
    'condition': ['Type 2 Diabetes', 'Hypertension', 'Type 1 Diabetes', 'Hypertension', 'Type 2 Diabetes'],
    'hba1c': [7.2, 5.8, 6.9, 5.5, 7.8],
    'medication_code': ['MED123', 'MED456', 'MED789', 'MED456', 'MED123']
})
```

and 

```
genetic_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003', 'P004', 'P005'],
    'gene_variant': ['rs123/AA', 'rs456/AG', 'rs123/GG', 'rs456/AA', 'rs789/AG'],
    'risk_score': [0.8, 0.4, 0.6, 0.3, 0.7]
})
```

#### 1. Using the patient_data DataFrame above, add a new column called 'weight_kg' with values [82, 95, 70, 88, 73]. What will the first two rows look like after this addition?

  <details>
  <summary>Click to view answer</summary>

  ```
  patient_data['weight_kg'] = [82, 95, 70, 88, 73]
  print(patient_data.head(2))
  ```

  </details>

#### 2. From the patient_data DataFrame, rename the 'condition' column to 'diagnosis'. What does the column list look like after renaming?

  <details>
  <summary>Click to view answer</summary>

  ```
  patient_data = patient_data.rename(columns={'condition': 'diagnosis'})
  print(patient_data.columns)
  ```
  
  </details>

#### 3. Looking at patient_data, sort the patients by hba1c from highest to lowest. Who are the top 2 patients with the highest hba1c?

  <details>
  <summary>Click to view answer</summary>

  ```
  sorted_patients = patient_data.sort_values('hba1c', ascending=False)
  print(sorted_patients[['patient_id', 'hba1c']].head(2))
  ```
  
  </details>

#### 4. Looking at patient_data, sort the patients by hba1c from highest to lowest. Who are the top 2 patients with the highest hba1c?

  <details>
  <summary>Click to view answer</summary>

  ```
  diabetic_patients = patient_data[patient_data['condition'] == 'Type 2 Diabetes']
  print(f"Number of Type 2 Diabetes patients: {len(diabetic_patients)}")
  print("Patient IDs:", list(diabetic_patients['patient_id']))
  ```
  
  </details>
