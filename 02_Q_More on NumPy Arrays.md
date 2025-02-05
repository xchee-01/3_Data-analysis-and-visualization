## Basic Level Questions

#### 1. Given this gene expression matrix:

```
gene_matrix = np.array([[1.2, 2.3, 3.1],
                       [4.5, 5.2, 6.7],
                       [7.8, 8.4, 9.0]])
```

**i. Write a code to acess the expression value in the second row, third column?**

**ii. Select the first two rows of data**

  <details>
  <summary>Click to view answer</summary>

  ```
  i. gene_matrix[1, 2]

  ii. gene_matrix[0:2, :]
  ```
  
  </details>

#### 2. You have two patient data matrices:

```
patient_data_A = np.array([[1.1, 1.2, 1.3],
                          [2.1, 2.2, 2.3]])
patient_data_B = np.array([[3.1, 3.2, 3.3],
                          [4.1, 4.2, 4.3]])
```

**i. How would you combine them _vertically_?**

**ii. How would you combine them _horizontally_?**

  <details>
  <summary>Click to view answer</summary>

  ```
  i. np.vstack([patient_data_A, patient_data_B])

  ii. np.hstack([patient_data_A, patient_data_B])
  ```
  
  </details>

#### 3. Given this protein expression data across different conditions, how would you extract all the measurements from the second time point?

```
protein_data = np.array([[[1.1, 1.2],
                         [1.3, 1.4]],
                        [[2.1, 2.2],
                         [2.3, 2.4]],
                        [[3.1, 3.2],
                         [3.3, 3.4]]])  # shape: (3, 2, 2)
```

  <details>
  <summary>Click to view answer</summary>

  ```
  protein_data[1, :, :
  ```
  
  </details>
