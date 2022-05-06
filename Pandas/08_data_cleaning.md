---
id: 08_data_cleaning
title: Data Cleaning
sidebar_label: Data Cleaning
slug: /08_data_cleaning
---

---


### Cleaning Empty Cells

In Pandas DataFrame, you may face some empty cells, which can cause some wrong results. Therefore, modifying these cells is so important in data analysis. There are various methods to deal with them, and using which way depends on several factors such as the number of data rows, number of empty cells in each row, etc.

#### Removing rows
One way of cleaning empty cells is by removing the whole row where those cells are located. Here, we can apply `df.dropna()` function.

- `df.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)`: removes missing values and returns DataFrame with `NA` entries dropped from it or None if `inplace` is True.
  - `axis`: {0 or 'index', 1 or 'columns'}. Determine if rows or columns which contain missing values are removed.
  - `how`: {'any', 'all'}. Determine if row or column is removed from DataFrame, when we have at least one NA or all NA.
  - `thresh`: int (optional). Require that many non-NA values.
  - subset: array-like (optional). Labels along other axis to consider, e.g. if you are dropping rows these would be a list of columns to include.
  - `inplace`: bool. If True, do operation inplace and return None.

```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

df.dropna(inplace=True)

print("\n New DataFrame:\n",df)



(output):
The whole DataFrame:
     Student NO   Age  Weight  Height
0        24353  20.0    78.0   180.0
1        43452  21.0    80.0     NaN
2        12643  24.0    60.0   160.0
3        65343   NaN    70.0   179.0
4        64345  21.0    73.0   177.0
5        97654  22.0     NaN   181.0
6        34543  26.0    91.0   180.0
7        23523  20.0    68.0   174.0
8        74555  19.0    59.0   164.0
9        75343  25.0     NaN   167.0
10       85454  24.0    77.0   177.0
11       33455   NaN    66.0   159.0
12       63784  21.0    79.0   167.0

 New DataFrame:
     Student NO   Age  Weight  Height
0        24353  20.0    78.0   180.0
2        12643  24.0    60.0   160.0
4        64345  21.0    73.0   177.0
6        34543  26.0    91.0   180.0
7        23523  20.0    68.0   174.0
8        74555  19.0    59.0   164.0
10       85454  24.0    77.0   177.0
12       63784  21.0    79.0   167.0
```

#### Replace empty cells
Another way is to replace the empty cells with values. Here, we can apply `df.fillna()` function.

- `df.fillna(value=None, method=None, axis=None, inplace=False, limit=None, downcast=None)`: fills `NA/NaN` values using the specified method.
  - `value`: scalar, dict, Series, or DataFrame. Value to use to fill holes.
  - `method`: {'backfill', 'bfill', 'pad', 'ffill', None}. Method to use for filling holes in reindexed Series.
    - pad / ffill: propagate last valid observation forward to next valid
    - backfill / bfill: use next valid observation to fill gap.
  - `axis`: {0 or 'index', 1 or 'columns'}. Axis along which to fill missing values.
  - `inplace`: bool. If True, fill in-place.
  - `limit`: int. If method is specified, this is the maximum number of consecutive `NaN` values to forward/backward fill. In other words, if there is a gap with more than this number of consecutive `NaNs`, it will only be partially filled. If method is not specified, this is the maximum number of entries along the entire axis where `NaNs` will be filled.
  - `downcast`: dict. A dict of item->dtype of what to downcast if possible, or the string 'infer' which will try to downcast to an appropriate equal type.


###### Replace with values
Here, the missing data is filled with value(s).

```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

df.fillna(100, inplace=True)
print('\nNew DataFrame:\n', df)



(output):
The whole DataFrame:
     Student NO   Age  Weight  Height
0        24353  20.0    78.0   180.0
1        43452  21.0    80.0     NaN
2        12643  24.0    60.0   160.0
3        65343   NaN    70.0   179.0
4        64345  21.0    73.0   177.0
5        97654  22.0     NaN   181.0
6        34543  26.0    91.0   180.0
7        23523  20.0    68.0   174.0
8        74555  19.0    59.0   164.0
9        75343  25.0     NaN   167.0
10       85454  24.0    77.0   177.0
11       33455   NaN    66.0   159.0
12       63784  21.0    79.0   167.0

New DataFrame:
     Student NO    Age  Weight  Height
0        24353   20.0    78.0   180.0
1        43452   21.0    80.0   100.0
2        12643   24.0    60.0   160.0
3        65343  100.0    70.0   179.0
4        64345   21.0    73.0   177.0
5        97654   22.0   100.0   181.0
6        34543   26.0    91.0   180.0
7        23523   20.0    68.0   174.0
8        74555   19.0    59.0   164.0
9        75343   25.0   100.0   167.0
10       85454   24.0    77.0   177.0
11       33455  100.0    66.0   159.0
12       63784   21.0    79.0   167.0
```

###### Replace only for a specified Columns
It is even possible to fill the empty cells of specified columns.

```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

df['Age'].fillna(20, inplace=True)
print('\nNew DataFrame:\n', df)


(output):
The whole DataFrame:
     Student NO   Age  Weight  Height
0        24353  20.0    78.0   180.0
1        43452  21.0    80.0     NaN
2        12643  24.0    60.0   160.0
3        65343   NaN    70.0   179.0
4        64345  21.0    73.0   177.0
5        97654  22.0     NaN   181.0
6        34543  26.0    91.0   180.0
7        23523  20.0    68.0   174.0
8        74555  19.0    59.0   164.0
9        75343  25.0     NaN   167.0
10       85454  24.0    77.0   177.0
11       33455   NaN    66.0   159.0
12       63784  21.0    79.0   167.0

New DataFrame:
     Student NO   Age  Weight  Height
0        24353  20.0    78.0   180.0
1        43452  21.0    80.0     NaN
2        12643  24.0    60.0   160.0
3        65343  20.0    70.0   179.0
4        64345  21.0    73.0   177.0
5        97654  22.0     NaN   181.0
6        34543  26.0    91.0   180.0
7        23523  20.0    68.0   174.0
8        74555  19.0    59.0   164.0
9        75343  25.0     NaN   167.0
10       85454  24.0    77.0   177.0
11       33455  20.0    66.0   159.0
12       63784  21.0    79.0   167.0
```

###### Replace using Mean, Median or Mode
Another important way of filling empty cells is to use Mean, Median or Mode. This method is widely used in Data analysis.

```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

age_filling = df['Age'].mean()
weight_filling = df['Weight'].median()
height_filling = df['Height'].mode()

print('\n Mean of Age: ', age_filling)
print('\n Median of Weight: ', weight_filling)
print('\n Mode of Height: ', height_filling)

df['Age'].fillna(age_filling, inplace=True)
df['Weight'].fillna(weight_filling, inplace=True)
df['Height'].fillna(height_filling, inplace=True)

print('\nNew DataFrame:\n', df)



(output):
The whole DataFrame:
     Student NO   Age  Weight  Height
0        24353  20.0    78.0   180.0
1        43452  21.0    80.0     NaN
2        12643  24.0    60.0   160.0
3        65343   NaN    70.0   179.0
4        64345  21.0    73.0   177.0
5        97654  22.0     NaN   181.0
6        34543  26.0    91.0   180.0
7        23523  20.0    68.0   174.0
8        74555  19.0    59.0   164.0
9        75343  25.0     NaN   167.0
10       85454  24.0    77.0   177.0
11       33455   NaN    66.0   159.0
12       63784  21.0    79.0   167.0

 Mean of Age:  22.09090909090909

 Median of Weight:  73.0

 Mode of Height:  0    167.0
1    177.0
2    180.0
dtype: float64

New DataFrame:
     Student NO        Age  Weight  Height
0        24353  20.000000    78.0   180.0
1        43452  21.000000    80.0   177.0
2        12643  24.000000    60.0   160.0
3        65343  22.090909    70.0   179.0
4        64345  21.000000    73.0   177.0
5        97654  22.000000    73.0   181.0
6        34543  26.000000    91.0   180.0
7        23523  20.000000    68.0   174.0
8        74555  19.000000    59.0   164.0
9        75343  25.000000    73.0   167.0
10       85454  24.000000    77.0   177.0
11       33455  22.090909    66.0   159.0
12       63784  21.000000    79.0   167.0
```


### Cleaning Data in Wrong Format
Sometimes, we are faced with the wrong format in our DataFrame. For example, this may happen for those columns which are defined for Date and Time. There are two main ways to deal with this issue, one is removing the row, and the other is converting the available data.


#### Convert into a correct format
There is a function which can help us to convert a value to date and time.

- `pandas.to_datetime(arg, errors='raise', dayfirst=False, yearfirst=False, utc=None, format=None, exact=True, unit=None, infer_datetime_format=False, origin='unix', cache=True)`: converts argument to datetime.
  - `arg`: int, float, str, datetime, list, tuple, 1-d array, Series, DataFrame/dict-like. The object to convert to a datetime.
  - `errors`: {'ignore', 'raise', 'coerce'}.
    - If 'raise', then invalid parsing will raise an exception.
    - If 'coerce', then invalid parsing will be set as NaT.
    - If 'ignore', then invalid parsing will return the input.
  - `dayfirst`: bool. Specify a date parse order if `arg` is str or its list-likes.
    If True, parses dates with the day first.
  - `yearfirst`: bool. Specify a date parse order if `arg` is str or its list-likes. If True parses dates with the year first. If both dayfirst and yearfirst are True, yearfirst is preceded.
  - `utc`: bool. Return UTC DatetimeIndex if True.
  - `format`: str. The strftime to parse time, eg "%d/%m/%Y".
  - `exact`: bool. Behaves as:
    - If True, require an exact format match.
    - If False, allow the format to match anywhere in the target string.
  - `unit`: str. The unit of the arg.
  - `infer_datetime_format`: bool. If True and no `format` is given, attempt to infer the format of the datetime strings based on the first non-NaN element, and if it can be inferred, switch to a faster method of parsing them.
  - `origin`: scalar. Define the reference date.
  - `cache`: bool. If True, use a cache of unique, converted dates to apply the datetime conversion.

```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

df['BirthDate'] = pd.to_datetime(df['BirthDate'])
print('\nThe New DataFrame:\n:', df)


(output):
The whole DataFrame:
     Student NO  BirthDate
0        24353  5/23/1989
1        43452  4/12/1988
2        12643  12/2/1990
3        64345   7/4/1989
4        97654  3/10/1991
5        34543        NaN
6        23523  7/22/1990
7        74555  1/12/1993
8        75343   2/1/1989
9        85454  3/17/1988
10       33455  1/16/1987
11       63784  2/12/1986

The New DataFrame:
:     Student NO  BirthDate
0        24353 1989-05-23
1        43452 1988-04-12
2        12643 1990-12-02
3        64345 1989-07-04
4        97654 1991-03-10
5        34543        NaT
6        23523 1990-07-22
7        74555 1993-01-12
8        75343 1989-02-01
9        85454 1988-03-17
10       33455 1987-01-16
11       63784 1986-02-12
```


### Cleaning Wrong Data
In a DataFrame, some data may be wrong. For example, instead of putting 177 for the height column, we specify 17.7. This incorrect data whether can be replaced, or its row can be removed.

#### Replacing values
One way is to replace a value with correct one.

```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

df.loc[6, 'Weight'] = 91
df.loc[0, 'Height'] = 180
df.loc[10, 'Height'] = 170

print('\nThe New DataFrame:\n', df)



(output):
The whole DataFrame:
     Student NO  Age  Weight  Height
0        24353   20      78    18.0
1        43452   21      80   165.0
2        12643   24      60   160.0
3        65343   23      70   179.0
4        64345   21      73   177.0
5        97654   22      90   181.0
6        34543   26       9   180.0
7        23523   20      68   174.0
8        74555   19      59   164.0
9        75343   25      83   167.0
10       85454   24      77    17.7
11       33455   24      66   159.0
12       63784   21      79   167.0

The New DataFrame:
     Student NO  Age  Weight  Height
0        24353   20      78   180.0
1        43452   21      80   165.0
2        12643   24      60   160.0
3        65343   23      70   179.0
4        64345   21      73   177.0
5        97654   22      90   181.0
6        34543   26      91   180.0
7        23523   20      68   174.0
8        74555   19      59   164.0
9        75343   25      83   167.0
10       85454   24      77   170.0
11       33455   24      66   159.0
12       63784   21      79   167.0
```

#### removing rows
The other way is to remove the whole row.

- `df.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')`: removes rows or columns by specifying label names and corresponding
axis, or by specifying directly index or column names.
  - `labels`: single label or list-like. Index or column labels to drop.
  - `axis`: {0 or 'index', 1 or 'columns'}. Whether to drop labels from the index or
    columns.
  -  `index`: single label or list-like. Alternative to specifying axis.
  - `columns`: single label or list-like. Alternative to specifying axis.
  - `level`: int or level name (optional). For MultiIndex, level from which the labels will be removed.
  - `inplace`: bool. If False, return a copy. Otherwise, do operation inplace and return None.
  - `errors` : {'ignore', 'raise'}.


```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

for i in df.index:        
    if df.loc[i , 'Height'] < 140:
        df.drop(i, inplace=True)

print('\nThe New DataFrame:\n', df)



(output):
The whole DataFrame:
     Student NO  Age  Weight  Height
0        24353   20      78    18.0
1        43452   21      80   165.0
2        12643   24      60   160.0
3        65343   23      70   179.0
4        64345   21      73   177.0
5        97654   22      90   181.0
6        34543   26      91   180.0
7        23523   20      68   174.0
8        74555   19      59   164.0
9        75343   25      83   167.0
10       85454   24      77    17.7
11       33455   24      66   159.0
12       63784   21      79   167.0

The New DataFrame:
     Student NO  Age  Weight  Height
1        43452   21      80   165.0
2        12643   24      60   160.0
3        65343   23      70   179.0
4        64345   21      73   177.0
5        97654   22      90   181.0
6        34543   26      91   180.0
7        23523   20      68   174.0
8        74555   19      59   164.0
9        75343   25      83   167.0
11       33455   24      66   159.0
12       63784   21      79   167.0
```

### Removing Duplications
Sometimes, we may face duplicated data in a DataFrame. First, the duplicated items should be discovered to deal with this issue, then they are removed.


- `df.duplicated(subset=None, keep='first')`: returns boolean Series denoting duplicate rows.
  - `subset` : column label or sequence of labels (optional). Only consider certain columns for identifying duplicates, by default use all of the columns.
  - `keep`: {'first', 'last', False}. Determines which duplicates (if any) to mark.

- `df.drop_duplicates(subset=None, keep='first', inplace=False, ignore_index=False)`: returns DataFrame with duplicate rows removed.
  - `subset` : column label or sequence of labels (optional). Only consider certain columns for identifying duplicates, by default use all of the columns.
  - `keep`: {'first', 'last', False}. Determines which duplicates (if any) to mark.
  - `inplace`: bool. Whether to drop duplicates in place or to return a copy.
  - `ignore_index`: bool. If True, the resulting axis will be labeled 0, 1, …, n - 1.


```
import pandas as pd

df = pd.read_csv('dirtydata.csv')
print('The whole DataFrame:\n', df)

print('\nDuplicated indices:\n', df.duplicated())

df.drop_duplicates(inplace=True, ignore_index=True)
print('\nThe New DataFrame:\n', df)



(output):
The whole DataFrame:
     Student NO  Age  Weight  Height
0        24353   20      78     180
1        43452   21      80     165
2        12643   24      60     160
3        65343   23      70     179
4        64345   21      73     177
5        97654   22      90     181
6        34543   26      91     180
7        43452   21      80     165
8        74555   19      59     164
9        75343   25      83     167
10       64345   21      73     177
11       33455   24      66     159
12       64345   21      73     177

Duplicated indices:
 0     False
1     False
2     False
3     False
4     False
5     False
6     False
7      True
8     False
9     False
10     True
11    False
12     True
dtype: bool

The New DataFrame:
    Student NO  Age  Weight  Height
0       24353   20      78     180
1       43452   21      80     165
2       12643   24      60     160
3       65343   23      70     179
4       64345   21      73     177
5       97654   22      90     181
6       34543   26      91     180
7       74555   19      59     164
8       75343   25      83     167
9       33455   24      66     159
```
