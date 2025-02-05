## Numerical computing with NumPy

NumPy (Numerical Python) is a fundamental library for scientific computing in Python that provides support for large, multi-dimensional arrays and matrices, along with a vast collection of mathematical functions to operate on these arrays efficiently.

Developed by Travis Oliphant in 2005, NumPy evolved from an earlier package called Numeric, which was created by Jim Hugunin in 1995. NumPy unified the competing array packages of its time under one powerful library, becoming a cornerstone of Python's scientific computing ecosystem.

At its core, NumPy's main object is the homogeneous multidimensional array. Unlike Python lists, NumPy arrays require all elements to be of the same type, which enables much more efficient storage and operations. This efficiency comes from NumPy's use of contiguous memory blocks and its ability to perform operations on entire arrays without Python loops, a concept known as vectorization.

> [!NOTE]  
> **Homogenous array** means that all elements must be the same type
> For example, numpy_array = [1,2,3,4] where all of the elements inside are integers


> [!NOTE]  
> **Contiguous memory blocks** means that the items are stored next to each other, making it faster to access them.
><p align="center">
>  <img width="690" height="450" src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*mF9QCqqIKBLhRz4Xco0-EQ.png">
></p>


> [!NOTE]  
> **Vectorization** is a programming technique where operations are performed on entire arrays/blocks of data at once, rather than using loops to process one element at a time.
> Here's traditional way that you would do **without vectorization**
> ```
> # Let's say you want to multiply each number by 2
> numbers = [1, 2, 3, 4, 5]
> result = []
> for number in numbers:    # Have to go through one by one
>    result.append(number * 2)
> ```
> However, with vectorization using NumPy, you can:
> ```
> import numpy as np
> numbers = np.array([1, 2, 3, 4, 5])
> result = numbers * 2      # All numbers multiplied at once
> ```

### Numpy data structures

**1. Basic 1D-arrays (ndarray - N-dimensional array)**
   
Arrays are fundamental data structures in NumPy. 
```
import numpy as np

# Creating a 1D array of patient blood glucose readings
glucose_readings = np.array([95, 102, 98, 115, 107])
```

There are a three ways of how you can create arrays. You can:
(a) Create from scratch 
```
import numpy as np

# Create array with specific values
arr = np.array([1, 2, 3, 4, 5])
```

(b) Using array creation functions 
```
zeros = np.zeros(5)         # [0. 0. 0. 0. 0.]
ones = np.ones(5)          # [1. 1. 1. 1. 1.]
empty = np.empty(5)        # Uninitialized values

numbers = np.arange(5) 
temp_scale = np.linspace(1,11,num=2)
```

> [!NOTE]  
> You can read more about the documentation for arange [here](https://www.geeksforgeeks.org/numpy-arrange-in-python/)
> 
> You can read more about the documentation for linspace [here](https://www.geeksforgeeks.org/numpy-arrange-in-python/)


(c) Initialize with shapes (especially for 2D and 3D-arrays
```
arr = np.zeroes((3,3))
```

**2. Array properties and attributes**

```
# Shape: dimensions of the array
print(vitals.shape) 

# Data type
print(vitals.dtype)  

# Size: total number of elements
print(vitals.size)   
```

**3. Array operations**

1. Mathematical and statistical operations
```
# Analysis of patient cohort
ages = np.array([45, 55, 67, 48, 52, 59, 61])
mean_age = np.mean(ages)
std_age = np.std(ages)
median_age = np.median(ages)

# Percentiles for reference ranges
percentiles = np.percentile(glucose_readings, [25, 50, 75])
```

2. Broadcasting
Broadcasting in NumPy is a mechanism that allows arrays with different shapes to be used together in arithmetic operations. It automatically expands the smaller array to match the shape of the larger array without actually copying the data.

```
array1 = np.array([[1, 2, 3],
                   [4, 5, 6]])    # 2x3 array

array2 = np.array([10, 20, 30])   # 1x3 array

# When combined, array2 is broadcast to match array1:
# [[10, 20, 30],
#  [10, 20, 30]]

array3 = array1 + array2
print(array3)
```

**4. Array indexing**

Indexing in NumPy is used to access individual elements in an array using their position numbers (like arr[0] for the first element).

```
import numpy as np

# Create a sample array
arr = np.array([10, 20, 30, 40, 50, 60, 70, 80, 90])

# Basic indexing (getting single elements)
print(arr[0])      # First element: 10
print(arr[-1])     # Last element: 90
print(arr[-2])     # Second to last: 80
```

**5. Array slicing**

Slicing allows you to extract a range of elements from an array using a start:end:step pattern (like arr[1:4] to get elements from position 1 to 3).

```
# Basic slicing [start:end:step]
print(arr[2:5])    # Elements from index 2 to 4: [30, 40, 50]
print(arr[:4])     # Elements from start to index 3: [10, 20, 30, 40]
print(arr[4:])     # Elements from index 4 to end: [50, 60, 70, 80, 90]
print(arr[::2])    # Every second element: [10, 30, 50, 70, 90]

# Reverse array
print(arr[::-1])   # All elements in reverse: [90, 80, 70, 60, 50, 40, 30, 20, 10]

# Negative slicing
print(arr[-3:])    # Last three elements: [70, 80, 90]
print(arr[:-2])    # All except last two: [10, 20, 30, 40, 50, 60, 70]

# Using step with slicing
print(arr[1:7:2])  # From index 1 to 6, step by 2: [20, 40, 60]
```

**6. Array manipulation**

(a) Reshaping means rearranging elements in the array into a different shape while keeping all the elements

```
import numpy as np

# Start with a 1D array
arr = np.array([1, 2, 3, 4, 5, 6])
print("Original array:", arr)  # [1, 2, 3, 4, 5, 6]

# Reshape to 2x3 matrix (2 rows, 3 columns)
matrix1 = arr.reshape(2, 3)
print(matrix1)

# Reshape to 3x2 matrix (3 rows, 2 columns)
matrix2 = arr.reshape(3, 2)
print(matrix2)

# Using -1 lets NumPy calculate the necessary size
matrix3 = arr.reshape(-1, 2)  # -1 means "figure out how many rows are needed"
print(matrix3)
```

(b) Concatenation and staking

You can concatenate a 1D-array
```
import numpy as np

# 1D arrays
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# Concatenate 1D
concat_1d = np.concatenate((arr1, arr2))
print(concat_1d)  # [1 2 3 4 5 6]
```

and you can also concatenate multi-dimensional arrays as well 
```
# 2D arrays
array1 = np.array([[1, 2], [3, 4]])
array2 = np.array([[5, 6], [7, 8]])

# Concatenate along rows (axis=0)
vertical_concat = np.concatenate((array1, array2), axis=0)
print(vertical_concat)

# Concatenate along columns (axis=1)
horizontal_concat = np.concatenate((array1, array2), axis=1)
print(horizontal_concat)
```

You can also us stacking to achieve the same effect 
```
# 2D arrays
array1 = np.array([[1, 2], [3, 4]])
array2 = np.array([[5, 6], [7, 8]])

vstack = np.vstack((array1, array2))
print(vstack)

# Horizontal Stack (hstack)
hstack = np.hstack((array1, array2))
print(hstack)
```



