# Pandas --- Complete Study Notes with Examples and Diagrams

**Course:** M.Sc. Computer Applications --- Python\
**Source:** Uploaded *pandas.pdf* (72 pages)\
**Purpose:** Lecture-aligned study notes for concepts, practicals, and
exam revision.

> The notes follow the uploaded PDF's Pandas topics. The PDF's final
> pages also include Python magic methods; these are separated into an
> appendix. Outdated examples are explained with modern equivalents
> where necessary.

## Contents

1.  Introduction to Pandas
2.  Installation and Import
3.  Pandas Data Structures
4.  Series
5.  DataFrame
6.  Selecting and Modifying Data
7.  Indexing: `loc` and `iloc`
8.  Rows: Adding and Deleting
9.  Attributes
10. Basic Inspection Methods
11. Descriptive Statistics
12. Missing Data
13. Practical Case Study
14. Practice Programs
15. Exam Questions and Quick Revision
16. Appendix: Python Magic Methods

------------------------------------------------------------------------

# 1. Introduction to Pandas

**Pandas** is an open-source Python library used for data manipulation
and analysis. It provides labelled data structures and functions that
help us organise, inspect, clean, transform, and analyse structured
data.

### Common uses

-   Read CSV, Excel, JSON, and SQL data.
-   Select rows and columns.
-   Filter, sort, and transform records.
-   Detect and handle missing values.
-   Calculate statistics and aggregate data.
-   Prepare data for visualisation and machine learning.

### Why use Pandas?

Suppose a college stores student details in a spreadsheet. Pandas can
calculate average marks, select students scoring above 80, find missing
marks, and group results by class.

``` text
CSV / Excel / Database
          |
          v
     Read with Pandas
          |
          v
    Inspect and clean
          |
          v
 Select / filter / transform
          |
          v
 Statistics and analysis
          |
          v
    Reports / ML models
```

Pandas works well with NumPy, Matplotlib, and scikit-learn.

# 2. Installation and Import

Install Pandas from the terminal:

``` bash
python -m pip install pandas
```

Import it using the conventional alias `pd`:

``` python
import pandas as pd
import numpy as np
```

Check the installed version:

``` python
print(pd.__version__)
```

`pd` is a conventional alias; it is not mandatory.

# 3. Pandas Data Structures

The lecture PDF mentions Series, DataFrame, and Panel. In modern Pandas,
**Series** and **DataFrame** are the main data structures. The old
`Panel` structure was deprecated and removed from modern Pandas.

  ------------------------------------------------------------------------
  Structure                               Dimensions Description
  --------------------- ---------------------------- ---------------------
  Series                                          1D Labelled sequence of
                                                     values

  DataFrame                                       2D Labelled rows and
                                                     columns

  Panel                               3D, historical Old structure; not
                                                     available in modern
                                                     Pandas
  ------------------------------------------------------------------------

## 3.1 Series

A **Series** is a one-dimensional labelled array. It contains values and
an index label for each value.

-   One-dimensional.
-   Usually stores values of one common data type.
-   Values can be changed.
-   A Series has an index associated with its values.

Diagram:

``` text
Index (labels)     Values
     0                10
     1                23
     2                56
     3                17

A Series combines an index with a sequence of values.
```

Example:

``` python
import pandas as pd

s = pd.Series([10, 23, 56, 17])
print(s)
```

Output:

``` text
0    10
1    23
2    56
3    17
dtype: int64
```

## 3.2 DataFrame

A **DataFrame** is a two-dimensional labelled table. Different columns
can contain different data types.

``` python
df = pd.DataFrame({
    "Name": ["Steve", "Lia", "Vin", "Katie"],
    "Age": [32, 28, 45, 38],
    "Gender": ["Male", "Female", "Male", "Female"],
    "Rating": [3.45, 4.60, 3.90, 2.78]
})
print(df)
```

Conceptual diagram:

``` text
          Columns
        Name     Age    Gender    Rating
Row 0   Steve     32     Male       3.45
Row 1   Lia       28     Female     4.60
Row 2   Vin       45     Male       3.90
Row 3   Katie     38     Female     2.78
          |         |       |          |
        string   integer  string     float
```

-   Each row commonly represents one record.
-   Each column represents one attribute.
-   Index labels identify rows; column names identify columns.

## 3.3 Series vs DataFrame

  -----------------------------------------------------------------------
  Feature                 Series                  DataFrame
  ----------------------- ----------------------- -----------------------
  Dimensions              1D                      2D

  Example shape           `(4,)`                  `(4, 3)`

  Structure               Labelled sequence       Labelled table

  Data types              One Series dtype        Each column may have a
                                                  different dtype

  Example                 One marks column        Complete student table
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 4. Creating a Series

General constructor:

``` python
pd.Series(data=None, index=None, dtype=None, copy=None)
```

-   `data`: list, array, dictionary, scalar, or other supported input.
-   `index`: labels for the values.
-   `dtype`: optional data type.
-   `copy`: whether input data should be copied.

## 4.1 From a list

``` python
s = pd.Series([10, 20, 30, 40])
print(s)
```

Output:

``` text
0    10
1    20
2    30
3    40
dtype: int64
```

If no index is provided, Pandas creates default integer labels beginning
at zero.

## 4.2 From a NumPy array

``` python
import numpy as np

data = np.array(["a", "b", "c", "d"])
s = pd.Series(data)
print(s)
```

Output:

``` text
0    a
1    b
2    c
3    d
dtype: object
```

Custom index:

``` python
s = pd.Series(data, index=[100, 101, 102, 103])
print(s)
```

The number of index labels must match the number of values.

## 4.3 From a dictionary

Dictionary keys become index labels.

``` python
data = {"a": 0.0, "b": 1.0, "c": 2.0}
s = pd.Series(data)
print(s)
```

Output:

``` text
a    0.0
b    1.0
c    2.0
dtype: float64
```

Request a different order or an additional label:

``` python
s = pd.Series(data, index=["b", "c", "d", "a"])
print(s)
```

Output:

``` text
b    1.0
c    2.0
d    NaN
a    0.0
dtype: float64
```

`d` was not present in the dictionary, so its value becomes `NaN`
(missing).

## 4.4 From a scalar

A scalar is repeated to match the supplied index length.

``` python
s = pd.Series(5, index=[0, 1, 2, 3])
print(s)
```

Output:

``` text
0    5
1    5
2    5
3    5
dtype: int64
```

## 4.5 Empty Series

Prefer specifying the dtype for an empty Series:

``` python
s = pd.Series(dtype="float64")
print(s)
```

Output:

``` text
Series([], dtype: float64)
```

# 5. Accessing Series Data

Example Series:

``` python
s = pd.Series([1, 2, 3, 4, 5], index=["a", "b", "c", "d", "e"])
```

## 5.1 Positional selection with `iloc`

`iloc` uses integer positions, starting at zero.

``` python
print(s.iloc[0])      # 1
print(s.iloc[2])      # 3
print(s.iloc[-1])     # 5
print(s.iloc[:3])     # first three values
print(s.iloc[-3:])    # last three values
```

## 5.2 Label selection with `loc`

`loc` uses index labels.

``` python
print(s.loc["a"])                # 1
print(s.loc[["a", "c", "d"]])    # multiple labels
```

A missing requested label generally raises `KeyError`.

## 5.3 `loc` vs `iloc`

  Method   Basis              Example
  -------- ------------------ --------------
  `loc`    Index label        `s.loc["b"]`
  `iloc`   Integer position   `s.iloc[1]`

Important: label-based slices generally include the stop label;
positional slices exclude the stop position. For example, `s.iloc[:3]`
returns positions 0, 1, and 2.

------------------------------------------------------------------------

# 6. Creating a DataFrame

General constructor:

``` python
pd.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)
```

Data may be supplied as lists, dictionaries, Series, NumPy arrays, or
another DataFrame.

## 6.1 Empty DataFrame

``` python
df = pd.DataFrame()
print(df)
```

Output:

``` text
Empty DataFrame
Columns: []
Index: []
```

## 6.2 From a list of values

``` python
df = pd.DataFrame([1, 2, 3, 4, 5])
print(df)
```

Pandas creates one column with default name `0`.

## 6.3 From a list of lists

``` python
data = [["Alex", 10], ["Bob", 12], ["Clarke", 13]]
df = pd.DataFrame(data, columns=["Name", "Age"])
print(df)
```

Output:

``` text
     Name  Age
0    Alex   10
1     Bob   12
2  Clarke   13
```

Custom index:

``` python
df = pd.DataFrame(
    data,
    columns=["Name", "Age"],
    index=["student1", "student2", "student3"]
)
```

## 6.4 From a dictionary of lists

``` python
data = {
    "Name": ["Tom", "Jack", "Steve", "Ricky"],
    "Age": [28, 34, 29, 42]
}
df = pd.DataFrame(data)
print(df)
```

Output:

``` text
    Name  Age
0    Tom   28
1   Jack   34
2  Steve   29
3  Ricky   42
```

Each dictionary key becomes a column name. Column lists must have
compatible lengths.

## 6.5 From a list of dictionaries

``` python
data = [
    {"a": 1, "b": 2},
    {"a": 5, "b": 10, "c": 20}
]
df = pd.DataFrame(data)
print(df)
```

Output:

``` text
   a   b     c
0  1   2   NaN
1  5  10  20.0
```

A missing key becomes a missing value.

## 6.6 From a dictionary of Series

Pandas aligns values by index labels and uses the union of the indexes.

``` python
data = {
    "one": pd.Series([1, 2, 3], index=["a", "b", "c"]),
    "two": pd.Series([1, 2, 3, 4], index=["a", "b", "c", "d"])
}
df = pd.DataFrame(data)
print(df)
```

Output:

``` text
   one  two
a  1.0    1
b  2.0    2
c  3.0    3
d  NaN    4
```

Diagram:

``` text
Series one: a -> 1, b -> 2, c -> 3
Series two: a -> 1, b -> 2, c -> 3, d -> 4
                     |
                     v
          Align values by index labels
                     |
                     v
d: one = NaN, two = 4
```

------------------------------------------------------------------------

# 7. Selecting and Modifying Columns

## 7.1 Select one column

``` python
df = pd.DataFrame({
    "Name": ["Tom", "Jack", "Steve"],
    "Age": [28, 34, 29]
})

print(df["Name"])
```

Selecting one column generally returns a Series.

## 7.2 Select multiple columns

``` python
print(df[["Name", "Age"]])
```

Double square brackets select multiple columns and return a DataFrame.

## 7.3 Add a new column

``` python
df["City"] = ["Pune", "Jaipur", "Pune"]
df["AgeNextYear"] = df["Age"] + 1
print(df)
```

## 7.4 Assign a Series to a DataFrame

``` python
df = pd.DataFrame({"one": [1, 2, 3]}, index=["a", "b", "c"])
extra = pd.Series([10, 20], index=["a", "c"])

df["three"] = extra
print(df)
```

Output:

``` text
   one  three
a    1   10.0
b    2    NaN
c    3   20.0
```

Pandas aligns by index label, not merely by row position.

## 7.5 Delete a column

``` python
del df["one"]
```

Or:

``` python
removed = df.pop("three")
```

`del` removes the column. `pop()` removes it and returns its values as a
Series.

------------------------------------------------------------------------

# 8. Selecting Rows with `loc`, `iloc`, and Slicing

## 8.1 `loc` --- label-based selection

``` python
df = pd.DataFrame(
    {"one": [1, 2, 3], "two": [1, 2, 3]},
    index=["a", "b", "c"]
)

print(df.loc["b"])
```

## 8.2 `iloc` --- position-based selection

``` python
print(df.iloc[2])       # third row
print(df.iloc[0, 1])    # first row, second column
```

## 8.3 Select multiple rows

``` python
df = pd.DataFrame({
    "Name": ["Alex", "Bob", "Clarke", "Dia"],
    "Age": [10, 12, 13, 14]
})

print(df.iloc[1:3])
```

Output:

``` text
     Name  Age
1     Bob   12
2  Clarke   13
```

Diagram:

``` text
Index 0 -> Alex
Index 1 -> Bob       <- included
Index 2 -> Clarke    <- included
Index 3 -> Dia       <- stop position, excluded

df.iloc[1:3] returns rows at positions 1 and 2.
```

------------------------------------------------------------------------

# 9. Adding and Deleting Rows

The lecture PDF uses `DataFrame.append()`. This method was removed in
Pandas 2.0; use `pd.concat()` in modern Pandas.

## 9.1 Add rows using `concat()`

``` python
df1 = pd.DataFrame([[1, 2], [3, 4]], columns=["a", "b"])
df2 = pd.DataFrame([[5, 6], [7, 8]], columns=["a", "b"])

combined = pd.concat([df1, df2], ignore_index=True)
print(combined)
```

Output:

``` text
   a  b
0  1  2
1  3  4
2  5  6
3  7  8
```

`ignore_index=True` resets the result to a fresh sequential index.

## 9.2 Delete rows with `drop()`

``` python
df = pd.DataFrame(
    {"a": [1, 3, 5], "b": [2, 4, 6]},
    index=[0, 1, 2]
)

df = df.drop(0)
print(df)
```

`drop(0)` removes the row with index label `0`, not necessarily the
first row by position.

------------------------------------------------------------------------

# 10. Important Pandas Attributes

Attributes provide information about a Series or DataFrame.

  Attribute   Description
  ----------- -----------------------------------------------
  `dtype`     Data type of a Series
  `dtypes`    Data type of each DataFrame column
  `index`     Row/index labels
  `values`    Underlying values as an array-like object
  `shape`     Shape tuple; DataFrame uses `(rows, columns)`
  `ndim`      Number of dimensions
  `size`      Total number of elements
  `empty`     `True` if the object has no items
  `columns`   Column labels of a DataFrame

Example:

``` python
df = pd.DataFrame({
    "Name": ["Tom", "James", "Ricky"],
    "Age": [25, 26, 25],
    "Rating": [4.23, 3.24, 3.98]
})

print("Data types:\n", df.dtypes)
print("Index:", df.index)
print("Columns:", df.columns)
print("Values:\n", df.values)
print("Shape:", df.shape)       # (3, 3)
print("Dimensions:", df.ndim)   # 2
print("Total elements:", df.size)  # 9
print("Is empty:", df.empty)    # False
```

Remember: use `df.dtypes` for a DataFrame, but `s.dtype` for a Series.

------------------------------------------------------------------------

# 11. Basic Inspection Methods

## 11.1 `head(n)`

Returns the first `n` rows; default is 5.

``` python
df.head()
df.head(3)
```

## 11.2 `tail(n)`

Returns the last `n` rows; default is 5.

``` python
df.tail()
df.tail(2)
```

## 11.3 `info()`

Displays a concise summary of the DataFrame, including columns, non-null
counts, data types, and memory usage.

``` python
df.info()
```

## 11.4 `describe()`

Generates descriptive statistics for selected columns.

``` python
print(df.describe())
print(df.describe(include="all"))
```

For numeric columns, statistics commonly include count, mean, standard
deviation, minimum, quartiles, and maximum. `include="all"` also
requests summaries of non-numeric columns where supported.

------------------------------------------------------------------------

# 12. Descriptive Statistics

The lecture PDF introduces the following functions:

  Function      Purpose
  ------------- --------------------------------
  `count()`     Count non-missing observations
  `sum()`       Sum values
  `mean()`      Arithmetic mean
  `median()`    Median
  `mode()`      Most frequent value(s)
  `std()`       Standard deviation
  `min()`       Minimum
  `max()`       Maximum
  `abs()`       Absolute values
  `prod()`      Product
  `cumsum()`    Cumulative sum
  `cumprod()`   Cumulative product

Example:

``` python
df = pd.DataFrame({
    "Name": ["Tom", "James", "Ricky", "Vin"],
    "Age": [25, 26, 25, 23],
    "Rating": [4.23, 3.24, 3.98, 2.56]
})

print("Mean age:", df["Age"].mean())
print("Minimum rating:", df["Rating"].min())
print("Maximum rating:", df["Rating"].max())
print("Median rating:", df["Rating"].median())
print("Count:", df["Age"].count())
print("Cumulative sum:\n", df["Age"].cumsum())
```

Pandas `Series.std()` uses sample standard deviation by default
(`ddof=1`), unlike NumPy's default `np.std()` (`ddof=0`).

------------------------------------------------------------------------

# 13. Missing Data

## 13.1 What is missing data?

Missing data occurs when a value has not been recorded or is
unavailable. It may appear as `NaN`, `None`, or another missing-value
marker depending on the data type.

``` text
Raw Data
+---------+-----+-------+
| Student | Age | Marks |
+---------+-----+-------+
| A       | 21  | 78    |
| B       | NaN | 85    |
| C       | 22  | NaN   |
+---------+-----+-------+
           |
           v
   Detect missing values
           |
      +----+-----+
      |          |
      v          v
    Fill       Drop
      |          |
      +----+-----+
           |
           v
   Prepared data for analysis
```

## 13.2 Create missing values using `reindex()`

``` python
df = pd.DataFrame(
    {"one": [1.0, 3.0, 5.0], "two": [2.0, 4.0, 6.0]},
    index=["a", "c", "e"]
)

df = df.reindex(["a", "b", "c", "d", "e"])
print(df)
```

Labels `b` and `d` did not exist, so the newly introduced values are
missing.

## 13.3 Detect missing values

``` python
print(df["one"].isnull())
print(df["one"].notnull())
print(df.isna().sum())
```

-   `isnull()` / `isna()` identify missing values.
-   `notnull()` / `notna()` identify non-missing values.
-   `df.isna().sum()` counts missing values per column.

## 13.4 Fill missing values with a scalar

``` python
clean_df = df.fillna(0)
print(clean_df)
```

This replaces missing values with zero in the returned DataFrame. Zero
should only be used when it is a meaningful replacement.

## 13.5 Forward fill

The lecture uses `fillna(method="pad")`. The modern, clearer equivalent
is `.ffill()`.

``` python
df = pd.DataFrame({
    "A": [10, None, None, 40],
    "B": [1, 2, None, 4]
})

print(df.ffill())
```

Output:

``` text
      A    B
0  10.0  1.0
1  10.0  2.0
2  10.0  2.0
3  40.0  4.0
```

Forward fill uses the previous valid value in the same column.

## 13.6 Drop missing values

``` python
df.dropna()            # drop rows with at least one missing value
df.dropna(axis=1)      # drop columns with missing values
df.dropna(how="all")   # drop rows where all values are missing
```

These return new objects by default.

## 13.7 Choosing a strategy

  -----------------------------------------------------------------------
  Method                  Behaviour               Caution
  ----------------------- ----------------------- -----------------------
  `fillna(0)`             Replace missing values  Zero may be a real
                          with zero               measurement

  `fillna(mean)`          Replace with column     Can distort
                          mean                    distribution

  `ffill()`               Carry the previous      Best only when
                          value forward           meaningful for ordered
                                                  data

  `dropna()`              Remove rows with        Can discard useful
                          missing values          records

  `dropna(axis=1)`        Remove columns with     Can discard useful
                          missing values          variables
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 14. Practical Case Study: Student Marks Analysis

This program uses DataFrame creation, inspection, filtering, statistics,
missing-value treatment, and grouping.

``` python
import pandas as pd
import numpy as np

students = pd.DataFrame({
    "Name": ["Aarav", "Diya", "Kabir", "Meera", "Rohan"],
    "Age": [21, 22, 21, 23, 22],
    "Marks": [78, 91, np.nan, 67, 84],
    "City": ["Pune", "Pune", "Jaipur", "Pune", "Jaipur"]
})

print("First rows:")
print(students.head())

print("\nDataFrame structure:")
students.info()

print("\nMissing values:")
print(students.isna().sum())

print("\nStudents scoring above 80:")
print(students.loc[students["Marks"] > 80, ["Name", "Marks"]])

print("\nAverage available marks:")
print(students["Marks"].mean())

students["Marks"] = students["Marks"].fillna(students["Marks"].mean())

print("\nAverage marks by city:")
print(students.groupby("City")["Marks"].mean())
```

Workflow:

``` text
Create DataFrame
      |
      v
Inspect with head() and info()
      |
      v
Check missing values
      |
      v
Filter rows using a condition
      |
      v
Calculate statistics
      |
      v
Treat missing values if justified
      |
      v
Group and aggregate
```

`groupby()` is a useful extension to the PDF's introduction to grouping
and aggregation.

------------------------------------------------------------------------

# 15. Common Mistakes

1.  Confusing `loc` (labels) with `iloc` (positions).
2.  Assuming index labels always match row positions.
3.  Creating columns from lists of incompatible lengths.
4.  Forgetting that Series assignment aligns by index labels.
5.  Using the removed `DataFrame.append()` method; use `pd.concat()`.
6.  Using `df.dtype` rather than `df.dtypes`.
7.  Treating missing values as ordinary values instead of using
    `isna()`.
8.  Filling all missing values with zero without considering the meaning
    of the data.
9.  Confusing `shape`, `size`, and `ndim`.
10. Confusing methods such as `head()` with attributes such as `shape`.
11. Assuming an operation changed the original object when it returned a
    new one.
12. Forgetting that `describe()` normally summarises numeric columns by
    default.

------------------------------------------------------------------------

# 16. Practice Programs with Answers

## Program 1: Create a Series with custom labels

``` python
import pandas as pd

s = pd.Series([85, 90, 78], index=["A", "B", "C"])
print(s)
```

## Program 2: Create a DataFrame

``` python
data = {"Name": ["Asha", "Ravi", "Mina"], "Marks": [80, 75, 92]}
df = pd.DataFrame(data)
print(df)
```

## Program 3: Select a column

``` python
print(df["Marks"])
```

## Program 4: Select rows by label and position

``` python
print(df.loc[1])   # row whose label is 1, if it exists
print(df.iloc[1])  # second row by position
```

## Program 5: Filter marks of 80 or more

``` python
print(df.loc[df["Marks"] >= 80])
```

## Program 6: Add a result column

``` python
df["Result"] = ["Pass", "Pass", "Pass"]
print(df)
```

## Program 7: Calculate basic statistics

``` python
print("Mean:", df["Marks"].mean())
print("Minimum:", df["Marks"].min())
print("Maximum:", df["Marks"].max())
```

## Program 8: Count missing values

``` python
df = pd.DataFrame({"A": [1, None, 3], "B": [None, 5, 6]})
print(df.isna().sum())
```

Expected output:

``` text
A    1
B    1
dtype: int64
```

## Program 9: Fill missing values

``` python
print(df.fillna(0))
```

## Program 10: Combine DataFrames

``` python
df1 = pd.DataFrame({"A": [1, 2]})
df2 = pd.DataFrame({"A": [3, 4]})

result = pd.concat([df1, df2], ignore_index=True)
print(result)
```

## Program 11: Remove a column

``` python
df = pd.DataFrame({"A": [1, 2], "B": [3, 4]})
del df["A"]
print(df)
```

## Program 12: Remove rows with missing values

``` python
df = pd.DataFrame({
    "Name": ["A", "B", "C"],
    "Marks": [80, None, 90]
})
print(df.dropna())
```

------------------------------------------------------------------------

# 17. Exam and Viva Questions

## Short-answer questions

1.  What is Pandas? State its uses.
2.  Explain the Series and DataFrame data structures.
3.  Differentiate Series and DataFrame.
4.  How do you install and import Pandas?
5.  Explain the parameters of `pd.Series()`.
6.  Demonstrate Series creation from a list, NumPy array, dictionary,
    and scalar.
7.  What happens when a requested Series index is missing from a
    dictionary?
8.  Differentiate `loc` and `iloc`.
9.  Explain the `pd.DataFrame()` constructor.
10. List different ways to create a DataFrame.
11. How can you select one or multiple columns?
12. How do you add and delete a DataFrame column?
13. Explain `del` and `pop()`.
14. How can you add rows using modern Pandas?
15. Explain row deletion using `drop()`.
16. Explain the attributes `dtype`, `dtypes`, `index`, `values`,
    `shape`, `ndim`, `size`, `empty`, and `columns`.
17. Explain `head()`, `tail()`, `info()`, and `describe()`.
18. Explain `count()`, `sum()`, `mean()`, `median()`, `mode()`, and
    `std()`.
19. What are `cumsum()` and `cumprod()`?
20. Define missing data and explain its causes.
21. Explain `isnull()` and `notnull()`.
22. Explain `fillna()` with an example.
23. What is forward fill?
24. Compare filling and dropping missing values.

## Long-answer and practical questions

1.  Explain Pandas features and applications with a workflow diagram.
2.  Explain Series and DataFrame with code and outputs.
3.  Demonstrate four ways to create a Series.
4.  Demonstrate different methods of creating a DataFrame.
5.  Explain column selection, addition, and deletion.
6.  Explain row selection with `loc`, `iloc`, and slicing.
7.  Explain Pandas attributes with a suitable example.
8.  Demonstrate basic DataFrame inspection methods.
9.  Explain descriptive statistics using a DataFrame.
10. Explain missing-value detection and treatment.
11. Write a program to analyse student marks and handle missing values.

## Output-prediction questions

### Q1

``` python
s = pd.Series([10, 20, 30], index=["a", "b", "c"])
print(s.loc["b"])
print(s.iloc[0])
```

**Answer:** `20`, then `10`.

### Q2

``` python
df = pd.DataFrame({"Name": ["A", "B"], "Age": [20, 21]})
print(df.shape)
print(df.size)
```

**Answer:** `(2, 2)`, then `4`.

### Q3

``` python
df = pd.DataFrame({"Marks": [50, 70, 90]})
print(df["Marks"].mean())
```

**Answer:** `70.0`.

### Q4

``` python
df = pd.DataFrame({"A": [1, None, 3]})
print(df.isna().sum())
```

**Answer:** `A    1`.

### Q5

``` python
df = pd.DataFrame({"A": [1, None, 3]})
print(df.fillna(0))
```

**Answer:**

``` text
     A
0  1.0
1  0.0
2  3.0
```

------------------------------------------------------------------------

# 18. Quick Revision Sheet

  Topic                     Syntax / Reminder
  ------------------------- --------------------------------------------
  Import                    `import pandas as pd`
  Series                    `pd.Series([10, 20, 30])`
  Custom Series index       `pd.Series(values, index=["a", "b", "c"])`
  DataFrame                 `pd.DataFrame({"A": [1, 2], "B": [3, 4]})`
  Select column             `df["A"]`
  Select multiple columns   `df[["A", "B"]]`
  Label selection           `df.loc["row_label"]`
  Position selection        `df.iloc[0]`
  Add column                `df["C"] = values`
  Delete column             `del df["A"]` or `df.pop("A")`
  Combine rows              `pd.concat([df1, df2], ignore_index=True)`
  Delete rows               `df.drop([0, 2])`
  First rows                `df.head()`
  Last rows                 `df.tail()`
  Structure summary         `df.info()`
  Statistics                `df.describe()`
  Shape                     `df.shape` → `(rows, columns)`
  Column types              `df.dtypes`
  Count non-missing         `df["A"].count()`
  Mean                      `df["A"].mean()`
  Standard deviation        `df["A"].std()`
  Detect missing            `df.isna()` or `df.isnull()`
  Count missing             `df.isna().sum()`
  Fill missing              `df.fillna(0)`
  Forward fill              `df.ffill()`
  Drop missing rows         `df.dropna()`
  Cumulative sum            `df["A"].cumsum()`

------------------------------------------------------------------------

# 19. Source Alignment and Scope

These notes are based on the supplied *pandas.pdf*. The main topics
follow the lecture sequence: introduction and features; Series and
DataFrame creation; selecting and modifying columns and rows;
attributes; inspection methods; descriptive statistics; and missing-data
handling.

Modern-code clarifications: - `DataFrame.append()` has been removed in
Pandas 2.0; use `pd.concat()`. - `.ffill()` is used for forward fill. -
`Panel` is a historical structure, not a current Pandas data
structure. - The final six pages of the supplied PDF discuss Python
magic methods (`__add__`, `__new__`, `__init__`, and `__str__`), which
are general Python OOP topics rather than Pandas features.
