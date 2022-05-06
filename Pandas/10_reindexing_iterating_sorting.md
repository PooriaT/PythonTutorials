---
id: 10_reindexing_iterating_sorting
title: Reindexing, Iterating and Sorting
sidebar_label: Reindexing, Iterating and Sorting
slug: /10_reindexing_iterating_sorting
---

---

### Reindexing

Reindexing in Pandas means changing the index of rows and columns of a DataFrame. Below Functions can support us in reindexing or renaming the index.

- `df.reindex(labels=None, index=None, columns=None, axis=None, method=None, copy=True, level=None, fill_value=nan, limit=None)`:  conforms Series/DataFrame to new index with optional filling logic. Places NA/NaN in locations having no value in the previous index.
  - keywords for axes: array-like (optional). New labels / index to conform to, should be specified using keywords.
  - `method`: {None, 'backfill'/'bfill', 'pad'/'ffill', 'nearest'}. Method to use for filling holes in reindexed DataFrame.
    * `None` (default): don't fill gaps
    * `pad / ffill`: Propagate last valid observation forward to next valid.
    * `backfill / bfill`: Use next valid observation to fill gap.
    * `nearest`: Use nearest valid observations to fill gap.
  - `copy`: bool. it returns a new object, even if the passed indexes are the same.
  - `level`: int or name. it broadcasts across a level, matching Index values on the passed MultiIndex level.
  - `fill_value`: scalar, default np.NaN. Value to use for missing values. D
  - `limit`: int. Maximum number of consecutive elements to forward or backward fill.


- `df.reindex_like(other, method=None, copy=True, limit=None)`: returns an object with matching indices as other object. it conforms the object to the same index on all axes.
  - `other`: Object of the same data type. Its row and column indices are used to define the new indices of this object.
  - `method`: {None, 'backfill'/'bfill', 'pad'/'ffill', 'nearest'}. Method to use for filling holes in reindexed DataFrame.
    * `None` (default): don't fill gaps
    * `pad / ffill`: Propagate last valid observation forward to next valid.
    * `backfill / bfill`: Use next valid observation to fill gap.
    * `nearest`: Use nearest valid observations to fill gap.
  - `copy`: bool. it returns a new object, even if the passed indexes are the same.
  - `level`: int or name. it broadcasts across a level, matching Index values on the passed MultiIndex level.


- `df.rename(mapper=None, index=None, columns=None, axis=None, copy=True, inplace=False, level=None, errors='ignore')`: alters axes labels.
  - `mapper`: dict-like or function. Dict-like or function transformations to apply to
  that axis' values.
  - `index`: dict-like or function. Alternative to specifying axis (`mapper, axis=0` is equivalent to `index=mapper`).
  - `columns`: dict-like or function. Alternative to specifying axis (`mapper, axis=1` is equivalent to `index=mapper`).
  - `axis`: {0 or 'index', 1 or 'columns'}.
  - `copy`: bool. Also copy underlying data.
  - `inplace`: bool. Whether to return a new DataFrame. If True then value of copy is
  ignored.
  - `level`: int or level name. In case of a MultiIndex, only rename labels in the specified level.
  - `errors`: {'ignore', 'raise'}. If `raise`, raise a `KeyError` when a dict-like `mapper`, `index`, or `columns` contains labels that are not present in the Index being transformed. If `ignore`, existing keys will be renamed and extra keys will be ignored.


#### 1. Reindexing the Rows and Columns
```
import pandas as pd
import numpy as np

index = ['A', 'B', 'C', 'D']
columns = ['w', 'x', 'y', 'z']
df = pd.DataFrame(np.random.randn(4,4),index=index, columns=columns)
print("DataFrame:\n", df)


print("\nDataFrame after reindexing its rows:\n",df.reindex(['B', 'D', 'A', 'D']))

print("\nDataFrame after reindexing its columns:\n",df.reindex(['z', 'y', 'x', 'w'],axis=1))

print("\nDataFrame after reindexing its columns:\n",df.reindex(columns= ['z', 'y', 'x', 't']))



(output):
DataFrame:
           w         x         y         z
A -0.586927  0.429363  0.100944  0.897108
B -0.680413  0.934947  1.448152 -0.927108
C  0.546334 -1.270565  0.730399 -0.111934
D -0.159365 -0.251216  0.717659 -0.887854

DataFrame after reindexing its rows:
           w         x         y         z
B -0.680413  0.934947  1.448152 -0.927108
D -0.159365 -0.251216  0.717659 -0.887854
A -0.586927  0.429363  0.100944  0.897108
D -0.159365 -0.251216  0.717659 -0.887854

DataFrame after reindexing its columns:
           z         y         x         w
A  0.897108  0.100944  0.429363 -0.586927
B -0.927108  1.448152  0.934947 -0.680413
C -0.111934  0.730399 -1.270565  0.546334
D -0.887854  0.717659 -0.251216 -0.159365

DataFrame after reindexing its columns:
           z         y         x   t
A  0.897108  0.100944  0.429363 NaN
B -0.927108  1.448152  0.934947 NaN
C -0.111934  0.730399 -1.270565 NaN
D -0.887854  0.717659 -0.251216 NaN
```


#### 2. Replacing the Missing Values
```
import pandas as pd
import numpy as np

index = ['A', 'B', 'C', 'D']
columns = ['w', 'x', 'y', 'z']
df = pd.DataFrame(np.random.randn(4,4),index=index, columns=columns)
print("DataFrame:\n", df)


print("\nDataFrame after reindexing its columns:\n",df.reindex(columns= ['z', 'y', 'x', 't'], fill_value=np.random.rand()))



(output):
DataFrame:
           w         x         y         z
A -0.492146  1.349420 -0.440582 -0.748597
B -0.120275  0.309600 -0.502779 -1.665235
C  0.279676  1.403310  0.259808  1.800163
D  1.226154  1.330155  0.013400 -0.269252

DataFrame after reindexing its columns:
           z         y         x         t
A -0.748597 -0.440582  1.349420  0.784029
B -1.665235 -0.502779  0.309600  0.784029
C  1.800163  0.259808  1.403310  0.784029
D -0.269252  0.013400  1.330155  0.784029
```


#### 3. Reindexing to Align with other DF
```
import pandas as pd
import numpy as np

index = ['A', 'B', 'C', 'D']
columns = ['w', 'x', 'y', 'z']
df = pd.DataFrame(np.random.randn(4,4),index=index, columns=columns)
df1 = pd.DataFrame(np.random.rand(3,3), index=['C','D','E'], columns=['x','y','z'])
print("DataFrame:\n", df)
print("\nSecond DataFrame:\n", df1)


print("\nDataFrame after aligning with the second DF:\n",df.reindex_like(df1))
print("\nDataFrame after aligning with the second DF and filling the missing values:\n",df.reindex_like(df1,method='ffill'))



(output):
DataFrame:
           w         x         y         z
A -0.498052  0.019227  1.685025 -0.574614
B -2.500187  1.038742 -0.262461 -2.233247
C -0.999338  0.695937 -0.387189  0.249610
D  0.774896 -0.853807 -0.152949  1.361564

Second DataFrame:
           x         y         z
C  0.232178  0.749794  0.333435
D  0.308821  0.888049  0.053381
E  0.311926  0.588947  0.477604

DataFrame after aligning with the second DF:
           x         y         z
C  0.695937 -0.387189  0.249610
D -0.853807 -0.152949  1.361564
E       NaN       NaN       NaN

DataFrame after aligning with the second DF and filling the missing values:
           x         y         z
C  0.695937 -0.387189  0.249610
D -0.853807 -0.152949  1.361564
E -0.853807 -0.152949  1.361564
```

#### 4. Renaming the Rows or Columns
```
import pandas as pd
import numpy as np

index = ['A', 'B', 'C', 'D']
columns = ['w', 'x', 'y', 'z']
df = pd.DataFrame(np.random.randn(4,4),index=index, columns=columns)
print("DataFrame:\n", df)

print('\nDataFrame after renaming its index and columns:\n', df.rename(index={'A':'AAA', 'C': 'CCC'}, columns={'w':'xyz'}))



(output):
DataFrame:
           w         x         y         z
A  2.237535  4.836081 -2.122544  0.708416
B -2.110257 -1.617059  0.691209  1.388126
C -0.901843 -0.757745 -1.159576  0.868868
D  1.023723  1.419014 -1.717514 -0.314740

DataFrame after renaming its index:
           xyz         x         y         z
AAA  2.237535  4.836081 -2.122544  0.708416
B   -2.110257 -1.617059  0.691209  1.388126
CCC -0.901843 -0.757745 -1.159576  0.868868
D    1.023723  1.419014 -1.717514 -0.314740
```


### Iteration

Based on what the Pandas Object type is, the behavior of iteration changes. For example, if we are working with Series, the returned result will be a value. For DataFrame, the final output will be column labels.

- `df.iteritems()`: iterates over the DataFrame columns, returning a tuple with the column name and the content as a Series.

- `df.iterrows()`: iterates over DataFrame rows as (index, Series) pairs.

- `df.itertuples(index=True, name='Pandas')`: iterates over DataFrame rows as namedtuples.
  - `index`: bool. If True, return the index as the first element of the tuple.
  - `name`: str or None. The name of the returned namedtuples or None to return regular tuples.


```
import pandas as pd
import numpy as np

index = ['A', 'B', 'C', 'D']
df = pd.DataFrame(np.random.randn(4,4),index=index)
print("DataFrame:\n", df)

print('_'*40)
print("\nIterate over the DataFrame Columns:\n")
for key, value in df.iteritems():
    print(f'{key}\n{value}\n')

print('_'*40)    
print("\nIterate over the DataFrame rows:\n")
for r_idx, row in df.iterrows():
    print(f'{r_idx}\n{row}\n')


print('_'*40)    
print("\nIterate over DataFrame rows as namedtuples:\n")
for row in df.itertuples():
    print(row)



(output):
DataFrame:
           0         1         2         3
A  0.942512 -2.298977  0.843561  0.873152
B -4.182539  2.544485  0.625164 -0.623750
C  0.100735 -0.686678  0.404784  0.732146
D  1.740246  0.472439  0.646567  0.807058
________________________________________

Iterate over the DataFrame Columns:

0
A    0.942512
B   -4.182539
C    0.100735
D    1.740246
Name: 0, dtype: float64

1
A   -2.298977
B    2.544485
C   -0.686678
D    0.472439
Name: 1, dtype: float64

2
A    0.843561
B    0.625164
C    0.404784
D    0.646567
Name: 2, dtype: float64

3
A    0.873152
B   -0.623750
C    0.732146
D    0.807058
Name: 3, dtype: float64

________________________________________

Iterate over the DataFrame rows:

A
0    0.942512
1   -2.298977
2    0.843561
3    0.873152
Name: A, dtype: float64

B
0   -4.182539
1    2.544485
2    0.625164
3   -0.623750
Name: B, dtype: float64

C
0    0.100735
1   -0.686678
2    0.404784
3    0.732146
Name: C, dtype: float64

D
0    1.740246
1    0.472439
2    0.646567
3    0.807058
Name: D, dtype: float64

________________________________________

Iterate over DataFrame rows as namedtuples:

Pandas(Index='A', _1=0.9425119011363567, _2=-2.298977232697303, _3=0.8435608126427299, _4=0.8731519028236635)
Pandas(Index='B', _1=-4.182539283420651, _2=2.54448453173199, _3=0.6251638765930526, _4=-0.6237500441231231)
Pandas(Index='C', _1=0.1007353565149741, _2=-0.6866776717944301, _3=0.4047841722920351, _4=0.7321457195844745)
Pandas(Index='D', _1=1.740245853491503, _2=0.47243895173258155, _3=0.6465667562234418, _4=0.8070581090645265)
```


### Sorting

In order to sort the data in Pandas, There are two kinds:
  - Sort by label
  - Sort by Value


- `df.sort_index(axis=0, level=None, ascending=True, inplace=False, kind='quicksort', na_position='last', sort_remaining=True, ignore_index=False)`: sorts object by labels (along an axis).
  - `axis`: {0 or 'index', 1 or 'columns'}. The axis along which to sort.  
  - `level`: int or level name or list of ints or list of level names. If not None, sort on values in specified index level(s).
  - `axis`: {0 or 'index', 1 or 'columns'}. The axis along which to sort.
  - `ascending`: bool or list-like of bools. Sort ascending vs. descending. When the index is a MultiIndex the sort direction can be controlled for each level individually.
  - `inplace`: bool. If True, perform operation in-place.
  - `kind`: {'quicksort', 'mergesort', 'heapsort'}. Choice of sorting algorithm.
  - `na_position`: {'first', 'last'}. it puts NaNs at the beginning if `first`; `last` puts NaNs at the end.
  - `sort_remaining`: bool. If True and sorting by level and index is multilevel, sort by other levels too (in order) after sorting by specified level.
  - `ignore_index`: bool. If True, the resulting axis will be labeled 0, 1, …, n - 1.

- `df.sort_values(by, axis=0, ascending=True, inplace=False, kind='quicksort', na_position='last', ignore_index=False)`: sorts by the values along either axis.
  - `by`: str or list of str. Name or list of names to sort by.
  - `ascending`: bool or list-like of bools. Sort ascending vs. descending. When the index is a MultiIndex the sort direction can be controlled for each level individually.
  - `inplace`: bool. If True, perform operation in-place.
  - `kind`: {'quicksort', 'mergesort', 'heapsort'}. Choice of sorting algorithm.
  - `na_position`: {'first', 'last'}. it puts NaNs at the beginning if `first`; `last` puts NaNs at the end.
  - `ignore_index`: bool. If True, the resulting axis will be labeled 0, 1, …, n - 1.


```
import pandas as pd
import numpy as np


df = pd.DataFrame(np.random.randn(10,4), index=[1,2,3,4,5,6,7,8,9,10],columns=['a','b','c','d'])
print("DataFrame:\n", df)

df1 = df.sort_index(ascending=False)
print("\nSort By Labels (rows):\n", df1)

df2 = df.sort_index(ascending=False, axis=1)
print("\nSort By Labels (columns):\n", df2)

df3 = df.sort_values(by=['a','b','c','d'],ascending=True)
print("\nSort By Values:\n", df3)



(output):
DataFrame:
            a         b         c         d
1  -2.560428 -0.682470  0.263519 -1.611353
2   0.571391  0.229277 -0.845570 -0.659568
3   0.120580 -1.087334 -0.609759  0.779149
4  -1.841184 -0.778723  1.425955  0.838267
5  -0.111947  1.021800  0.282545  0.407721
6  -0.585476  0.044984 -0.284971  1.438245
7   0.686786 -0.688238 -1.768186 -0.266546
8   0.965797  1.706951 -0.762466 -0.841219
9   0.134450  2.128831  0.206357  0.722662
10 -0.225583 -1.138097 -0.915440 -1.017996

Sort By Labels (rows):
            a         b         c         d
10 -0.225583 -1.138097 -0.915440 -1.017996
9   0.134450  2.128831  0.206357  0.722662
8   0.965797  1.706951 -0.762466 -0.841219
7   0.686786 -0.688238 -1.768186 -0.266546
6  -0.585476  0.044984 -0.284971  1.438245
5  -0.111947  1.021800  0.282545  0.407721
4  -1.841184 -0.778723  1.425955  0.838267
3   0.120580 -1.087334 -0.609759  0.779149
2   0.571391  0.229277 -0.845570 -0.659568
1  -2.560428 -0.682470  0.263519 -1.611353

Sort By Labels (columns):
            d         c         b         a
1  -1.611353  0.263519 -0.682470 -2.560428
2  -0.659568 -0.845570  0.229277  0.571391
3   0.779149 -0.609759 -1.087334  0.120580
4   0.838267  1.425955 -0.778723 -1.841184
5   0.407721  0.282545  1.021800 -0.111947
6   1.438245 -0.284971  0.044984 -0.585476
7  -0.266546 -1.768186 -0.688238  0.686786
8  -0.841219 -0.762466  1.706951  0.965797
9   0.722662  0.206357  2.128831  0.134450
10 -1.017996 -0.915440 -1.138097 -0.225583

Sort By Values:
            a         b         c         d
1  -2.560428 -0.682470  0.263519 -1.611353
4  -1.841184 -0.778723  1.425955  0.838267
6  -0.585476  0.044984 -0.284971  1.438245
10 -0.225583 -1.138097 -0.915440 -1.017996
5  -0.111947  1.021800  0.282545  0.407721
3   0.120580 -1.087334 -0.609759  0.779149
9   0.134450  2.128831  0.206357  0.722662
2   0.571391  0.229277 -0.845570 -0.659568
7   0.686786 -0.688238 -1.768186 -0.266546
8   0.965797  1.706951 -0.762466 -0.841219
```
