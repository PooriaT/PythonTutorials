---
id: 09_function_definition
title: Function Definition
sidebar_label: Function Definition
slug: /09_function_definition
---

---

In Pandas, there is a possibility to apply our function. To do so, we can use three different methods, which depends on how we would like to operate on the data (on the whole DataFrame, row or column, an element only)

1. Table wise Function Application:
  - `df.pipe(func, *args, **kwargs)` applies `func(self, *args, **kwargs)`.
    - `func`: function. Function to apply to the Series/DataFrame. `args` and `kwargs` are passed into `func`.
    - `args`: iterable (optional).
    - `kwargs`: mapping (optional).

Use `.pipe` when chaining together functions that expect Series, DataFrames or GroupBy objects. Instead of writing `func(g(h(df), arg1=a), arg2=b, arg3=c)`, you can write `df.pipe(h).pipe(g, arg1=a).pipe(func, arg2=b, arg3=c)`.



2. Row or Column Wise Function Application:
  - `df.apply(func, axis=0, raw=False, result_type=None, args=(), **kwds)` applies a function along an axis of the DataFrame.
    - `func`: function. Function to apply to each column or row.
    - `axis`: {0 or 'index', 1 or 'columns'}.
    - `raw`: bool. it will be determined if row or column is passed as a Series or ndarray object:
      * ``False``: passes each row or column as a Series to the function.
      * ``True``: the passed function will receive ndarray objects instead.
    - `result_type`: {'expand', 'reduce', 'broadcast', None}. These only act when `axis=1` (columns):
      * `expand`: list-like results will be turned into columns.
      * `reduce`: returns a Series if possible rather than expanding list-like results.
      * `broadcast`: results will be broadcast to the original shape of the DataFrame, the original index and columns will be
      retained.
    - `args`: tuple. Positional arguments to pass to `func` in addition to the array/series.
    - `**kwds`: Additional keyword arguments to pass as keywords arguments to `func`.



3. Element wise Function Application:
  - `df.applymap(func, na_action=None)` applies a function to a Dataframe elementwise.
  - `func`: function, returns a single value from a single value.
  - `na_action`: {None, 'ignore'}. If `ignore`, propagate NaN values, without passing them to func.


```
import pandas as pd
import numpy as np

#Creating DataFrame with Random values
df = pd.DataFrame(np.random.randn(3,4))
print("DataFrame:\n", df)

print("\nTable wise Function Application:\n", df.pipe(np.mean))

print("\nRow Wise Function Application:\n", df.apply(np.mean))
print("\nColumn Wise Function Application:\n", df.apply(np.mean, axis=1))

print("\nElement wise Function Application:\n", df.applymap(lambda x: x**2))



(output):
DataFrame:
           0         1         2         3
0  1.499589 -1.627439 -0.200967 -0.525438
1  0.471910  0.728061 -1.826043 -0.093602
2 -2.136906  1.156234  1.148803 -1.615314

Table wise Function Application:
 0   -0.055136
1    0.085619
2   -0.292736
3   -0.744785
dtype: float64

Row Wise Function Application:
 0   -0.055136
1    0.085619
2   -0.292736
3   -0.744785
dtype: float64

Column Wise Function Application:
 0   -0.213564
1   -0.179919
2   -0.361796
dtype: float64

Element wise Function Application:
           0         1         2         3
0  2.248767  2.648559  0.040388  0.276085
1  0.222699  0.530072  3.334432  0.008761
2  4.566365  1.336878  1.319749  2.609240
```
