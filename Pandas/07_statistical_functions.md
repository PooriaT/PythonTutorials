---
id: 07_statistical_functions
title: Statistical Functions
sidebar_label: Statistical Functions
slug: /07_statistical_functions
---

---


As we are mainly working with *DataFrame* in *pandas*, there are a lot of statistical functions which help you to describe your available data. Here, we are looking at the most common functions:

- `df.describe(percentiles=None, include=None, exclude=None, datetime_is_numeric=False)`: Descriptive statistics include those that summarize the central tendency, dispersion and shape of a dataset’s distribution, excluding `NaN` values.
  - `percentiles`: list-like of numbers (optional). The percentiles to include in the output.
  - `include`: ‘all’, list-like of dtypes or None (optional). A white list of data types to include in the result.
  - `exclude`: list-like of dtypes or None (optional). A black list of data types to omit from the result.
  - `datetime_is_numeric`: bool. Whether to treat datetime dtypes as numeric.


- `df.sum(axis=None, skipna=None, level=None, numeric_only=None, min_count=0)`: returns the sum of the values over the requested axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `numeric_only`: bool. Include only float, int, boolean columns.
  - `min_count`: int. The required number of valid values to perform the operation.


- `df.count(axis=0, level=None, numeric_only=False)`: counts non-NA cells for each column or row.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `numeric_only`: bool. Include only float, int, boolean columns.


- `df.mean(axis=None, skipna=None, level=None, numeric_only=None)`: returns the mean of the values over the requested axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `numeric_only`: bool. Include only float, int, boolean columns.


- `df.median(axis=None, skipna=None, level=None, numeric_only=None)`: returns the median of the values over the request axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `numeric_only`: bool. Include only float, int, boolean columns.


- `df.mode(axis=0, numeric_only=False, dropna=True)`: gets the modes of each element along the selected axis.
  - `axis`: {0 or 'index', 1 or 'columns'}. Axis for the function to be applied on.
  - `numeric_only`: bool. Include only float, int, boolean columns.
  - `dropna`: bool. Don't consider counts of NaN/NaT.


- `df.std(axis=None, skipna=None, level=None, ddof=1, numeric_only=None,)`: returns sample standard deviation over request axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `ddof`: int. Delta degrees of freedom.  The divisor used in calculations is `N - ddof`, where `N` represents the number of elements.
  - `numeric_only`: bool. Include only float, int, boolean columns.


- `df.min(axis=None, skipna=None, level=None, numeric_only=None)`: returns the minimum of the values over the requested axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `numeric_only`: bool. Include only float, int, boolean columns.


- `df.max(axis=None, skipna=None, level=None, numeric_only=None)`: returns the maximum of the values over the requested axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
- `numeric_only`: bool. Include only float, int, boolean columns.


- `df.abs()`: returns a series/DataFrame with absolute numeric value of each element.


- `df.prod(axis=None, skipna=None, level=None, numeric_only=None, min_count=0)`: returns the product of the values over the requested axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.
  - `level`: int or level name. If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a Series.
  - `numeric_only`: bool. Include only float, int, boolean columns.
  - `min_count`: int. The required number of valid values to perform the operation.


- `df.cumsum(axis=None, skipna=True)`: returns cumulative sum over a DataFrame or Series axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.


- `df.cumprod(axis=None, skipna=True)`: returns cumulative product over a DataFrame or Series axis.
  - `axis`: {index (0), columns (1)}. Axis for the function to be applied on.
  - `skipna`: bool. Exclude NA/null values when computing the result.


- `df.pct_change(periods=1, fill_method='pad', limit=None, freq=None,)`: returns percentage change between the current and a prior element.
  - `periods`: int. Periods to shift for forming percent change.
  - `fill_method` : str. How to handle NAs before computing percent changes.
  - `limit`: int. The number of consecutive NAs to fill before stopping.
  - `freq`: DateOffset, timedelta, or str (optional). Increment to use from time series API (e.g. 'M' or BDay()).


- `df.cov(min_periods=None, ddof=1)`: computes pairwise covariance of columns, excluding NA/null values.
  - `min_periods`: int (optional). Minimum number of observations required per pair of columns to have a valid result.
  - `ddof`: int. Delta degrees of freedom.  The divisor used in calculations is `N - ddof`, where `N` represents the number of elements.


- `df.corr(method='pearson', min_periods=1)`: computes pairwise correlation of columns, excluding NA/null values.
  - `method`: {'pearson', 'kendall', 'spearman'} or callable
    Method of correlation:
    - `pearson` : standard correlation coefficient
    - `kendall` : Kendall Tau correlation coefficient
    - `spearman` : Spearman rank correlation
    - callable: callable with input two 1d ndarrays and returning a float.
  - `min_periods`: int (optional). Minimum number of observations required per pair of columns to have a valid result.



```
import pandas as pd

df = pd.read_csv('grades.csv')
print("Whole Data: \n", df.to_string())

print('\nDataFrame Description: \n', df.describe())
print('\nCount: \n', df.count())
print('\nSum: \n', df.sum())
print('\nMean: \n', df.mean())
print('\nMedian: \n', df.median())
print('\nMode: \n', df.mode())
print('\nStandard Deviation: \n', df.std())
print('\nMin: \n', df.min())
print('\nMax: \n', df.max())

print('\n\n')
data = [{'a': 2, 'b': 4}, {'a': 1, 'b': 5, 'c':3}]
df = pd.DataFrame(data, index=['r1', 'r2'])
print("Whole Data: \n", df.to_string())

print('\nProduct: \n', df.prod())
print('\nCumulative sum: \n', df.cumsum())
print('\nCumulative product: \n', df.cumprod())

print('\nPercentage change: \n', df.pct_change())
print('\nCovariance: \n', df.cov())
print('\nCorrelation: \n', df.corr())



(output):
Whole Data:
     Last name      "First name"                  "SSN"          "Test1"   "Test2"   "Test3"   "Test4"   "Final"  "Grade"
0     Alfalfa        "Aloysius"          "123-45-6789"               40        90       100        83        49     "D-"
1      Alfred      "University"          "123-12-1234"               41        97        96        97        48     "D+"
2       Gerty          "Gramma"          "567-89-0123"               41        80        60        40        44      "C"
3     Android        "Electric"          "087-65-4321"               42        23        36        45        47     "B-"
4     Bumpkin            "Fred"          "456-78-9012"               43        78        88        77        45     "A-"
5      Rubble           "Betty"          "234-56-7890"               44        90        80        90        46     "C-"
6      Noshow           "Cecil"          "345-67-8901"               45        11        -1         4        43      "F"
7        Buff             "Bif"          "632-79-9939"               46        20        30        40        50     "B+"
8     Airpump          "Andrew"          "223-45-6789"               49         1        90       100        83      "A"
9      Backus             "Jim"          "143-12-1234"               48         1        97        96        97     "A+"
10  Carnivore             "Art"          "565-89-0123"               44         1        80        60        40     "D+"
11      Dandy             "Jim"          "087-75-4321"               47         1        23        36        45     "C+"
12   Elephant             "Ima"          "456-71-9012"               45         1        78        88        77     "B-"
13   Franklin           "Benny"          "234-56-2890"               50         1        90        80        90     "B-"
14     George             "Boy"          "345-67-3901"               40         1        11        -1         4      "B"
15  Heffalump          "Harvey"          "632-79-9439"               30         1        20        30        40      "C"

DataFrame Description:
                "Test1"    "Test2"     "Test3"     "Test4"    "Final"
count         16.00000  16.000000   16.000000   16.000000  16.000000
mean          43.43750  31.062500   61.125000   60.312500  53.000000
std            4.74649  39.760062   35.137587   33.189795  23.041991
min           30.00000   1.000000   -1.000000   -1.000000   4.000000
25%           41.00000   1.000000   28.250000   39.000000  43.750000
50%           44.00000   6.000000   79.000000   68.500000  46.500000
75%           46.25000  78.500000   90.000000   88.500000  56.750000
max           50.00000  97.000000  100.000000  100.000000  97.000000

Count:
 Last name          16
 "First name"      16
 "SSN"             16
        "Test1"    16
 "Test2"           16
 "Test3"           16
 "Test4"           16
 "Final"           16
 "Grade"           16
dtype: int64

Sum:
 Last name          AlfalfaAlfredGertyAndroidBumpkinRubbleNoshowBu...
 "First name"         "Aloysius"    "University"     "Gramma"   "...
 "SSN"                "123-45-6789" "123-12-1234"     "567-89-012...
        "Test1"                                                  695
 "Test2"                                                         497
 "Test3"                                                         978
 "Test4"                                                         965
 "Final"                                                         848
 "Grade"              "D-"   "D+"   "C"   "B-"   "A-"   "C-"   "F...
dtype: object

Mean:
         "Test1"    43.4375
 "Test2"           31.0625
 "Test3"           61.1250
 "Test4"           60.3125
 "Final"           53.0000
dtype: float64

Median:
         "Test1"    44.0
 "Test2"            6.0
 "Test3"           79.0
 "Test4"           68.5
 "Final"           46.5
dtype: float64

Mode:
     Last name      "First name"                  "SSN"          "Test1"  \
0     Airpump             "Bif"          "087-75-4321"             40.0   
1     Alfalfa          "Gramma"          "143-12-1234"             41.0   
2      Alfred             "Jim"          "345-67-3901"             44.0   
3     Android           "Betty"          "456-71-9012"             45.0   
4      Backus             "Boy"          "565-89-0123"              NaN   
5        Buff           "Cecil"          "632-79-9939"              NaN   
6     Bumpkin             "Jim"          "456-78-9012"              NaN   
7   Carnivore      "University"          "234-56-2890"              NaN   
8       Dandy        "Aloysius"          "234-56-7890"              NaN   
9    Elephant          "Andrew"          "345-67-8901"              NaN   
10   Franklin        "Electric"          "223-45-6789"              NaN   
11     George            "Fred"          "567-89-0123"              NaN   
12      Gerty           "Benny"          "632-79-9439"              NaN   
13  Heffalump             "Ima"          "087-65-4321"              NaN   
14     Noshow             "Art"          "123-45-6789"              NaN   
15     Rubble          "Harvey"          "123-12-1234"              NaN   

     "Test2"   "Test3"   "Test4"   "Final"  "Grade"  
0        1.0      80.0      40.0      40.0     "B-"  
1        NaN      90.0       NaN      45.0      NaN  
2        NaN       NaN       NaN       NaN      NaN  
3        NaN       NaN       NaN       NaN      NaN  
4        NaN       NaN       NaN       NaN      NaN  
5        NaN       NaN       NaN       NaN      NaN  
6        NaN       NaN       NaN       NaN      NaN  
7        NaN       NaN       NaN       NaN      NaN  
8        NaN       NaN       NaN       NaN      NaN  
9        NaN       NaN       NaN       NaN      NaN  
10       NaN       NaN       NaN       NaN      NaN  
11       NaN       NaN       NaN       NaN      NaN  
12       NaN       NaN       NaN       NaN      NaN  
13       NaN       NaN       NaN       NaN      NaN  
14       NaN       NaN       NaN       NaN      NaN  
15       NaN       NaN       NaN       NaN      NaN  

Standard Deviation:
         "Test1"     4.746490
 "Test2"           39.760062
 "Test3"           35.137587
 "Test4"           33.189795
 "Final"           23.041991
dtype: float64

Min:
 Last name                        Airpump
 "First name"                      "Bif"
 "SSN"                     "087-75-4321"
        "Test1"                       30
 "Test2"                               1
 "Test3"                              -1
 "Test4"                              -1
 "Final"                               4
 "Grade"                             "A"
dtype: object

Max:
 Last name                  Rubble
 "First name"            "Harvey"
 "SSN"              "123-12-1234"
        "Test1"                50
 "Test2"                       97
 "Test3"                      100
 "Test4"                      100
 "Final"                       97
 "Grade"                      "F"
dtype: object



Whole Data:
     a  b    c
r1  2  4  NaN
r2  1  5  3.0

Product:
 a     2.0
b    20.0
c     3.0
dtype: float64

Cumulative sum:
     a  b    c
r1  2  4  NaN
r2  3  9  3.0

Cumulative product:
     a   b    c
r1  2   4  NaN
r2  2  20  3.0

Percentage change:
       a     b   c
r1  NaN   NaN NaN
r2 -0.5  0.25 NaN

Covariance:
      a    b   c
a  0.5 -0.5 NaN
b -0.5  0.5 NaN
c  NaN  NaN NaN

Correlation:
      a    b   c
a  1.0 -1.0 NaN
b -1.0  1.0 NaN
c  NaN  NaN NaN
```
