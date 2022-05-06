---
id: 11_windowing_operations
title: Windowing Operations
sidebar_label: Windowing Operations
slug: /11_windowing_operations
---

---

### Window Functions

Window functions can support computations on the given row's data and return a value that original query. They are mainly applied in finding trends in the data.

- `df.rolling(window, min_periods=None, center=False, win_type=None, on=None, axis=0, closed=None)`: provide rolling window calculations.
  - `window`: int, offset, or BaseIndexer subclass. Size of the moving window. This is the number of observations used for calculating the statistic. Each window will be a fixed size. If its an offset then this will be the time period of each window. If a BaseIndexer subclass is passed, calculates the window boundaries based on the defined `get_window_bounds` method.
  - `min_periods`: int. Minimum number of observations in window required to have a value (otherwise result is NA).
  - `center`: bool. it sets the labels at the center of the window.
  - `win_type`: str. Provide a window type. If `None`, all points are evenly weighted.
  - `on`: str (optional). For a DataFrame, a datetime-like column or MultiIndex level on which to calculate the rolling window, rather than the DataFrame's index. Provided integer column is ignored and excluded from result since an integer index is not used to calculate the rolling window.
  - `axis`: int or str.
  - `closed`: str. it makes the interval closed on the 'right', 'left', 'both' or 'neither' endpoints.


- `df.expanding(min_periods=1, center=None, axis=0)`: provides expanding transformations.
  - `min_periods`: int. Minimum number of observations in window required to have a value (otherwise result is NA).
  - `center`: bool. it sets the labels at the center of the window.
  - `axis`: int or str.


- `df.ewm(com=None, span=None, halflife=None, alpha=None, min_periods=0, adjust=True, ignore_na=False, axis=0, times=None)`: provide exponential weighted (EW) functions.
  - `com`: float (optional). it specifies decay in terms of center of mass.
  - `span`: float (optional). it specifies decay in terms of span.
  - `halflife`: float, str, timedelta (optional). it specifies decay in terms of half-life.
  - `alpha`: float (optional). it specifies smoothing factor.
  - `min_periods`: int. Minimum number of observations in window required to have a value (otherwise result is NA).
  - `adjust`: bool. it divides by decaying adjustment factor in beginning periods to account for imbalance in relative weightings.
  - `ignore_na`: bool. Ignore missing values when calculating weights.
  - `axis`: {0, 1}. The axis to use.
  - `times`: str, np.ndarray, Series. Times corresponding to the observations.


```
import pandas as pd
import numpy as np

index = pd.date_range('6/1/2021', periods=10)
columns = ['A','B','C']
df = pd.DataFrame(np.random.randn(10,3), index=index, columns=columns)

print('Original DataFrame:\n',df)

print('\nRolling Window Calculations:\n',df.rolling(window=4).mean())
print('\nExpanding Transformations:\n',df.expanding(min_periods=4).mean())
print('\nExponential Weighted Functions:\n',df.ewm(com=0.5).mean())



(output):
Original DataFrame:
                    A         B         C
2021-06-01  0.815196  1.342416 -1.055178
2021-06-02  0.052216  0.248385  0.356229
2021-06-03  0.920710  0.622922  2.148739
2021-06-04  0.583613  0.114132  0.075902
2021-06-05 -0.267948  0.411267 -0.899480
2021-06-06  1.238612  0.515583  1.884964
2021-06-07  2.662540 -0.015558  0.134951
2021-06-08 -1.255923 -0.175340  0.156625
2021-06-09 -0.485567 -0.164051 -0.146699
2021-06-10 -0.300542  1.263235  0.049133

Rolling Window Calculations:
                    A         B         C
2021-06-01       NaN       NaN       NaN
2021-06-02       NaN       NaN       NaN
2021-06-03       NaN       NaN       NaN
2021-06-04  0.592933  0.581964  0.381423
2021-06-05  0.322147  0.349176  0.420348
2021-06-06  0.618746  0.415976  0.802531
2021-06-07  1.054204  0.256356  0.299084
2021-06-08  0.594320  0.183988  0.319265
2021-06-09  0.539916  0.040158  0.507460
2021-06-10  0.155127  0.227072  0.048503

Expanding Transformations:
                    A         B         C
2021-06-01       NaN       NaN       NaN
2021-06-02       NaN       NaN       NaN
2021-06-03       NaN       NaN       NaN
2021-06-04  0.592933  0.581964  0.381423
2021-06-05  0.420757  0.547824  0.125242
2021-06-06  0.557066  0.542451  0.418529
2021-06-07  0.857848  0.462735  0.378018
2021-06-08  0.593627  0.382976  0.350344
2021-06-09  0.473716  0.322195  0.295117
2021-06-10  0.396291  0.416299  0.270519

Exponential Weighted Functions:
                    A         B         C
2021-06-01  0.815196  1.342416 -1.055178
2021-06-02  0.242961  0.521893  0.003377
2021-06-03  0.712172  0.591836  1.488628
2021-06-04  0.625394  0.269386  0.535038
2021-06-05  0.027372  0.364364 -0.425259
2021-06-06  0.835974  0.465315  1.117005
2021-06-07  2.054242  0.144586  0.462003
2021-06-08 -0.152871 -0.068731  0.258387
2021-06-09 -0.374680 -0.132281 -0.011684
2021-06-10 -0.325254  0.798079  0.028862
```
