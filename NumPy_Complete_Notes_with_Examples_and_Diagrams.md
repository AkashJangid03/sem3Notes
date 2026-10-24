# NumPy --- Complete Notes with Examples and Diagrams

**M.Sc. Computer Applications \| Semester 3**\
**Source:** *NumPy_1_sem 3.pdf* (80 pages)\
**Format:** Concept explanations, diagrams, runnable Python examples,
output interpretation, and exam revision.

> These notes follow the topics in the supplied lecture PDF and expand
> them with explanatory examples. Random-number outputs vary between
> runs unless a seed is fixed. Examples use `import numpy as np`.

## Contents

1.  Need for NumPy and numerical data
2.  Python lists vs NumPy arrays
3.  Installing and importing NumPy
4.  Creating arrays
5.  NumPy data types (`dtype`)
6.  Array attributes
7.  Indexing and updating elements
8.  Slicing one-dimensional and multidimensional arrays
9.  Reshaping arrays
10. Concatenation and stacking
11. Splitting arrays
12. Universal functions (ufuncs)
13. Vectorization
14. Broadcasting
15. Common mathematical and statistical operations
16. Case study: sales analysis
17. Common errors and best practices
18. Practice programs
19. Exam and viva questions
20. Quick revision sheet

------------------------------------------------------------------------

# 1. Need for NumPy

## 1.1 What is NumPy?

**NumPy** stands for **Numerical Python**. It is a Python library for
efficiently storing and operating on numerical arrays. Its central
object is the multidimensional array, usually called an `ndarray`.

NumPy is used in: - Numerical and scientific computing - Data analysis
and preprocessing - Statistics and mathematical calculations - Machine
learning and AI workflows - Image processing (an image can be
represented as a numerical array) - Simulations and engineering
calculations

## 1.2 Why represent data as arrays?

Many forms of data can be converted into numerical representations: - A
grayscale image can be represented as a 2D array of pixel intensities. -
A sound recording can be represented as a 1D sequence of measurements
over time. - A table of measurements can be represented as rows and
columns. - Text can be transformed into numbers using an appropriate
encoding or feature representation.

Efficient array storage and manipulation is therefore an important
foundation for data analysis.

## 1.3 Diagram: data represented as arrays

``` text
Image pixels             Sound samples             Tabular measurements
+---+---+---+             time ->                   City  Mon Tue Wed
| 0 |50 |90 |             0.1, 0.4, 0.2, ...        A     21  23  22
+---+---+---+                                       B     27  26  28
|20 |80 |10 |       -> numerical arrays             C     18  19  20
+---+---+---+
        |
        v
  NumPy array operations
  (filter, transform, aggregate, calculate)
```

## 1.4 Why not use only Python lists?

Python lists are flexible: they can contain objects of different types
and can grow dynamically. This flexibility introduces overhead. A NumPy
array normally stores elements of one data type in a compact data
buffer, enabling efficient numerical operations.

``` python
# Python list: manually process every value
values = [1, 2, 3, 4]
squared_list = []
for value in values:
    squared_list.append(value ** 2)

# NumPy: apply the operation to the whole array
import numpy as np
arr = np.array([1, 2, 3, 4])
squared_array = arr ** 2

print(squared_list)   # [1, 4, 9, 16]
print(squared_array)  # [ 1  4  9 16]
```

**Key idea:** NumPy makes many numerical operations shorter and often
faster, especially for large arrays. The exact performance depends on
the operation, data size, and environment.

## 1.5 Conceptual memory diagram

``` text
Python list
list object -> [pointer, pointer, pointer, ...]
                 |        |        |
                 v        v        v
              object 1  object 2  object 3
              (value)   (value)   (value)

NumPy numeric array
array metadata -> [ 1 ][ 2 ][ 3 ][ 4 ]
                   contiguous numerical data buffer
```

This is a simplified conceptual diagram. NumPy arrays also keep metadata
such as shape, data type, strides, and a reference to their data buffer.

------------------------------------------------------------------------

# 2. Python Lists vs NumPy Arrays

  -----------------------------------------------------------------------
  Feature                 Python list             NumPy array
  ----------------------- ----------------------- -----------------------
  Data types              Can mix types           Normally one common
                                                  `dtype`

  Numerical operations    Often require loops or  Vectorized element-wise
                          comprehensions          operations

  Storage                 References to Python    Compact typed data
                          objects                 buffer in typical
                                                  numeric arrays

  Multidimensional data   Nested lists            Native multidimensional
                                                  array

  Mathematical functions  Limited built-in        Many array and
                          support                 mathematical functions

  Best suited for         General collections and Numerical computation
                          mixed data              and array processing
  -----------------------------------------------------------------------

## 2.1 Mixed data and NumPy type conversion

``` python
mixed = [True, "2", 3.0, 4]
print([type(item).__name__ for item in mixed])
# ['bool', 'str', 'float', 'int']

arr = np.array([3.14, 4, 2, 3])
print(arr)
# [3.14 4.   2.   3.  ]
print(arr.dtype)
# Typically float64 on common installations
```

When possible, NumPy converts compatible values to a common type. This
is called **type promotion** or **upcasting**. Exact default integer and
floating types can depend on platform and input.

------------------------------------------------------------------------

# 3. Installing and Importing NumPy

If NumPy is not installed in your Python environment, run this in a
terminal:

``` bash
python -m pip install numpy
```

In a notebook, a common command is:

``` python
%pip install numpy
```

Import it using the conventional alias `np`:

``` python
import numpy as np
```

Check the installed version:

``` python
print(np.__version__)
```

**Note:** Installation is usually needed once per Python environment. Do
not type terminal commands such as `pip install numpy` as ordinary
Python statements in a `.py` file.

------------------------------------------------------------------------

# 4. Creating NumPy Arrays

## 4.1 From a Python list: `np.array()`

``` python
import numpy as np

a = np.array([1, 4, 2, 5, 3])
print(a)
# [1 4 2 5 3]
```

A two-dimensional array can be created from nested lists:

``` python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])
print(matrix)
# [[1 2 3]
#  [4 5 6]]
```

## 4.2 `np.zeros()`

Creates an array filled with zeros.

``` python
a = np.zeros(5, dtype=int)
print(a)
# [0 0 0 0 0]
```

## 4.3 `np.ones()`

Creates an array filled with ones.

``` python
a = np.ones((2, 3), dtype=float)
print(a)
# [[1. 1. 1.]
#  [1. 1. 1.]]
```

`(2, 3)` means 2 rows and 3 columns.

## 4.4 `np.full()`

Creates an array filled with a specified value.

``` python
a = np.full((2, 3), 7)
print(a)
# [[7 7 7]
#  [7 7 7]]
```

## 4.5 `np.arange()`

Creates values at regular steps. The stop value is excluded, as in
Python's `range()`.

``` python
print(np.arange(0, 10, 2))
# [0 2 4 6 8]

print(np.arange(5))
# [0 1 2 3 4]
```

Syntax: `np.arange(start, stop, step)`.

## 4.6 `np.linspace()`

Creates a specified number of evenly spaced values between endpoints. By
default, the endpoint is included.

``` python
print(np.linspace(0, 1, 5))
# [0.   0.25 0.5  0.75 1.  ]
```

Unlike `arange`, the third argument here is the **number of samples**,
not the step size.

## 4.7 Random arrays

The lecture PDF uses `np.random` functions. These remain useful for
learning and simple examples.

### Random decimal values from 0 up to (but not including) 1

``` python
np.random.seed(0)  # optional: makes legacy random output repeatable
print(np.random.random((2, 3)))
```

The seed makes the sequence reproducible in the same compatible
environment; printed values are omitted here because exact sequences can
vary by API/version.

### Normally distributed random values

``` python
values = np.random.normal(loc=0, scale=1, size=(2, 3))
print(values)
```

-   `loc`: mean of the distribution
-   `scale`: standard deviation
-   `size`: output shape

### Random integers

``` python
print(np.random.randint(0, 10, size=(2, 3)))
```

The lower bound `0` is included; upper bound `10` is excluded. Output
shape is 2 rows by 3 columns.

For newer code that needs an explicit random generator, use:

``` python
rng = np.random.default_rng(42)
print(rng.integers(0, 10, size=(2, 3)))
```

## 4.8 Identity matrix: `np.eye()`

An identity matrix has ones on the main diagonal and zeros elsewhere.

``` python
print(np.eye(3))
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]
```

## 4.9 Array-creation function summary

  -------------------------------------------------------------------------------
  Function                Purpose                 Example
  ----------------------- ----------------------- -------------------------------
  `np.array()`            Create from             `np.array([1, 2, 3])`
                          list/sequence           

  `np.zeros()`            Fill with zeros         `np.zeros((2, 3))`

  `np.ones()`             Fill with ones          `np.ones(5)`

  `np.full()`             Fill with a specified   `np.full((2, 2), 9)`
                          value                   

  `np.arange()`           Regular step sequence   `np.arange(0, 10, 2)`

  `np.linspace()`         Fixed number of evenly  `np.linspace(0, 1, 5)`
                          spaced values           

  `np.random.random()`    Random decimals in      `np.random.random((2, 2))`
                          `[0, 1)`                

  `np.random.normal()`    Normal-distribution     `np.random.normal(0, 1, 5)`
                          samples                 

  `np.random.randint()`   Random integers         `np.random.randint(0, 10, 5)`

  `np.eye()`              Identity matrix         `np.eye(3)`
  -------------------------------------------------------------------------------

------------------------------------------------------------------------

# 5. NumPy Data Types (`dtype`)

A NumPy array generally stores elements using one data type. The `dtype`
attribute reports that type.

``` python
a = np.array([1, 2, 3])
print(a.dtype)
print(a.dtype.itemsize)  # bytes per element
```

## 5.1 Common NumPy data types

  -----------------------------------------------------------------------
  Type                                Meaning
  ----------------------------------- -----------------------------------
  `bool_`                             Boolean values

  `int8`, `int16`, `int32`, `int64`   Signed integers of specified bit
                                      widths

  `uint8`, `uint16`, `uint32`,        Unsigned integers
  `uint64`                            

  `float16`, `float32`, `float64`     Floating-point values

  `complex64`, `complex128`           Complex numbers
  -----------------------------------------------------------------------

The exact aliases and default types available depend on NumPy version
and platform. A signed 8-bit integer can represent values from -128 to
127; an unsigned 8-bit integer represents 0 to 255.

## 5.2 Explicitly set the data type

``` python
a = np.array([1, 2, 3, 4], dtype=np.float32)
print(a)
# [1. 2. 3. 4.]
print(a.dtype)
# float32
```

Convert an existing array:

``` python
a = np.array([1.8, 2.6, 3.2])
b = a.astype(int)
print(b)
# [1 2 3]
```

Converting floating-point values to integers truncates the fractional
part toward zero; it does not round to the nearest integer.

## 5.3 Why `dtype` matters

-   Controls how values are represented and stored.
-   Influences memory use.
-   Determines supported precision and numeric range.
-   Can affect arithmetic results and type promotion.

Avoid selecting a type too small for the values you expect to store;
integer overflow can occur for fixed-width integer types.

------------------------------------------------------------------------

# 6. NumPy Array Attributes

Consider these arrays:

``` python
x1 = np.array([10, 20, 30, 40, 50])
x2 = np.array([[1, 2, 3],
               [4, 5, 6]])
x3 = np.arange(24).reshape(2, 3, 4)
```

## 6.1 Important attributes

  Attribute    Meaning                              Example
  ------------ ------------------------------------ -----------------------
  `ndim`       Number of dimensions (axes)          `x2.ndim` → `2`
  `shape`      Size of each dimension               `x2.shape` → `(2, 3)`
  `size`       Total number of elements             `x2.size` → `6`
  `dtype`      Element data type                    `x2.dtype`
  `itemsize`   Bytes per element                    `x2.itemsize`
  `nbytes`     Total bytes used by array elements   `x2.nbytes`

Example:

``` python
print("Dimensions:", x2.ndim)     # 2
print("Shape:", x2.shape)         # (2, 3)
print("Elements:", x2.size)       # 6
print("Data type:", x2.dtype)
print("Bytes per element:", x2.itemsize)
print("Data-buffer bytes:", x2.nbytes)
```

`nbytes` describes the element data buffer, not all metadata or the
complete memory overhead of the array object.

## 6.2 Understanding dimensions with a diagram

``` text
1D array: shape (4)
[10, 20, 30, 40]

2D array: shape (2, 3)
          column index
             0  1  2
row index 0 [ 1  2  3 ]
          1 [ 4  5  6 ]

3D array: shape (2, 3, 4)
2 blocks, each containing 3 rows and 4 columns
```

For `shape = (2, 3, 4)`, total elements = `2 × 3 × 4 = 24`.

------------------------------------------------------------------------

# 7. Array Indexing: Accessing and Updating Elements

Python and NumPy indexing starts at `0`.

## 7.1 One-dimensional indexing

``` python
x = np.array([5, 0, 3, 3, 7, 9])

print(x[0])    # 5
print(x[4])    # 7
print(x[-1])   # 9 (last element)
print(x[-2])   # 7 (second last element)
```

Index diagram:

``` text
Values:  [ 5   0   3   3   7   9 ]
Index:     0   1   2   3   4   5
Negative: -6  -5  -4  -3  -2  -1
```

## 7.2 Two-dimensional indexing

Use `array[row_index, column_index]`.

``` python
x = np.array([[3, 5, 2, 4],
              [7, 6, 8, 8],
              [1, 6, 7, 7]])

print(x[0, 0])   # 3
print(x[2, 0])   # 1
print(x[2, -1])  # 7
```

``` text
          col 0  col 1  col 2  col 3
row 0       3      5      2      4
row 1       7      6      8      8
row 2       1      6      7      7

x[1, 2] -> row 1, column 2 -> 8
```

## 7.3 Updating a value

``` python
x[0, 0] = 12
print(x)
# [[12  5  2  4]
#  [ 7  6  8  8]
#  [ 1  6  7  7]]
```

The assigned value must be compatible with the array's data type. For
example, assigning a decimal to an integer array may convert it to an
integer.

------------------------------------------------------------------------

# 8. Array Slicing: Accessing Subarrays

Slicing syntax:

``` python
array[start:stop:step]
```

The `stop` index is excluded. If omitted, the defaults depend on the
direction of the step.

## 8.1 One-dimensional slicing

``` python
x = np.arange(10)  # [0 1 2 3 4 5 6 7 8 9]

print(x[:5])     # [0 1 2 3 4]
print(x[5:])     # [5 6 7 8 9]
print(x[4:7])    # [4 5 6]
print(x[::2])    # [0 2 4 6 8]
print(x[1::2])   # [1 3 5 7 9]
print(x[::-1])   # [9 8 7 6 5 4 3 2 1 0]
print(x[5::-2])  # [5 3 1]
```

## 8.2 Two-dimensional slicing

For a 2D array, use `array[rows, columns]`. Each part may be a slice.

``` python
grid = np.array([[12, 5, 2, 4],
                 [7, 6, 8, 8],
                 [1, 6, 7, 7]])

print(grid[:2, :3])  # first 2 rows, first 3 columns
# [[12  5  2]
#  [ 7  6  8]]

print(grid[:, 0])    # first column
# [12  7  1]

print(grid[:, ::2])  # all rows, every other column
# [[12  2]
#  [ 7  8]
#  [ 1  7]]

print(grid[::-1, ::-1])  # reverse rows and columns
```

### Slice diagram

``` text
Original (3 rows × 4 columns)
+----+----+----+----+
| 12 |  5 |  2 |  4 |
+----+----+----+----+
|  7 |  6 |  8 |  8 |
+----+----+----+----+
|  1 |  6 |  7 |  7 |
+----+----+----+----+

grid[:2, :3] selects:
+----+----+----+
| 12 |  5 |  2 |
+----+----+----+
|  7 |  6 |  8 |
+----+----+----+
```

## 8.3 Important: slices often share data

Basic NumPy slices commonly return **views**, not independent copies.
Updating a view can update the original array.

``` python
a = np.array([10, 20, 30, 40])
view = a[1:3]
view[0] = 99
print(a)  # [10 99 30 40]
```

To make an independent copy:

``` python
copy = a[1:3].copy()
```

This distinction is important when editing a selected portion of data.

------------------------------------------------------------------------

# 9. Reshaping Arrays

`reshape()` changes the arrangement/shape of an array without changing
the number of elements.

## 9.1 Reshape a 1D array into a 2D array

``` python
a = np.arange(1, 10)
grid = a.reshape((3, 3))
print(grid)
# [[1 2 3]
#  [4 5 6]
#  [7 8 9]]
```

Diagram:

``` text
1D: [1 2 3 4 5 6 7 8 9]
                 |
                 | reshape(3, 3)
                 v
2D:  [[1 2 3]
      [4 5 6]
      [7 8 9]]
```

The element count must remain the same: `9` values can become `(3, 3)`
or `(1, 9)`, but not `(2, 5)`.

## 9.2 Row vector and column vector

``` python
x = np.array([1, 2, 3])

row = x.reshape((1, 3))
column = x.reshape((3, 1))

print(row)
# [[1 2 3]]

print(column)
# [[1]
#  [2]
#  [3]]
```

## 9.3 Infer one dimension with `-1`

``` python
a = np.arange(12)
print(a.reshape(3, -1))
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]
```

NumPy infers the missing dimension. Only one dimension can be `-1` in a
reshape call.

------------------------------------------------------------------------

# 10. Array Concatenation and Stacking

Concatenation combines arrays. For multidimensional arrays, shapes must
be compatible along the dimensions not being joined.

## 10.1 `np.concatenate()`

``` python
x = np.array([1, 2, 3])
y = np.array([3, 2, 1])

print(np.concatenate([x, y]))
# [1 2 3 3 2 1]
```

For 2D arrays:

``` python
grid = np.array([[1, 2, 3],
                 [4, 5, 6]])

print(np.concatenate([grid, grid], axis=0))  # add rows
# [[1 2 3]
#  [4 5 6]
#  [1 2 3]
#  [4 5 6]]

print(np.concatenate([grid, grid], axis=1))  # add columns
# [[1 2 3 1 2 3]
#  [4 5 6 4 5 6]]
```

## 10.2 `np.vstack()` and `np.hstack()`

-   `vstack`: stack vertically (add rows).
-   `hstack`: stack horizontally (add columns in common 2D examples).

``` python
x = np.array([1, 2, 3])
grid = np.array([[9, 8, 7],
                 [6, 5, 4]])

print(np.vstack([x, grid]))
# [[1 2 3]
#  [9 8 7]
#  [6 5 4]]

y = np.array([[99], [99]])
print(np.hstack([grid, y]))
# [[ 9  8  7 99]
#  [ 6  5  4 99]]
```

Diagram:

``` text
vstack: one row + two-row grid -> three-row array
[1 2 3]                  [1 2 3]
                         [9 8 7]
                         [6 5 4]

hstack: grid + one column -> wider grid
[9 8 7] + [99]  ->  [9 8 7 99]
[6 5 4]   [99]      [6 5 4 99]
```

------------------------------------------------------------------------

# 11. Splitting Arrays

Splitting is the opposite of concatenation. Functions include
`np.split()`, `np.vsplit()` and `np.hsplit()`.

## 11.1 `np.split()`

``` python
x = np.array([1, 2, 3, 99, 99, 3, 2, 1])
x1, x2, x3 = np.split(x, [3, 5])

print(x1)  # [1 2 3]
print(x2)  # [99 99]
print(x3)  # [3 2 1]
```

Two split positions produce three subarrays. With integer `sections`,
the array generally needs to divide evenly into that many sections.

## 11.2 `np.vsplit()` and `np.hsplit()`

``` python
grid = np.arange(16).reshape((4, 4))

upper, lower = np.vsplit(grid, [2])
print(upper)
# [[0 1 2 3]
#  [4 5 6 7]]
print(lower)
# [[ 8  9 10 11]
#  [12 13 14 15]]

left, right = np.hsplit(grid, [2])
print(left)
# [[ 0  1]
#  [ 4  5]
#  [ 8  9]
#  [12 13]]
print(right)
# [[ 2  3]
#  [ 6  7]
#  [10 11]
#  [14 15]]
```

Diagram:

``` text
Original 4 × 4 array          Vertical split       Horizontal split
+----+----+----+----+         top two rows         left two columns
|  0 |  1 |  2 |  3 |         +-------------+      +------+------+
|  4 |  5 |  6 |  7 |   ->    | 0  1  2  3  |      | 0  1 | 2  3 |
|  8 |  9 | 10 | 11 |         | 4  5  6  7  |      | 4  5 | 6  7 |
| 12 | 13 | 14 | 15 |         +-------------+      | 8  9 |10 11 |
+----+----+----+----+         bottom two rows      |12 13 |14 15 |
                              +-------------+      +------+------+
                              | 8  9 10 11  |
                              |12 13 14 15  |
                              +-------------+
```

`np.dsplit()` splits along the third axis for arrays with at least three
dimensions.

------------------------------------------------------------------------

# 12. Universal Functions (Ufuncs)

## 12.1 Definition

A **universal function (ufunc)** operates element by element on array
values. Ufuncs are designed for efficient numerical operations and
support vectorized calculations and broadcasting.

Two broad types: - **Unary ufuncs:** operate on one input,
e.g. `np.sqrt()`, `np.sin()`. - **Binary ufuncs:** operate on two
inputs, e.g. `np.add()`, `np.multiply()`.

## 12.2 Arithmetic ufuncs

``` python
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(np.add(a, b))       # [11 22 33]
print(np.subtract(a, b))  # [ 9 18 27]
print(np.multiply(a, b))  # [10 40 90]
print(np.divide(a, b))    # [10. 10. 10.]
print(np.power(b, 2))     # [1 4 9]
print(np.mod(a, 7))       # [3 6 2]
```

Operators such as `a + b`, `a * b`, and `a ** 2` provide convenient ways
to perform many of these operations.

## 12.3 Common ufunc categories

  -------------------------------------------------------------------------
  Category                  Example functions       Purpose
  ------------------------- ----------------------- -----------------------
  Arithmetic                `np.add`,               Numerical operations
                            `np.subtract`,          
                            `np.multiply`,          
                            `np.divide`, `np.mod`,  
                            `np.power`              

  Trigonometric             `np.sin`, `np.cos`,     Trigonometric
                            `np.tan`, `np.arcsin`,  calculations (angles in
                            `np.arccos`,            radians)
                            `np.arctan`             

  Exponential/logarithmic   `np.exp`, `np.log`,     Exponential and
                            `np.log2`, `np.log10`   logarithmic
                                                    calculations

  Bitwise                   `np.bitwise_and`,       Operations on integer
                            `np.bitwise_or`,        bits
                            `np.bitwise_xor`,       
                            `np.invert`             

  Comparison                `np.greater`,           Element-wise
                            `np.less`, `np.equal`,  comparisons
                            `np.not_equal`          

  Floating-point checks     `np.isfinite`,          Check special
                            `np.isinf`, `np.isnan`  floating-point values

  Rounding                  `np.ceil`, `np.floor`,  Rounding and truncation
                            `np.trunc`, `np.round`, 
                            `np.rint`               

  Miscellaneous             `np.abs`,               Other common numerical
                            `np.conjugate`,         operations
                            `np.square`, `np.sqrt`, 
                            `np.clip`               

  Logical                   `np.logical_and`,       Boolean logic
                            `np.logical_or`,        
                            `np.logical_not`,       
                            `np.logical_xor`        

  Hyperbolic                `np.sinh`, `np.cosh`,   Hyperbolic functions
                            `np.tanh`               
  -------------------------------------------------------------------------

The exact set of available functions may change across NumPy versions.

## 12.4 Examples

``` python
a = np.array([-2.4, -0.2, 0.6, 2.8])

print(np.abs(a))    # [2.4 0.2 0.6 2.8]
print(np.floor(a))  # [-3. -1.  0.  2.]
print(np.ceil(a))   # [-2. -0.  1.  3.]
print(np.round(a))  # [-2. -0.  1.  3.]
```

Comparison returns a Boolean array:

``` python
marks = np.array([35, 49, 72, 28])
print(marks >= 40)
# [False  True  True False]
```

Filter using the Boolean mask:

``` python
print(marks[marks >= 40])
# [49 72]
```

Handle special floating-point values:

``` python
values = np.array([1.0, np.inf, np.nan])
print(np.isfinite(values))
# [ True False False]
print(np.isnan(values))
# [False False  True]
```

------------------------------------------------------------------------

# 13. Vectorization

## 13.1 What is vectorization?

**Vectorization** means applying an operation to an entire array without
writing an explicit Python loop for each element. NumPy performs these
operations through optimized low-level routines.

## 13.2 Without vectorization

``` python
arr = np.array([1, 2, 3, 4, 5])
result = []
for value in arr:
    result.append(value ** 2)
print(result)
# [1, 4, 9, 16, 25]
```

## 13.3 With vectorization

``` python
arr = np.array([1, 2, 3, 4, 5])
result = arr ** 2
print(result)
# [ 1  4  9 16 25]
```

Diagram:

``` text
Explicit loop:
1 -> square -> 1
2 -> square -> 4
3 -> square -> 9
4 -> square -> 16
5 -> square -> 25

Vectorized operation:
[1, 2, 3, 4, 5]  ** 2  ->  [1, 4, 9, 16, 25]
```

## 13.4 Why can vectorization be faster?

-   Reduces overhead from Python-level loops.
-   Uses optimized low-level implementations.
-   Can make efficient use of memory access and CPU vector instructions.
-   Makes numerical code more concise and easier to express.

Vectorization is not automatically faster for every tiny task;
performance depends on array size, operation and environment. For
numerical workloads, it is usually the preferred starting point.

------------------------------------------------------------------------

# 14. Broadcasting

## 14.1 Definition

**Broadcasting** allows NumPy to perform element-wise operations on
arrays with compatible but different shapes. NumPy conceptually expands
dimensions of size `1` or a scalar to match the other array without
necessarily creating repeated copies of the data.

## 14.2 Example 1: Add a scalar

``` python
arr = np.array([1, 2, 3])
print(arr + 5)
# [6 7 8]
```

Conceptually:

``` text
[1, 2, 3]
[5, 5, 5]   (conceptual broadcast)
-----------
[6, 7, 8]
```

## 14.3 Example 2: Add a 1D array to a 2D array

``` python
arr1 = np.array([[1, 2, 3],
                 [4, 5, 6],
                 [7, 8, 9]])

arr2 = np.array([10, 20, 30])

print(arr1 + arr2)
# [[11 22 33]
#  [14 25 36]
#  [17 28 39]]
```

`arr1.shape` is `(3, 3)` and `arr2.shape` is `(3,)`. The one-dimensional
array is aligned with the final dimension and its values are applied to
every row.

Conceptually:

``` text
[[1, 2, 3],      [[10, 20, 30],      [[11, 22, 33],
 [4, 5, 6],   +   [10, 20, 30],   =   [14, 25, 36],
 [7, 8, 9]]       [10, 20, 30]]       [17, 28, 39]]
```

## 14.4 Broadcasting rules

Compare dimensions from **right to left**. Two dimensions are compatible
when: 1. They are equal, or 2. One of them is `1`.

If one array has fewer dimensions, missing dimensions are treated as
size `1` on the left. If any aligned pair is neither equal nor `1`,
broadcasting fails.

Examples:

  Shape A    Shape B    Result
  ---------- ---------- -------------------------------
  `(3, 3)`   `(3,)`     `(3, 3)`
  `(4, 1)`   `(1, 3)`   `(4, 3)`
  `(2, 3)`   `(2, 3)`   `(2, 3)`
  `(3, 4)`   `(2, 3)`   Incompatible; raises an error

Example with two column/row shapes:

``` python
a = np.array([[1], [2], [3]])   # shape (3, 1)
b = np.array([10, 20])          # shape (2,)

print(a + b)
# [[11 21]
#  [12 22]
#  [13 23]]
# Result shape: (3, 2)
```

**Common mistake:** assuming NumPy will automatically make any two
shapes compatible. Broadcasting has strict shape rules.

------------------------------------------------------------------------

# 15. Common Mathematical and Statistical Operations

The lecture material lists statistical functions such as `sum`, `prod`,
`mean`, `std`, `var`, `min` and `max`.

``` python
data = np.array([10, 20, 30, 40])

print(np.sum(data))    # 100
print(np.prod(data))   # 240000
print(np.mean(data))   # 25.0
print(np.min(data))    # 10
print(np.max(data))    # 40
print(np.argmin(data)) # 0 (index of minimum)
print(np.argmax(data)) # 3 (index of maximum)
print(np.var(data))    # population variance, by default
print(np.std(data))    # population standard deviation, by default
```

`np.var()` and `np.std()` use `ddof=0` by default (population
variance/standard deviation). Use `ddof=1` when calculating the common
sample estimate.

## 15.1 The `axis` parameter

For a 2D array: - `axis=0`: operate down rows, producing one result per
**column**. - `axis=1`: operate across columns, producing one result per
**row**. - No `axis`: reduce all elements into one result for functions
such as `sum` and `mean`.

``` python
scores = np.array([[70, 80, 90],
                   [60, 75, 85]])

print(np.sum(scores, axis=0))  # column totals
# [130 155 175]

print(np.sum(scores, axis=1))  # row totals
# [240 220]

print(np.mean(scores))         # overall mean
# 76.66666666666667
```

Diagram:

``` text
                 Columns
               0   1   2
Row 0         [70  80  90]  <- axis=1 sum: 240
Row 1         [60  75  85]  <- axis=1 sum: 220
                ^   ^   ^
                |   |   |
           axis=0 sums each column
             [130, 155, 175]
```

## 15.2 Useful functions for analysis

  Function                         What it returns
  -------------------------------- -------------------------------------
  `np.sum(a)`                      Sum of values
  `np.mean(a)`                     Arithmetic mean
  `np.median(a)`                   Median
  `np.min(a)`, `np.max(a)`         Minimum and maximum
  `np.argmin(a)`, `np.argmax(a)`   Index of minimum/maximum
  `np.std(a)`, `np.var(a)`         Standard deviation and variance
  `np.any(condition)`              True if any element is true
  `np.all(condition)`              True if all elements are true
  `np.count_nonzero(condition)`    Number of nonzero/true elements
  `np.clip(a, low, high)`          Values limited to a specified range

------------------------------------------------------------------------

# 16. Case Study: Sales Data Analysis with NumPy

This case study follows the lecture PDF's example: sales for **4
products over 7 days**. Each row represents one product, and each column
represents one day.

## 16.1 Create the dataset

``` python
import numpy as np

sales_data = np.array([
    [150, 200, 250, 300, 350, 400, 450],  # Product 1
    [100, 150, 200, 250, 300, 350, 400],  # Product 2
    [ 50, 100, 150, 200, 250, 300, 350],  # Product 3
    [200, 250, 300, 350, 400, 450, 500]   # Product 4
])

print("Sales data:\n", sales_data)
print("Shape:", sales_data.shape)  # (4, 7)
```

Table view:

``` text
              Day1 Day2 Day3 Day4 Day5 Day6 Day7
Product 1      150  200  250  300  350  400  450
Product 2      100  150  200  250  300  350  400
Product 3       50  100  150  200  250  300  350
Product 4      200  250  300  350  400  450  500
```

## 16.2 Total and average sales per product

Rows are products, so use `axis=1`.

``` python
total_sales_per_product = np.sum(sales_data, axis=1)
average_sales_per_product = np.mean(sales_data, axis=1)

print("Product totals:", total_sales_per_product)
# [2100 1750 1400 2450]

print("Product averages:", average_sales_per_product)
# [300. 250. 200. 350.]
```

## 16.3 Find the day with the highest total sales

Columns are days, so use `axis=0`.

``` python
total_sales_per_day = np.sum(sales_data, axis=0)
highest_sales_day_index = np.argmax(total_sales_per_day)

print("Daily totals:", total_sales_per_day)
# [500 700 900 1100 1300 1500 1700]

print("Highest-sales day:", highest_sales_day_index + 1)
# 7
```

`np.argmax()` returns a zero-based index, so add `1` to display it as
Day 1 through Day 7.

## 16.4 Percentage contribution per product

``` python
grand_total_sales = np.sum(sales_data)
percentage_contribution = (total_sales_per_product / grand_total_sales) * 100

print("Grand total:", grand_total_sales)
# 7700

print("Percentage contribution:", np.round(percentage_contribution, 2))
# [27.27 22.73 18.18 31.82]
```

Percentages are approximately 100% when added together (small
differences can occur due to rounding).

## 16.5 Check for zero-sales days per product

``` python
zero_sales_per_product = np.any(sales_data == 0, axis=1)
print(zero_sales_per_product)
# [False False False False]
```

`np.any(sales_data == 0, axis=1)` checks each product's row for at least
one zero. `False` means that product has no zero-sales day in this
dataset.

## 16.6 Full case-study program

``` python
import numpy as np

sales_data = np.array([
    [150, 200, 250, 300, 350, 400, 450],
    [100, 150, 200, 250, 300, 350, 400],
    [ 50, 100, 150, 200, 250, 300, 350],
    [200, 250, 300, 350, 400, 450, 500]
])

total_per_product = np.sum(sales_data, axis=1)
average_per_product = np.mean(sales_data, axis=1)
total_per_day = np.sum(sales_data, axis=0)
best_day = np.argmax(total_per_day) + 1
grand_total = np.sum(sales_data)
percentage = total_per_product / grand_total * 100
has_zero_sales = np.any(sales_data == 0, axis=1)

print("Total sales per product:", total_per_product)
print("Average sales per product:", average_per_product)
print("Total sales per day:", total_per_day)
print("Day with highest sales:", best_day)
print("Grand total:", grand_total)
print("Product percentage contribution:", np.round(percentage, 2))
print("Any zero-sales day per product:", has_zero_sales)
```

## 16.7 Interpreting the result

-   Product 4 has the highest total sales: `2450`.
-   Product 3 has the lowest total sales: `1400`.
-   Day 7 has the highest total sales: `1700`.
-   Product 4 contributes approximately `31.82%` of total sales.
-   None of the four products has a zero-sales day in the given data.

These conclusions are for the supplied sample dataset only; they do not
establish a general business trend.

------------------------------------------------------------------------

# 17. Common Errors and Best Practices

1.  **Incorrect shape:** `reshape()` requires the same total number of
    elements.
2.  **Wrong index:** indexes start at zero; out-of-range access raises
    `IndexError`.
3.  **Stop index confusion:** slices exclude their stop position.
4.  **Shape mismatch:** concatenation requires compatible shapes;
    broadcasting requires compatible dimensions.
5.  **Wrong axis:** remember `axis=0` produces column-wise reductions
    and `axis=1` row-wise reductions for 2D arrays.
6.  **Mixed data types:** NumPy may promote values to a common type.
7.  **Integer conversion:** `astype(int)` truncates fractional parts
    rather than rounding.
8.  **Slice/view side effects:** basic slices often share data with the
    original array; use `.copy()` when independent data is needed.
9.  **Random outputs:** random arrays differ between runs unless
    reproducibility is configured.
10. **Performance assumptions:** NumPy is designed for efficient array
    operations, but measure performance for the real workload.

------------------------------------------------------------------------

# 18. Practice Programs

Try each problem before reading the solution.

## Program 1: Create an array from 1 to 10

``` python
import numpy as np
a = np.arange(1, 11)
print(a)
```

Output: `[ 1  2  3  4  5  6  7  8  9 10]`

## Program 2: Create a 3 × 3 matrix containing 1 to 9

``` python
a = np.arange(1, 10).reshape(3, 3)
print(a)
```

## Program 3: Find all values greater than 5

``` python
a = np.array([2, 8, 3, 10, 5, 7])
print(a[a > 5])
# [ 8 10  7]
```

## Program 4: Calculate the mean of each row

``` python
a = np.array([[10, 20, 30],
              [40, 50, 60]])
print(np.mean(a, axis=1))
# [20. 50.]
```

## Program 5: Replace negative values with zero

``` python
a = np.array([-3, 2, -1, 5, 0])
a[a < 0] = 0
print(a)
# [0 2 0 5 0]
```

## Program 6: Combine two arrays

``` python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
print(np.concatenate([a, b]))
# [1 2 3 4 5 6]
```

## Program 7: Split an array into three equal sections

``` python
a = np.arange(12)
part1, part2, part3 = np.split(a, 3)
print(part1)  # [0 1 2 3]
print(part2)  # [4 5 6 7]
print(part3)  # [ 8  9 10 11]
```

## Program 8: Demonstrate broadcasting

``` python
a = np.array([[1], [2], [3]])  # shape (3, 1)
b = np.array([10, 20])         # shape (2,)
print(a + b)
# [[11 21]
#  [12 22]
#  [13 23]]
```

## Program 9: Find the maximum value and its index

``` python
a = np.array([18, 45, 27, 62, 39])
print(np.max(a))     # 62
print(np.argmax(a))  # 3
```

## Program 10: Count values satisfying a condition

``` python
temperatures = np.array([28, 35, 37, 31, 40, 33])
print(np.count_nonzero(temperatures > 35))
# 2
```

------------------------------------------------------------------------

# 19. Exam and Viva Questions

## Short-answer questions

1.  What is NumPy? What does the name stand for?
2.  Why are arrays useful in data science?
3.  List four advantages of NumPy arrays over Python lists for numerical
    work.
4.  What is an `ndarray`?
5.  How do you import NumPy using the conventional alias?
6.  Explain `np.array()`, `np.zeros()`, `np.ones()` and `np.full()`.
7.  Differentiate `np.arange()` and `np.linspace()`.
8.  What does `np.eye()` create?
9.  What is `dtype`? Name common NumPy data types.
10. Explain `ndim`, `shape`, `size`, `itemsize` and `nbytes`.
11. Explain positive and negative indexing.
12. What is array slicing? Give its syntax.
13. What is the difference between a view and a copy?
14. What does `reshape()` do? State its main restriction.
15. Differentiate `np.concatenate()`, `np.vstack()` and `np.hstack()`.
16. Explain `np.split()`, `np.vsplit()` and `np.hsplit()`.
17. What is a universal function (ufunc)?
18. Differentiate unary and binary ufuncs.
19. What is vectorization? Why can it be faster?
20. Define broadcasting and list its rules.
21. Explain `axis=0` and `axis=1` with a 2D array.
22. What do `np.sum()`, `np.mean()`, `np.std()` and `np.argmax()` do?
23. How can Boolean indexing be used to filter data?
24. Explain the use of `np.any()` in the sales case study.

## Long-answer/practical questions

1.  Explain the need for NumPy and compare Python lists with NumPy
    arrays.
2.  Demonstrate different ways of creating arrays with code and output.
3.  Explain NumPy data types and important array attributes with
    examples.
4.  Explain indexing and slicing in 1D and 2D arrays with diagrams.
5.  Explain reshaping, concatenation and splitting with suitable
    examples.
6.  Define ufuncs and describe their categories.
7.  Explain vectorization with a loop-based and a vectorized example.
8.  Explain broadcasting rules with examples of compatible and
    incompatible shapes.
9.  Write a program to calculate row-wise and column-wise totals.
10. Solve the sales-data case study using NumPy.

## Output-prediction questions

### Q1

``` python
import numpy as np
a = np.arange(1, 8, 2)
print(a)
```

**Answer:** `[1 3 5 7]`

### Q2

``` python
a = np.array([10, 20, 30, 40, 50])
print(a[1:4])
print(a[::-1])
```

**Answer:** `[20 30 40]`, then `[50 40 30 20 10]`.

### Q3

``` python
a = np.array([[1, 2, 3], [4, 5, 6]])
print(np.sum(a, axis=0))
print(np.sum(a, axis=1))
```

**Answer:** `[5 7 9]`, then `[6 15]`.

### Q4

``` python
a = np.array([1, 2, 3])
print(a * 3)
```

**Answer:** `[3 6 9]`.

### Q5

``` python
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([10, 20, 30])
print(a + b)
```

**Answer:**

``` text
[[11 22 33]
 [14 25 36]]
```

------------------------------------------------------------------------

# 20. Quick Revision Sheet

  ----------------------------------------------------------------------------------
  Topic                               Syntax / Reminder
  ----------------------------------- ----------------------------------------------
  Import                              `import numpy as np`

  Create array                        `np.array([1, 2, 3])`

  Zeros                               `np.zeros((rows, columns))`

  Ones                                `np.ones((rows, columns))`

  Fill value                          `np.full(shape, value)`

  Step sequence                       `np.arange(start, stop, step)`; stop excluded

  Evenly spaced values                `np.linspace(start, stop, number_of_values)`

  Identity matrix                     `np.eye(n)`

  Data type                           `array.dtype`

  Dimensions                          `array.ndim`

  Shape                               `array.shape`

  Number of elements                  `array.size`

  Index element                       `array[index]` or `array[row, column]`

  Slice                               `array[start:stop:step]`

  Reverse                             `array[::-1]`

  Reshape                             `array.reshape(new_shape)`

  Join                                `np.concatenate([a, b], axis=0)`

  Stack rows                          `np.vstack([a, b])`

  Stack columns                       `np.hstack([a, b])`

  Split                               `np.split(array, split_points)`

  Element-wise math                   `a + b`, `a * b`, `a ** 2`

  Mean                                `np.mean(array)`

  Sum                                 `np.sum(array, axis=...)`

  Maximum index                       `np.argmax(array)`

  Boolean filter                      `array[array > threshold]`

  Any condition                       `np.any(condition, axis=...)`

  Vectorization                       Apply operations to arrays without explicit
                                      element loops

  Broadcasting                        Dimensions must match or one dimension must be
                                      `1`
  ----------------------------------------------------------------------------------

------------------------------------------------------------------------

## Suggested study method

1.  Learn the definitions, array shapes, and the difference between
    `arange()` and `linspace()`.
2.  Draw the index grid for every 2D indexing/slicing question.
3.  Practise `shape`, `ndim`, `size`, and `axis` until they are clear.
4.  Run the examples in Python and check outputs; pay particular
    attention to slicing and broadcasting.
5.  Practise the sales-data case study from scratch because it combines
    array creation, aggregation, `axis`, `argmax`, percentages, and
    Boolean checks.

**Scope note:** The core topics are taken from the supplied 80-page
*NumPy_1_sem 3.pdf*. Examples and explanations have been reorganised for
clarity; supplementary clarifications (such as view/copy behaviour and
`default_rng`) are marked through context and should be distinguished
from the original lecture slide wording if your exam expects a
slide-specific definition.
