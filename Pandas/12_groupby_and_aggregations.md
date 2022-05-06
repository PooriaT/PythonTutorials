---
id: 12_groupby_and_aggregations
title: GroupBy and Aggregations
sidebar_label: GroupBy and Aggregations
slug: /12_groupby_and_aggregations
---

---

### Aggregations

Aggregation operation is used to reduce the dimension of the returned objects.

- `df.aggregate(func=None, axis=0, *args, **kwargs)`: aggregates using one or more operations over the specified axis.
  - `func`: function, str, list or dict. Function to use for aggregating the data. Accepted combinations are:
    - function
    - string function name
    - list of functions and/or function names, e.g. `[np.sum, 'mean']`
    - dict of axis labels -> functions, function names or list of such.
  - `axis`: {0 or 'index', 1 or 'columns'}.
  - `*args`: Positional arguments to pass to `func`.
  - `**kwargs`: Keyword arguments to pass to `func`.


```
import pandas as pd
import numpy as np

columns = ['A', 'B', 'C', 'D']
df = pd.DataFrame(np.random.randn(10,4), columns=columns)
print("Original DataFrame:\n",df)

print("\nAggregated DataFrame over rows:\n", df.aggregate(['sum', 'mean', 'max', 'min']))
print("\nAggregated DataFrame over columns:\n", df.aggregate(['sum', 'mean', 'max', 'min'],axis=1))



(output):
Original DataFrame:
           A         B         C         D
0  0.181717  1.147194 -0.347283  0.883029
1 -1.674634  1.974283 -0.134052 -0.435811
2 -0.677238  0.732769  1.107806 -1.430106
3 -0.619525 -0.923559  0.846841  1.194759
4  0.751142 -0.058263 -1.096218 -0.824850
5  0.214491  0.089884  0.314555  1.671592
6  0.158078  0.142937  1.206025  0.221779
7  0.565235 -1.870063  0.113365  0.350785
8  0.110632  1.116263 -1.499375  0.625471
9  0.989426 -0.295893 -0.477441  1.263583

Aggregated DataFrame over rows:
              A         B         C         D
sum  -0.000677  2.055552  0.034222  3.520232
mean -0.000068  0.205555  0.003422  0.352023
max   0.989426  1.974283  1.206025  1.671592
min  -1.674634 -1.870063 -1.499375 -1.430106

Aggregated DataFrame over columns:
         sum      mean       max       min
0  1.864656  0.466164  1.147194 -0.347283
1 -0.270213 -0.067553  1.974283 -1.674634
2 -0.266770 -0.066693  1.107806 -1.430106
3  0.498515  0.124629  1.194759 -0.923559
4 -1.228189 -0.307047  0.751142 -1.096218
5  2.290522  0.572630  1.671592  0.089884
6  1.728820  0.432205  1.206025  0.142937
7 -0.840679 -0.210170  0.565235 -1.870063
8  0.352992  0.088248  1.116263 -1.499375
9  1.479675  0.369919  1.263583 -0.477441
```

### Groupby

A groupby function involves some operations on original object as follows:
- Splitting the object into groups based on some criteria
- Applying a function to each group independently
- Combining a result into a data structure

It can be applied to make large amounts of data grouped and computer various operations on them.

- `df.groupby(by=None, axis=0, level=None, as_index=True, sort=True, group_keys=True, squeeze=<object object at 0x00000132C6DD0F40>, observed=False, dropna=True)`: groups DataFrame using a mapper or by a Series of columns.
  - `by`: mapping, function, label, or list of labels. Used to determine the groups for the groupby. If `by` is a function, it's called on each value of the object's index. If a dict or Series is passed, the Series or dict VALUES will be used to determine the groups (the Series' values are first aligned). If an ndarray is passed, the values are used as-is to determine the groups.
  - `axis`: {0 or 'index', 1 or 'columns'}.
  - `level`: int, level name, or sequence of such. If the axis is a MultiIndex (hierarchical), group by a particular level or levels.
  - `as_index`: bool. For aggregated output, return object with group labels as the
  index. Only relevant for DataFrame input.
  - `sort`: bool. Sort group keys. Get better performance by turning this off.
  - `group_keys`: bool. When calling apply, add group keys to index to identify pieces.
  - `squeeze`: bool. it reduces the dimensionality of the return type if possible, otherwise return a consistent type.
  - `observed`: bool. This only applies if any of the groupers are Categoricals. If True, it only shows observed values for categorical groupers.
  - `dropna`: bool. If True, and if group keys contain NA values, NA values together with row/column will be dropped.


```
import pandas as pd
import numpy as np

df = pd.read_csv('grades.csv')
print('The Original DataFrame:\n', df.to_string())

grouped_df_1 = df.groupby('First name')
print("\nGrouped DataFrame by Firstname:\n", grouped_df_1.groups)

grouped_df_2 = df.groupby(['Last name', 'SSN'])
print('\nGrouped DataFrame by Last name and SSN:\n', grouped_df_2.groups)

#Iterating over groups
for name, group in grouped_df_1:
    print(f'{name} ===> \n {group.to_string()}')



(output):
The Original DataFrame:
     Last name      First name                  SSN  Test1  Test2  Test3  Test4  Final  Grade
0     Alfalfa        Aloysius          123-45-6789     40     90    100     83     49     D-
1      Alfred      University          123-12-1234     41     97     96     97     48     D+
2       Gerty          Gramma          567-89-0123     41     80     60     40     44      C
3     Android        Electric          087-65-4321     42     23     36     45     47     B-
4     Bumpkin            Fred          456-78-9012     43     78     88     77     45     A-
5      Rubble           Betty          234-56-7890     44     90     80     90     46     C-
6      Noshow           Cecil          345-67-8901     45     11     -1      4     43      F
7        Buff             Bif          632-79-9939     46     20     30     40     50     B+
8     Airpump          Andrew          223-45-6789     49      1     90    100     83      A
9      Backus             Jim          143-12-1234     48      1     97     96     97     A+
10  Carnivore             Art          565-89-0123     44      1     80     60     40     D+
11      Dandy             Jim          087-75-4321     47      1     23     36     45     C+
12   Elephant             Ima          456-71-9012     45      1     78     88     77     B-
13   Franklin           Benny          234-56-2890     50      1     90     80     90     B-
14     George             Boy          345-67-3901     40      1     11     -1      4      B
15  Heffalump          Harvey          632-79-9439     30      1     20     30     40      C

Grouped DataFrame by Firstname:
 {'      Bif': [7], '     Gramma': [2], '     Jim': [11], '    Betty': [5], '    Boy': [14], '    Cecil': [6], '    Jim': [9], '    University': [1], '   Aloysius': [0], '   Andrew': [8], '   Electric': [3], '   Fred': [4], '  Benny': [13], '  Ima': [12], ' Art': [10], ' Harvey': [15]}

Grouped DataFrame by Last name and SSN:
 {('Airpump', '     223-45-6789'): [8], ('Alfalfa', '   123-45-6789'): [0], ('Alfred', ' 123-12-1234'): [1], ('Android', '   087-65-4321'): [3], ('Backus', '        143-12-1234'): [9], ('Buff', '        632-79-9939'): [7], ('Bumpkin', '       456-78-9012'): [4], ('Carnivore', '        565-89-0123'): [10], ('Dandy', '        087-75-4321'): [11], ('Elephant', '        456-71-9012'): [12], ('Franklin', '      234-56-2890'): [13], ('George', '        345-67-3901'): [14], ('Gerty', '     567-89-0123'): [2], ('Heffalump', '     632-79-9439'): [15], ('Noshow', '      345-67-8901'): [6], ('Rubble', '      234-56-7890'): [5]}
      Bif ===>
   Last name First name                  SSN  Test1  Test2  Test3  Test4  Final  Grade
7      Buff        Bif          632-79-9939     46     20     30     40     50     B+
     Gramma ===>
   Last name   First name               SSN  Test1  Test2  Test3  Test4  Final Grade
2     Gerty       Gramma       567-89-0123     41     80     60     40     44     C
     Jim ===>
    Last name First name                  SSN  Test1  Test2  Test3  Test4  Final  Grade
11     Dandy        Jim          087-75-4321     47      1     23     36     45     C+
    Betty ===>
   Last name First name                SSN  Test1  Test2  Test3  Test4  Final  Grade
5    Rubble      Betty        234-56-7890     44     90     80     90     46     C-
    Boy ===>
    Last name First name                  SSN  Test1  Test2  Test3  Test4  Final Grade
14    George        Boy          345-67-3901     40      1     11     -1      4     B
    Cecil ===>
   Last name First name                SSN  Test1  Test2  Test3  Test4  Final Grade
6    Noshow      Cecil        345-67-8901     45     11     -1      4     43     F
    Jim ===>
   Last name First name                  SSN  Test1  Test2  Test3  Test4  Final  Grade
9    Backus        Jim          143-12-1234     48      1     97     96     97     A+
    University ===>
   Last name      First name           SSN  Test1  Test2  Test3  Test4  Final  Grade
1    Alfred      University   123-12-1234     41     97     96     97     48     D+
   Aloysius ===>
   Last name   First name             SSN  Test1  Test2  Test3  Test4  Final  Grade
0   Alfalfa     Aloysius     123-45-6789     40     90    100     83     49     D-
   Andrew ===>
   Last name First name               SSN  Test1  Test2  Test3  Test4  Final Grade
8   Airpump     Andrew       223-45-6789     49      1     90    100     83     A
   Electric ===>
   Last name   First name             SSN  Test1  Test2  Test3  Test4  Final  Grade
3   Android     Electric     087-65-4321     42     23     36     45     47     B-
   Fred ===>
   Last name First name                 SSN  Test1  Test2  Test3  Test4  Final  Grade
4   Bumpkin       Fred         456-78-9012     43     78     88     77     45     A-
  Benny ===>
    Last name First name                SSN  Test1  Test2  Test3  Test4  Final  Grade
13  Franklin      Benny        234-56-2890     50      1     90     80     90     B-
  Ima ===>
    Last name First name                  SSN  Test1  Test2  Test3  Test4  Final  Grade
12  Elephant        Ima          456-71-9012     45      1     78     88     77     B-
 Art ===>
     Last name First name                  SSN  Test1  Test2  Test3  Test4  Final  Grade
10  Carnivore        Art          565-89-0123     44      1     80     60     40     D+
 Harvey ===>
     Last name First name               SSN  Test1  Test2  Test3  Test4  Final Grade
15  Heffalump     Harvey       632-79-9439     30      1     20     30     40     C
```

##### Selecting a Group

In order to select a group, below function can be applied:
- `grouped_df.get_group(name, obj=None)`: constructs DataFrame from group with provided name.
  - `name`: object. The name of the group to get as a DataFrame.
  - `obj`: DataFrame. The DataFrame to take the DataFrame out of. If it is None, the object groupby was called on will be used.

```
import pandas as pd
import numpy as np

df = pd.read_csv('grades.csv')
print('The Original DataFrame:\n', df.to_string())

grouped_df = df.groupby('Grade')
print("\nGrouped DataFrame by Grade:\n", grouped_df.groups)

print('\nSelecting a specified group:\n', grouped_df.get_group('D+').to_string())



(output):
The Original DataFrame:
     Last name   First name            SSN  Test1  Test2  Test3  Test4  Final Grade
0     Alfalfa     Aloysius    123-45-6789     40     90    100     83     49    D-
1      Alfred   University    123-12-1234     41     97     96     97     48    D+
2       Gerty       Gramma    567-89-0123     41     80     60     40     44     C
3     Android     Electric    087-65-4321     42     23     36     45     47    B-
4     Bumpkin         Fred    456-78-9012     43     78     88     77     45    A-
5      Rubble        Betty    234-56-7890     44     90     80     90     46    C-
6      Noshow        Cecil    345-67-8901     45     11     -1      4     43     F
7        Buff          Bif    632-79-9939     46     20     30     40     50    B+
8     Airpump       Andrew    223-45-6789     49      1     90    100     83     A
9      Backus          Jim    143-12-1234     48      1     97     96     97    A+
10  Carnivore          Art    565-89-0123     44      1     80     60     40    D+
11      Dandy          Jim    087-75-4321     47      1     23     36     45    C+
12   Elephant          Ima    456-71-9012     45      1     78     88     77    B-
13   Franklin        Benny    234-56-2890     50      1     90     80     90    B-
14     George          Boy    345-67-3901     40      1     11     -1      4     B
15  Heffalump       Harvey    632-79-9439     30      1     20     30     40     C

Grouped DataFrame by Grade:
 {'A': [8], 'A+': [9], 'A-': [4], 'B': [14], 'B+': [7], 'B-': [3, 12, 13], 'C': [2, 15], 'C+': [11], 'C-': [5], 'D+': [1, 10], 'D-': [0], 'F': [6]}

Selecting a group:
     Last name   First name            SSN  Test1  Test2  Test3  Test4  Final Grade
1      Alfred   University    123-12-1234     41     97     96     97     48    D+
10  Carnivore          Art    565-89-0123     44      1     80     60     40    D+
```


##### Aggregations on a Group

Aggregating operation can be used with groupby function.

```
import pandas as pd
import numpy as np

df = pd.read_csv('grades.csv')
print('The Original DataFrame:\n', df.to_string())

grouped_df = df.groupby('Grade')
print("\nGrouped DataFrame by Grade:\n", grouped_df.groups)

print('\nAggregating over Final score:\n', grouped_df['Final'].agg([np.mean, np.max]))



(output):
The Original DataFrame:
     Last name   First name            SSN  Test1  Test2  Test3  Test4  Final Grade
0     Alfalfa     Aloysius    123-45-6789     40     90    100     83     49    D-
1      Alfred   University    123-12-1234     41     97     96     97     48    D+
2       Gerty       Gramma    567-89-0123     41     80     60     40     44     C
3     Android     Electric    087-65-4321     42     23     36     45     47    B-
4     Bumpkin         Fred    456-78-9012     43     78     88     77     45    A-
5      Rubble        Betty    234-56-7890     44     90     80     90     46    C-
6      Noshow        Cecil    345-67-8901     45     11     -1      4     43     F
7        Buff          Bif    632-79-9939     46     20     30     40     50    B+
8     Airpump       Andrew    223-45-6789     49      1     90    100     83     A
9      Backus          Jim    143-12-1234     48      1     97     96     97    A+
10  Carnivore          Art    565-89-0123     44      1     80     60     40    D+
11      Dandy          Jim    087-75-4321     47      1     23     36     45    C+
12   Elephant          Ima    456-71-9012     45      1     78     88     77    B-
13   Franklin        Benny    234-56-2890     50      1     90     80     90    B-
14     George          Boy    345-67-3901     40      1     11     -1      4     B
15  Heffalump       Harvey    632-79-9439     30      1     20     30     40     C

Grouped DataFrame by Grade:
 {'A': [8], 'A+': [9], 'A-': [4], 'B': [14], 'B+': [7], 'B-': [3, 12, 13], 'C': [2, 15], 'C+': [11], 'C-': [5], 'D+': [1, 10], 'D-': [0], 'F': [6]}

Aggregating over Final score:
             mean  amax
Grade                 
A      83.000000    83
A+     97.000000    97
A-     45.000000    45
B       4.000000     4
B+     50.000000    50
B-     71.333333    90
C      42.000000    44
C+     45.000000    45
C-     46.000000    46
D+     44.000000    48
D-     49.000000    49
F      43.000000    43
```


##### Transformation on a Group

The transform method returns an object that is indexed the same (same size) as the one being grouped.

- `df.transform(func, axis=0, *args, **kwargs)`: calls `func` on self producing a DataFrame with transformed values.
  - `func`: function, str, list or dict. Function to use for aggregating the data. Accepted combinations are:
    - function
    - string function name
    - list of functions and/or function names, e.g. `[np.sum, 'mean']`
    - dict of axis labels -> functions, function names or list of such.
  - `axis`: {0 or 'index', 1 or 'columns'}.
  - `*args`: Positional arguments to pass to `func`.
  - `**kwargs`: Keyword arguments to pass to `func`.


```
import pandas as pd
import numpy as np

df = pd.read_csv('grades.csv')
print('The Original DataFrame:\n', df.to_string())

grouped_df = df.groupby('Grade')
print("\nGrouped DataFrame by Grade:\n", grouped_df.groups)


transformed = grouped_df.transform(lambda x: (x - x.mean()) / x.std())
print("\nTrnadormed DataFrame:\n", transformed)



(output):
The Original DataFrame:
     Last name   First name            SSN  Test1  Test2  Test3  Test4  Final Grade
0     Alfalfa     Aloysius    123-45-6789     40     90    100     83     49    D-
1      Alfred   University    123-12-1234     41     97     96     97     48    D+
2       Gerty       Gramma    567-89-0123     41     80     60     40     44     C
3     Android     Electric    087-65-4321     42     23     36     45     47    B-
4     Bumpkin         Fred    456-78-9012     43     78     88     77     45    A-
5      Rubble        Betty    234-56-7890     44     90     80     90     46    C-
6      Noshow        Cecil    345-67-8901     45     11     -1      4     43     F
7        Buff          Bif    632-79-9939     46     20     30     40     50    B+
8     Airpump       Andrew    223-45-6789     49      1     90    100     83     A
9      Backus          Jim    143-12-1234     48      1     97     96     97    A+
10  Carnivore          Art    565-89-0123     44      1     80     60     40    D+
11      Dandy          Jim    087-75-4321     47      1     23     36     45    C+
12   Elephant          Ima    456-71-9012     45      1     78     88     77    B-
13   Franklin        Benny    234-56-2890     50      1     90     80     90    B-
14     George          Boy    345-67-3901     40      1     11     -1      4     B
15  Heffalump       Harvey    632-79-9439     30      1     20     30     40     C

Grouped DataFrame by Grade:
 {'A': [8], 'A+': [9], 'A-': [4], 'B': [14], 'B+': [7], 'B-': [3, 12, 13], 'C': [2, 15], 'C+': [11], 'C-': [5], 'D+': [1, 10], 'D-': [0], 'F': [6]}

Trnadormed DataFrame:
        Test1     Test2     Test3     Test4     Final
0        NaN       NaN       NaN       NaN       NaN
1  -0.707107  0.707107  0.707107  0.707107  0.707107
2   0.707107  0.707107  0.707107  0.707107  0.707107
3  -0.907265  1.154701 -1.128553 -1.136901 -1.103404
4        NaN       NaN       NaN       NaN       NaN
5        NaN       NaN       NaN       NaN       NaN
6        NaN       NaN       NaN       NaN       NaN
7        NaN       NaN       NaN       NaN       NaN
8        NaN       NaN       NaN       NaN       NaN
9        NaN       NaN       NaN       NaN       NaN
10  0.707107 -0.707107 -0.707107 -0.707107 -0.707107
11       NaN       NaN       NaN       NaN       NaN
12 -0.164957 -0.577350  0.352673  0.743358  0.256957
13  1.072222 -0.577350  0.775880  0.393543  0.846447
14       NaN       NaN       NaN       NaN       NaN
15 -0.707107 -0.707107 -0.707107 -0.707107 -0.707107
```


##### Filtration on a Group
The filter method returns a subset of the original object.

- `df.filter(items=None, like=None, regex=None, axis=None)`: subsets the dataframe rows or columns according to the specified index labels.
  - `items`: list-like. It keeps labels from axis which are in items.
  - `like`: str. It keeps labels from axis for which "like in label == True".
  - `regex`: str. It keeps labels from axis for which re.search(regex, label) == True.
  - `axis`: {0 or ‘index’, 1 or ‘columns’, None}.

```
import pandas as pd
import numpy as np

df = pd.read_csv('grades.csv')
print('The Original DataFrame:\n', df.to_string())

grouped_df = df.groupby('Grade')
print("\nGrouped DataFrame by Grade:\n", grouped_df.groups)

print("\nFiltered DataFrame:\n", grouped_df.filter(lambda x: x['Final'].mean() > 75))



(output):
The Original DataFrame:
     Last name   First name            SSN  Test1  Test2  Test3  Test4  Final Grade
0     Alfalfa     Aloysius    123-45-6789     40     90    100     83     49    D-
1      Alfred   University    123-12-1234     41     97     96     97     48    D+
2       Gerty       Gramma    567-89-0123     41     80     60     40     44     C
3     Android     Electric    087-65-4321     42     23     36     45     47    B-
4     Bumpkin         Fred    456-78-9012     43     78     88     77     45    A-
5      Rubble        Betty    234-56-7890     44     90     80     90     46    C-
6      Noshow        Cecil    345-67-8901     45     11     -1      4     43     F
7        Buff          Bif    632-79-9939     46     20     30     40     50    B+
8     Airpump       Andrew    223-45-6789     49      1     90    100     83     A
9      Backus          Jim    143-12-1234     48      1     97     96     97    A+
10  Carnivore          Art    565-89-0123     44      1     80     60     40    D+
11      Dandy          Jim    087-75-4321     47      1     23     36     45    C+
12   Elephant          Ima    456-71-9012     45      1     78     88     77    B-
13   Franklin        Benny    234-56-2890     50      1     90     80     90    B-
14     George          Boy    345-67-3901     40      1     11     -1      4     B
15  Heffalump       Harvey    632-79-9439     30      1     20     30     40     C

Grouped DataFrame by Grade:
 {'A': [8], 'A+': [9], 'A-': [4], 'B': [14], 'B+': [7], 'B-': [3, 12, 13], 'C': [2, 15], 'C+': [11], 'C-': [5], 'D+': [1, 10], 'D-': [0], 'F': [6]}

Filtered DataFrame:
   Last name First name            SSN  Test1  Test2  Test3  Test4  Final Grade
8   Airpump     Andrew    223-45-6789     49      1     90    100     83     A
9    Backus        Jim    143-12-1234     48      1     97     96     97    A+
```
