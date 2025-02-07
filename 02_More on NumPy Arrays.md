## Numerical computing with NumPy
Let's dwell a bit more on generating 2D and 3D arrays. In real life, we would most likely be dealing with such multi-dimensional arrrays. 

A 2D array is called a **matrix**

```
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])
```

A 3D array is called a **cube**

```
cube = np.array([[[1, 2], [3, 4]],
                 [[5, 6], [7, 8]],
                 [[9, 10], [11, 12]]])
```

**1. Array indexing**

For a 2D array, you can access the elements by:

```
element = matrix[0,1] #array[row, column] 
```

For a 3D array, you access the elements by:

```
element = cube[0, 1, 0] #array[row, column, planes]
```

Here is a fantastic illustration from this website [here](https://bigfundu.medium.com/numpy-basics-4-fbd93ab72164)
<p align="center">
  <img width="690" height="450" src="https://miro.medium.com/v2/resize:fit:1400/format:webp/0*p5YOY0e2EXIYHGma.png">
</p>

- axis = 0 would correspond to **rows** in 2D arrays and in 3D arrays
- axis = 1 would correspond to **columns** in 2D arrays and in 3D arrays
- axis = 2 would correspond to **plans** in 3D arrays

> [!CAUTION]
> Sometimes, the terminologies for 3D arrays would differ. In some instances, the dimensions may be referred to as height, widgth and depth. Therefore, it is always easier to refer them by their axes number, i.e. 0, 1 or 2.

**2. Array slicing**
```
# Get first two rows of matrix
subset = matrix[0:2, :]

# Get specific plane from 3D array
plane = cube[1, :, :]
```

**3. Concatenation**
To join two matrices together, you can concatenate similarly. 

```
matrix = np.array([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9]])

matrix2 = np.array([[10, 11, 12],
                    [13, 14, 15],
                    [16, 17, 18])
```

You can do a vertical or horizontal concatenation 

```
# Vertical concatenation
vertical = np.concatenate([matrix, matrix2], axis=0)
print(vertical)

# Horizontal concatenation
horizontal = np.concatenate([matrix, matrix[:, :2]], axis=1)
print(horizontal)
```

or similarly, with stacking. 
```
# Vertical concatenation
vertical = np.vstack([matrix, matrix2])
print(vertical)

# Horizontal concatenation
horizontal = np.hstack([matrix, matrix2[:, :2]])
print(horizontal)
```

> [!CAUTION]
> When joining matrices in NumPy, you need to make sure their shapes are compatible along the axis where you're joining them.
> Try this:
> ```
> horizontal = np.hstack([matrix, matrix2])  #You will get an error 
> ```

> [!TIP]
> To avoid such runtime error, always check the shapes before concatenating or stacking.
> For example, for 2D arrays
> ```
> a = np.array([[1, 2, 3],
>              [4, 5, 6]])    
> b = np.array([[7, 8, 9],
>              [10, 11, 12]])
> 
> print("Shape of a:", a.shape)  # (2, 3)
> print("Shape of b:", b.shape)  # (2, 3)
> 
> vertical = np.concatenate([a, b], axis=0)
> print(vertical)
>
> horizontal = np.concatenate([a, b], axis=1)
> print(horizontal)
> 
> # Rule 1: For vertical stacking (axis=0)
> # Rule 2: For horizontal stacking (axis=1)
> ```
>
> For 3D arrays, 
> 
> ```
> c = np.array([[[1, 2], [3, 4]],
>              [[5, 6], [7, 8]]])    
> d = np.array([[[9, 10], [11, 12]],
>              [[13, 14], [15, 16]]])
>
> print("\nShape of c:", c.shape)  # (2, 2, 2)
> print("Shape of d:", d.shape)   # (2, 2, 2)
>
> # Rule for 3D: The numbers in the shape must match 
> # except for the axis you're stacking on
> # For axis=0, the last two numbers must match
> # For axis=1, first and last numbers must match
> # For axis=2, first two numbers must match
> 

**4. Matrix operations** (we will just look at 2D arrays for now)

> [!NOTE]
> If you would like a refresher on linear algebra, you can watch the video [here](https://www.youtube.com/watch?v=p48uw2vFWQs&t=10s)

 ```
# Create two sample matrices
A = np.array([[1, 2], 
              [3, 4]])
B = np.array([[5, 6],
              [7, 8]])
```

1. Matrix Addition
```
sum_matrix = A + B
print(sum_matrix)
```

2. Matrix Multiplication
```
product_matrix = np.dot(A, B)  # or use A @ B
print(product_matrix)
```

3. Matrix Transpose
```
transpose_A = A.T
print(transpose_A)
```

4. Element-wise multiplication
```
element_wise_product = A * B
print(element_wise_product)
```


> [!NOTE]  
> What is the difference between a dot product and an element-wise multiplication?
> Element-wise multiplication (A * B) multiplies corresponding elements in the same position. Result has the same shape as input matrices. Normally used in probability calculations. 
> Dot product (A @ B or np.dot(A,B) follows matrix multiplication rules Result shape is (rows of A) × (columns of B). Normally used in geometric transformations, neural networks and feature engineering in machine learning
> 
> ```
> A = np.array([[1, 2],
>              [3, 4]])
> B = np.array([[5, 6],
>              [7, 8]])
>
> element_wise = A * B
> print(element_wise)
>
> dot_product = np.dot(A, B)  # or A @ B
> print(dot_product)
