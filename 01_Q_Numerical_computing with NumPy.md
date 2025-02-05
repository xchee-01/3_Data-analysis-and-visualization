## Basic Level Questions

#### 1. Given a set of patient temperatures [98.6, 99.1, 97.9, 98.3, 98.9], create a NumPy array and calculate its mean.

  <details>
  <summary>Click to view answer</summary>

  ```
  import numpy as np
  temperatures = np.array([98.6, 99.1, 97.9, 98.3, 98.9])
  mean_temp = np.mean(temperatures)  # Result: 98.56
  ```
  
  </details>

#### 2. What command would you use to check the size (total number of elements) of a NumPy array containing patient IDs?

```
patient_ids = np.array([101, 102, 103, 104, 105])
```

> [!NOTE]
> You may read more [here](https://www.geeksforgeeks.org/numpy-ndarray-size/)

  <details>
  <summary>Click to view answer</summary>

  ```
  size = patient_ids.size
  ```
  
  </details>

#### 3. Create a sequence of BMI values from 18.5 to 30.0, with 10 _equally spaced_ numbers. 

> [!NOTE]
> You may read more [here](https://www.geeksforgeeks.org/numpy-linspace/)

  <details>
  <summary>Click to view answer</summary>

  ```
  bmi_range = np.linspace(18.5, 30.0, num=10)
  ```
  
  </details>

#### 4. Given this array of patient ages [25, 30, 35, 40, 45], how would you select just the first three ages?

  <details>
  <summary>Click to view answer</summary>

  ```
  ages = np.array([25, 30, 35, 40, 45])
  first_three = ages[0:3] 
  ```
  
  </details>

#### 5. How would you find the minimum and maximum values in an array of patient heart rates?

  <details>
  <summary>Click to view answer</summary>

  ```
  heart_rates = np.array([68, 72, 65, 82, 75])
  min_rate = np.min(heart_rates)  
  max_rate = np.max(heart_rates)  
  ```
  
  </details>

## Intermediate Level Questions

#### 2. You have gene expression data for 5 patients across 3 genes. Calculate the mean expression for each gene.

```
gene_data = np.array([[0.45, 0.67, 0.89],
                      [0.55, 0.72, 0.92],
                      [0.49, 0.65, 0.87],
                      [0.51, 0.71, 0.88],
                      [0.47, 0.69, 0.91]])
```

  <details>
  <summary>Click to view answer</summary>

  ```
  gene_means = np.mean(gene_data, axis=0)  # Calculates mean along columns
  ```
  
  </details>
