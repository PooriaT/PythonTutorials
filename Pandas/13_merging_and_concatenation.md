---
id: 13_merging_and_concatenation
title: Merging and Concatenation
sidebar_label: Merging and Concatenation
slug: /13_merging_and_concatenation
---

---

Pandas provides various functions for efficiently combining Series or DataFrame with different set logic for the indexes.

- `pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None, left_index=False, right_index=False, sort=False, suffixes=('_x', '_y'), copy=True, indicator=False, validate=None)`: merges DataFrame or named Series objects with a database-style join. The join is done on columns or indexes. If joining columns on columns, the DataFrame indexes *will be ignored*. Otherwise if joining indexes on indexes or indexes on a column or columns, the index will be passed on.
  - `left`: DataFrame.
  - `right`: DataFrame or named Series Object to merge with.
  - `how`: {'left', 'right', 'outer', 'inner', 'cross'}. Type of merge to be performed.
    * `left`: use only keys from left frame, similar to a SQL left outer join; preserve key order.
    * `right`: use only keys from right frame, similar to a SQL right outer join; preserve key order.
    * `outer`: use union of keys from both frames, similar to a SQL full outer join; sort keys lexicographically.
    * `inner`: use intersection of keys from both frames, similar to a SQL inner join; preserve the order of the left keys.
    * `cross`: creates the cartesian product from both frames, preserves the order of the left keys.
  - `on`: label or list. Column or index level names to join on. These must be found in both DataFrames.
  - `left_on`: label or list, or array-like. Column or index level names to join on in the left DataFrame.
  - `right_on`: label or list, or array-like. Column or index level names to join on in the right DataFrame.
  - `left_index`: bool. Use the index from the left DataFrame as the join key(s). If it is a MultiIndex, the number of keys in the other DataFrame must match the number of levels.
  - `right_index`: bool. Use the index from the right DataFrame as the join key.
  - `sort`: bool. it sorts the join keys lexicographically in the result DataFrame. If False, the order of the join keys depends on the join type (how keyword).
  - `suffixes`: list-like. A length-2 sequence where each element is optionally a string indicating the suffix to add to overlapping column names in `left` and `right` respectively.
  - `copy`: bool.
  - `indicator`: bool or str. If True, adds a column to the output DataFrame called "_merge" with information on the source of each row. The column can be given a different name by providing a string argument. The column will have a Categorical type with the value of "left_only" for observations whose merge key only appears in the left DataFrame, "right_only" for observations whose merge key only appears in the right DataFrame, and "both" if the observation's merge key is found in both DataFrames.
  - `validate`: str (optional). If specified, checks if merge is of specified type.
    * `"one_to_one"` or `"1:1"`: check if merge keys are unique in both left and right datasets.
    * `"one_to_many"` or `"1:m"`: check if merge keys are unique in left dataset.
    * `"many_to_one" o`r `"m:1"`: check if merge keys are unique in right dataset.
    * `"many_to_many"` or `"m:m"`: allowed, but does not result in checks.



```
import pandas as pd
import numpy as np

df1 = pd.DataFrame({'id1': [1, 1, 2, 3, 4],
                    'id2': [1, 2, 1, 2, 1],
                    'A': np.random.randn(5),
                    'B': np.random.randn(5)})
df2 = pd.DataFrame({'id1': [1, 2, 3, 4, 5],
                    'id2': [1, 2, 1, 6, 7],
                    'C': np.random.randn(5),
                    'D': np.random.randn(5)})

print('Two DataFrames individually:')
print('\nDataFrame1:\n',df1)
print('\nDataFrame2:\n',df2)



#Simple Merging
print('\nMerged DataFrame over id1:\n')
print(pd.merge(df1,df2, on='id1'))

print('\nMerged DataFrame over id1 and id2:\n')
print(pd.merge(df1,df2, on=['id1', 'id2']))

# Meging by considering how flag
print('\nMerged DataFrame over id1 and id2 with how=\'outer\':\n')
print(pd.merge(df1,df2, how='outer', on=['id1','id2']))



(output):
Two DataFrames individually:

DataFrame1:
    id1  id2         A         B
0    1    1  0.318611 -2.231987
1    1    2  0.303985 -0.037025
2    2    1  1.354474 -0.933455
3    3    2  0.069780 -0.506898
4    4    1 -1.004554  1.607020

DataFrame2:
    id1  id2         C         D
0    1    1 -0.443650  1.185767
1    2    2 -0.028692  0.013745
2    3    1  0.722863 -1.076306
3    4    6  1.749710  1.368985
4    5    7 -0.544999 -0.525113

Merged DataFrame over id1:

   id1  id2_x         A         B  id2_y         C         D
0    1      1  0.318611 -2.231987      1 -0.443650  1.185767
1    1      2  0.303985 -0.037025      1 -0.443650  1.185767
2    2      1  1.354474 -0.933455      2 -0.028692  0.013745
3    3      2  0.069780 -0.506898      1  0.722863 -1.076306
4    4      1 -1.004554  1.607020      6  1.749710  1.368985

Merged DataFrame over id1 and id2:

   id1  id2         A         B        C         D
0    1    1  0.318611 -2.231987 -0.44365  1.185767

Merged DataFrame over id1 and id2 and how='left':

   id1  id2         A         B         C         D
0    1    1  0.318611 -2.231987 -0.443650  1.185767
1    1    2  0.303985 -0.037025       NaN       NaN
2    2    1  1.354474 -0.933455       NaN       NaN
3    3    2  0.069780 -0.506898       NaN       NaN
4    4    1 -1.004554  1.607020       NaN       NaN
5    2    2       NaN       NaN -0.028692  0.013745
6    3    1       NaN       NaN  0.722863 -1.076306
7    4    6       NaN       NaN  1.749710  1.368985
8    5    7       NaN       NaN -0.544999 -0.525113
```



- `df.join(other, on=None, how='left', lsuffix='', rsuffix='', sort=False)`: joins columns with `other` DataFrame either on index or on a key column. Efficiently join multiple DataFrame objects by index at once by
passing a list.
  - `other`: DataFrame, Series, or list of DataFrame. Index should be similar to one of the columns in this one. If a Series is passed, its name attribute must be set, and that will be used as the column name in the resulting joined DataFrame.
  - `on`: str, list of str, or array-like  (optional). Column or index level name(s) in the caller to join on the index in `other`, otherwise joins index-on-index. If multiple values given, the `other` DataFrame must have a MultiIndex.
  - `how`: {'left', 'right', 'outer', 'inner'}. How to handle the operation of the two objects.
    * `left`: use calling frame's index (or column if on is specified)
    * `right`: use `other`'s index.
    * `outer`: form union of calling frame's index (or column if on is specified) with `other`'s index, and sort it. lexicographically.
    * `inner`: form intersection of calling frame's index (or column if on is specified) with `other`'s index, preserving the order of the calling's one.
  - `lsuffix`: str. Suffix to use from left frame's overlapping columns.
  - `rsuffix`: str. Suffix to use from right frame's overlapping columns.
  - sort : bool. Order result DataFrame lexicographically by the join key. If False, the order of the join key depends on the join type (how keyword).


```
import pandas as pd
import numpy as np


df1 = pd.DataFrame({'A': np.random.randn(5),
                    'B': np.random.randn(5)},
                  index = ['a', 'b', 'c', 'd', 'e'])
df2 = pd.DataFrame({'C': np.random.randn(5),
                    'D': np.random.randn(5)},
                  index = ['a', 'b', 'd', 'e', 'f'])

print('Two DataFrames individually:')
print('\nDataFrame1:\n',df1)
print('\nDataFrame2:\n',df2)



#Simple joining
print('\nJoined DataFrame:\n')
print(df1.join(df2))

# Joining by considering how flag
print('\nJoined DataFrame with how=\'outer\':\n')
print(df1.join(df2, how='outer'))



(output):
Two DataFrames individually:

DataFrame1:
           A         B
a -1.201688  0.645396
b -2.592874  0.443148
c  1.424857 -0.637192
d  0.598013  0.951034
e -1.136922  0.109475

DataFrame2:
           C         D
a -0.421880  0.237549
b -0.527864 -1.239245
d  0.266170 -1.599512
e  0.478595  1.736199
f  0.021794 -1.204098

Joined DataFrame:

          A         B         C         D
a -1.201688  0.645396 -0.421880  0.237549
b -2.592874  0.443148 -0.527864 -1.239245
c  1.424857 -0.637192       NaN       NaN
d  0.598013  0.951034  0.266170 -1.599512
e -1.136922  0.109475  0.478595  1.736199

Joined DataFrame with how='outer':

          A         B         C         D
a -1.201688  0.645396 -0.421880  0.237549
b -2.592874  0.443148 -0.527864 -1.239245
c  1.424857 -0.637192       NaN       NaN
d  0.598013  0.951034  0.266170 -1.599512
e -1.136922  0.109475  0.478595  1.736199
f       NaN       NaN  0.021794 -1.204098
```



- `pd.concat(objs, axis=0, join='outer', ignore_index=False, keys=None, levels=None, names=None, verify_integrity=False, sort=False, copy=True)`: concatenates pandas objects along a particular axis with optional set logic
along the other axes.
  - `objs`: a sequence or mapping of Series or DataFrame objects. If a mapping is passed, the sorted keys will be used as the `keys` argument, unless it is passed, in which case the values will be selected . Any None objects will be dropped silently unless they are all None in which case a ValueError will be raised.
  - `axis`: {0/'index', 1/'columns'}.The axis to concatenate along.
  - `join`: {'inner', 'outer'}. How to handle indexes on other axis (or axes).
  - `ignore_index`: bool. If True, do not use the index values along the concatenation axis. The resulting axis will be labeled 0, ..., n - 1.
  - `keys`: sequence. If multiple levels passed, should contain tuples. Construct hierarchical index using the passed keys as the outermost level.
  - `levels`: list of sequences. Specific levels (unique values) to use for constructing a MultiIndex. Otherwise they will be inferred from the keys.
  - `names`: list. Names for the levels in the resulting hierarchical index.
  - `verify_integrity`: bool. Check whether the new concatenated axis contains duplicates.
  - `sort`: bool. Sort non-concatenation axis if it is not already aligned when `join` is 'outer'. This has no effect when `join='inner'`, which already preserves the order of the non-concatenation axis.
  - `copy`: bool. If False, do not copy data unnecessarily.


```
import pandas as pd
import numpy as np


df1 = pd.DataFrame({'A': np.random.randn(5),
                    'B': np.random.randn(5),
                    'C': np.random.randn(5),
                    'D': np.random.randn(5)},
                  index = [1,2,3,4,5])
df2 = pd.DataFrame({'A': np.random.randn(5),
                    'B': np.random.randn(5),
                    'C': np.random.randn(5),
                    'D': np.random.randn(5)},
                  index = [6,7,8,9,10])
df3 = pd.DataFrame({'A': np.random.randn(5),
                    'B': np.random.randn(5),
                    'C': np.random.randn(5),
                    'D': np.random.randn(5)},
                  index = [11,12,13,14,15])

print('Each DataFrame individually:')
print('\nDataFrame1:\n',df1)
print('\nDataFrame2:\n',df2)
print('\nDataFrame2:\n',df3)


#concatenation
print('\nDataFrame concatenation:\n')
print(pd.concat([df1,df2,df3]))



(output):
Each DataFrame individually:

DataFrame1:
           A         B         C         D
1  0.876375  2.451137  0.677698 -0.061996
2  0.715572  1.671524 -0.014557 -0.989180
3 -1.774234 -0.590458 -0.770941 -0.610158
4 -0.299138  0.468284 -1.230156  0.571815
5 -0.085700  1.378504 -1.470673  0.080047

DataFrame2:
            A         B         C         D
6   0.053057 -1.493216 -1.643894 -0.079007
7  -0.405236 -1.345398 -0.118329 -0.304679
8   0.180470 -0.425508  1.438093  0.401781
9  -0.194235 -1.510673 -0.883018  2.012421
10  0.135232 -0.057220  0.237434 -0.052680

DataFrame2:
            A         B         C         D
11  1.596261 -0.605609 -0.883355 -1.347834
12 -0.276376  0.148217  0.513311 -1.273163
13 -2.276969 -0.400153  0.245633  0.811338
14 -0.867234  0.249021  0.183991  1.684204
15  0.035757  1.607882 -0.544709  2.030307

DataFrame concatenation:

           A         B         C         D
1   0.876375  2.451137  0.677698 -0.061996
2   0.715572  1.671524 -0.014557 -0.989180
3  -1.774234 -0.590458 -0.770941 -0.610158
4  -0.299138  0.468284 -1.230156  0.571815
5  -0.085700  1.378504 -1.470673  0.080047
6   0.053057 -1.493216 -1.643894 -0.079007
7  -0.405236 -1.345398 -0.118329 -0.304679
8   0.180470 -0.425508  1.438093  0.401781
9  -0.194235 -1.510673 -0.883018  2.012421
10  0.135232 -0.057220  0.237434 -0.052680
11  1.596261 -0.605609 -0.883355 -1.347834
12 -0.276376  0.148217  0.513311 -1.273163
13 -2.276969 -0.400153  0.245633  0.811338
14 -0.867234  0.249021  0.183991  1.684204
15  0.035757  1.607882 -0.544709  2.030307
```
