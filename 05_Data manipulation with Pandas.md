## Data manipulation with Pandas

When working with datas from multiple sources, we often work with complex datasets that need to be cleaned, reshaped, and combined to derive meaningful insights. 

Let's first set up two mock datasets for us to try out later. 

```
import pandas as pd
import numpy as np

# Create mock patient data
patient_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003', 'P004', 'P005'],
    'age': [45, 62, 33, 58, 41],
    'gender': ['F', 'M', 'F', 'M', 'F'],
    'condition': ['Type 2 Diabetes', 'Hypertension', 'Type 1 Diabetes', 'Hypertension', 'Type 2 Diabetes'],
    'hba1c': [7.2, 5.8, 6.9, 5.5, 7.8],
    'medication_code': ['MED123', 'MED456', 'MED789', 'MED456', 'MED123']
})

# Create mock genetic data
genetic_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003', 'P004', 'P005'],
    'gene_variant': ['rs123/AA', 'rs456/AG', 'rs123/GG', 'rs456/AA', 'rs789/AG'],
    'risk_score': [0.8, 0.4, 0.6, 0.3, 0.7]
})
```

Now, we can actually edit the datasets. 

1. Adding and removing columns

Adding and removing columns

```
# Add a new column for BMI
patient_data['bmi'] = [28.5, 31.2, 24.6, 29.8, 26.4]

# Remove columns
patient_data = patient_data.drop('medication_code', axis=1)
```

> [!TIP]
> You can also create a derived column.
> #Create risk score based on multiple factors
> ```
> patient_data['composite_risk'] = (
>     (patient_data['age'] * 0.2) +
>     (patient_data['hba1c_level'] * 0.5)
> )
> ```
> We will have a more detailed look at how to create columns using functions later


2. Renaming columns

```
# Rename specific columns
patient_data = patient_data.rename(columns={
    'condition': 'diagnosis',
    'hba1c': 'hba1c_level'
})
```

3. Sorting data

```
# Sort by HbA1c level descending
high_risk_patients = patient_data.sort_values('hba1c_level', ascending=False)

# Multiple column sorting
patient_data.sort_values(['diagnosis', 'age'], ascending=[True, False])

# Sort by index
patient_data.sort_index()
```

4. Combining datasets together using `concat()`

We can combine new data to existing dataframe. 

```
# Create another dataset with new patients
new_patients = pd.DataFrame({
    'patient_id': ['P006', 'P007'],
    'age': [52, 39],
    'diagnosis': ['Type 2 Diabetes', 'Hypertension']
})

# Concatenate vertically
all_patients = pd.concat([patient_data, new_patients], ignore_index=True)
```

Or, we can slice off a column from a dataframe and put onto a different dataframe. 

```
# Concatenate horizontally
patient_details = pd.concat([patient_data, genetic_data['gene_variant']], axis=1)
```

5. Combining datasets together using `merge()`

Let's create a new dataset

```
import pandas as pd

# Dataset 1: Clinical Trial Participation
trial_data = pd.DataFrame({
    'trial_id': ['T101', 'T101', 'T102', 'T102', 'T103'],
    'patient_id': ['P001', 'P003', 'P002', 'P005', 'P004'],
    'enrollment_date': ['2024-01-15', '2024-01-15', '2024-02-01', '2024-02-01', '2024-02-15'],
    'drug_arm': ['Treatment A', 'Treatment A', 'Treatment B', 'Treatment B', 'Placebo'],
    'completion_status': ['Completed', 'Withdrawn', 'Completed', 'Ongoing', 'Completed']
})

trial_data
```

and 

```
# Dataset 2: Patient Outcomes
outcome_data = pd.DataFrame({
    'patient_id': ['P001', 'P002', 'P003', 'P004', 'P005', 'P006'],
    'follow_up_date': ['2024-03-15', '2024-03-20', '2024-02-01', '2024-03-25', '2024-03-20', '2024-03-15'],
    'response_status': ['Positive', 'Positive', 'No Response', 'Positive', 'Partial', 'Positive'],
    'adverse_events': [0, 1, 2, 0, 1, 0],
    'biomarker_level': [45.2, 38.7, 41.5, 52.3, 39.8, 44.6]
})

outcome_data
```

We can join these datasets using multple ways

(a) Inner join

```
# Inner Join: Only patients who participated in trials and have outcome data
trial_outcomes = trial_data.merge(
    outcome_data,
    on='patient_id',
    how='inner'
)

trial_outcomes
```

(b) Left join

```
# Left Join: All trial participants, whether they have outcome data or not
all_trial_patients = trial_data.merge(
    outcome_data,
    on='patient_id',
    how='left'
)

all_trial_patients
```

(c) Right join

```
# Right Join: All patients with outcomes, whether they participated in trials or not
all_outcome_patients = trial_data.merge(
    outcome_data,
    on='patient_id',
    how='right'
)

all_outcome_patients
```

(d) 

```
# Full Outer Join: All patients from both datasets
all_patients = trial_data.merge(
    outcome_data,
    on='patient_id',
    how='outer'
)

all_patients
```

> [!NOTE]  
> One way of thinking about the different merging style is in the form of a Venn Diagram
> - inner join: Shows only patients who appear in both trials and have outcomes (intersection)
> - left join: Keeps all trial participants, useful for analyzing complete trial cohort
> - right join: Keeps all patients with outcomes, including those not in trials
> - outer join: Shows complete patient universe, with nulls where data is missing
