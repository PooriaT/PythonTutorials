---
id: 04_dataframes
title: Pandas DataFrames
sidebar_label: Pandas DataFrames
slug: /04_dataframes
---

---

A *Pandas DataFrames* is a two-dimensional dat structure same as 2D array (a table with rows and columns). Its size is mutable and it can contain heterogeneous data.

- `pandas.DataFrame(data=None, index=None, columns=None, dtype=None, copy=False)`: Two-dimensional, size-mutable, potentially heterogeneous tabular data. Data structure also contains labeled axes (rows and columns).
  - `data`: ndarray (structured or homogeneous), Iterable, dict, or DataFrame. Dict can contain Series, arrays, constants, dataclass or list-like objects. If data is a dict, column order follows insertion-order.
  - `index`: Index or array-like (optional). Index to use for resulting frame. If it is not provide, the default will be RangeIndex.
  - `columns`: Index or array-like (optional). Column labels to use for resulting frame. If it is not provide, the default will be (0, 1, 2, ..., n) range.
  - `dtype`: dtype (optional).
  - `copy`: bool. Copy data from inputs.

So, the input data can be
- Numpy ndarray
- Lists
- Dictionary
- Series
- even another DataFrame


```
import pandas as pd

### Creating Empty DataFrame
print("1- Creating Eempty DataFrame:\n")
empty_df = pd.DataFrame()
print(empty_df)

### Creating DataFrame from Lists
print("\n2- Creating DataFrame from lists:")

data_list = [1 ,2 , 'a', 10, 'ab']
df_1 = pd.DataFrame(data_list)
print("\n2.1:\n", df_1)

data_list = [['john', 'Sarah', 'Bob'], [72, 80, 78]]
df_1 = pd.DataFrame(data_list, index=['Name', 'Weight'])
print("\n2.2:\n", df_1)

data_list = [['John',72], ['Sarah',80], ['Bob',78]]
df_1 = pd.DataFrame(data_list, columns=['Name', 'Weight'])
print("\n2.2:\n", df_1)

### Creating DataFrame from Dict of lists or Ndarrays
print("\n3- Creating DataFrame from Dict of lists or Ndarrays:")
data_dict = {'Name': ['John', 'Sarah', 'Bob'], 'Weight': [72, 80, 78]}
df_2 = pd.DataFrame(data_dict)
print(df_2)

### Creating DataFrame from list of Dicts
print("\n4- Creating DataFrame from list of Dicts:")
data_listOfDict = [{'Math': 19, 'Physics': 17.5}, {'Math': 18.0, 'Physics': 13.0, 'Literature': 15}]
df_3 = pd.DataFrame(data_listOfDict, index=['Joe', 'Sarah'], dtype='float')
print(df_3)

### Creating DataFrame from Series
print("\n5- Creating DataFrame from Series:")
data_dictOfSeries = {'Joe': pd.Series([19, 17.5], index=['Math', 'Physics']) ,
                    'Sarah': pd.Series([18,13,15], index=['Math', 'Physics', 'Literature'])}
df_4 = pd.DataFrame(data_dictOfSeries)
print(df_4)



(output):
1- Creating Empty DataFrame:

Empty DataFrame
Columns: []
Index: []

2- Creating DataFrame from lists:

2.1:
     0
0   1
1   2
2   a
3  10
4  ab

2.2:
            0      1    2
Name    john  Sarah  Bob
Weight    72     80   78

2.2:
     Name  Weight
0   John      72
1  Sarah      80
2    Bob      78

3- Creating DataFrame from Dict of lists or Ndarrays:
    Name  Weight
0   John      72
1  Sarah      80
2    Bob      78

4- Creating DataFrame from list of Dicts:
       Math  Physics  Literature
Joe    19.0     17.5         NaN
Sarah  18.0     13.0        15.0

5- Creating DataFrame from Series:
             Joe  Sarah
Literature   NaN     15
Math        19.0     18
Physics     17.5     13
```


#### Row Selection, Addition, Deletion

- `df.loc[]`, `df.iloc[]` and slicing are user for row selection.
- `df.append()` is used for row addition.
- `df.drop()` is used for row deletion.


```
import pandas as pd

data = [{'a': 2, 'b': 4}, {'a': 1, 'b': 5, 'c':3}]
df = pd.DataFrame(data, index=['r1', 'r2'])
print(df)

# Selecting by label
print("\nSelecting the first row:\n", df.loc['r1'])

# Selecting by integer location
print("\nSelecting the second row:\n", df.iloc[1])

# Selecting by slicing:
print("\nSelecting the two rows:\n", df[0:2])

# Appending
new_data = [{'a': 6, 'c': 7}]
new_df = pd.DataFrame(new_data , index=['r3'])
print("\nRow Addition:\n", df.append(new_df))

# Row Deletion
print("\nDeleting the second row:\n", df.drop('r2'))



(output):
a  b    c
r1  2  4  NaN
r2  1  5  3.0

Selecting the first row:
a    2.0
b    4.0
c    NaN
Name: r1, dtype: float64

Selecting the second row:
a    1.0
b    5.0
c    3.0
Name: r2, dtype: float64

Selecting the two rows:
 a  b    c
r1  2  4  NaN
r2  1  5  3.0

Row Addition:
 a    b    c
r1  2  4.0  NaN
r2  1  5.0  3.0
r3  6  NaN  7.0

Deleting the second row:
 a  b   c
r1  2  4 NaN
```

#### Column Selection, Addition, Deletion

- `df[<Column Label>]` is used for column selection.
- `df[col1] + df[col2]` is used for addition.
- `del df[col]` or `df.pop(col)` can be used for column deletion.

```
import pandas as pd

data = [{'a': 2, 'b': 4}, {'a': 1, 'b': 5, 'c':3}]
df = pd.DataFrame(data, index=['r1', 'r2'])
print(df)

# Column Selection
print("\nColumn Selection:\n", df['a'])

# Column Addition
df['d'] = df['a'] + df['b']
print("\nColumn Addition:\n", df)

# Column Deletion
df.pop('c')
print("\nDeleting column c:\n", df)

del df['d']
print("\nDeleting column d:\n", df)



(output):
a  b    c
r1  2  4  NaN
r2  1  5  3.0

Column Selection:
r1    2
r2    1
Name: a, dtype: int64

Column Addition:
 a  b    c  d
r1  2  4  NaN  6
r2  1  5  3.0  6

Deleting column c:
 a  b  d
r1  2  4  6
r2  1  5  6

Deleting column d:
 a  b
r1  2  4
r2  1  5
```
