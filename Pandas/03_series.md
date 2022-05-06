---
id: 03_series
title: Pandas Series
sidebar_label: Pandas Series
slug: /03_series
---

---

A *Pandas Series* is an one-dimensional array which is like a column in a table. Note that its size is immutable. The labels are called index.

- `pandas.Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)`: One-dimensional `ndarray` with axis labels (including time series).
  - `data`: array-like, Iterable, dict, or scalar value. it contains data stored in Series. If data is a dict, argument order is maintained.
  - `index`: array-like or Index (1d). Values must be hashable and have the same length as `data`. Non-unique index values are allowed. If it is not provide, the default will be (0, 1, 2, ..., n) range.
  - `dtype`: str, numpy.dtype, or ExtensionDtype (optional). Data type for the output Series.
  - `name`: str (optional). The name to give to the Series.
  - `copy`: bool, default False. Copy input data.

```
import pandas as pd

age = [24, 36, 29, 37]

age_series = pd.Series(age, index = ['John', 'Sarah', 'Sarah', 'Joe'])
print("Pandas Series with defined Index: \n", age_series)
print("\nAn specific index: \n", age_series['Sarah'])
print("\nAn specific indices: \n", age_series[['John', 'Joe']])

print("\nPandas Series with default Index: \n", pd.Series(age))
print("\nAn specific index: \n", age_series['Sarah'])



(output):
Pandas Series with defined Index:
 John     24
Sarah    36
Sarah    29
Joe      37
dtype: int64

An specific index:
 Sarah    36
Sarah    29
dtype: int64

An specific indices:
 John    24
Joe     37
dtype: int64

Pandas Series with default Index:
 0    24
1    36
2    29
3    37
dtype: int64

An specific index:
 Sarah    36
Sarah    29
dtype: int64
```
