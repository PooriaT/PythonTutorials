---
id: 15_categorical_data
title: Categorical Data
sidebar_label: Categorical Data
slug: /15_categorical_data
---

---

In reality, our data includes different types, from numeric to text format.  Categorical is a kind of pandas data type related to categorical variables in statistics. A categorical variable can take on a limited and usually fixed number of possible values. Examples are gender, social class, blood type, or observation time.

The categorical data type can be useful in the bellow cases:
- A string variable consisting of only a few different values. Converting such a string variable to a categorical variable will save some memory.
- The lexical order of a variable is not the same as the logical order.

There are two main ways of creating categorical objects. One is specifying the dtype as `categoty`, and the other uses `pandas.categorical` function.


```
import pandas as pd

df = pd.DataFrame({
    'A':['A0','A1','A0','A1'],
    'B':['B0','B1','B2','B3']
    },
    dtype="category"
)

print("Original dataFrame:\n",df)
print("\nDtype of DataFrame:\n", df.dtypes)



(output):
Original dataFrame:
     A   B
0  A0  B0
1  A1  B1
2  A0  B2
3  A1  B3

Dtype of DataFrame:
 A    category
B    category
dtype: object
```


- `pd.Categorical(values, categories=None, ordered=None, dtype=None)`: represents a categorical variable in classic R / S-plus fashion. All values of the `Categorical` are either in `categories` or `np.nan`. Assigning values outside of `categories` will raise a `ValueError`. Order is defined by the order of the `categories`, not lexical order of the values.
  - `values`: list-like. The values of the categorical. If categories are given, values not in categories will be replaced with `NaN`.
  - `categories`: Index-like (unique) (optional). The unique categories for this categorical. If not given, the categories are assumed to be the unique values of `values` (sorted, if possible, otherwise in the order in which they appear).
  - `ordered`: bool. Whether or not this categorical is treated as a ordered categorical.
  - `dtype`: CategoricalDtype. An instance of `CategoricalDtype` to use for this categorical.


- Attributes of `pandas.Categorical`:
  - `categories`: Index. The categories of this categorical.
  - `codes`: ndarray. The codes (integer positions, which point to the categories) of this categorical, read only.
  - `ordered`: bool. Whether or not this Categorical is ordered.
  - `dtype`: CategoricalDtype. The instance of `CategoricalDtype` storing the `categories` and `ordered`.


```
import pandas as pd

cat = pd.Categorical(['a','b','c','d'])
print("Simple Categorical structure:\n", cat)

#Considering Categories
cat = pd.Categorical(['a','b','c','d','a','f','c','d','a','b','h'],
                    categories=['b','c','d','a'])
print("\nCategorical with Categories flag:\n", cat)

#Considering Categories and ordered
cat = pd.Categorical(['a','b','c','d','a','f','c','d','a','b','h'],
                    categories=['b','c','d','a'], ordered=True)
print("\nCategorical with Categories and ordered flags:\n", cat)

### Using Categotical attributes
print()
print("-"*50)
print("\nCategories Attribute:", cat.categories)
print("The Codes Attribute:", cat.codes)
print("The dtype Attribute:", cat.dtype)
print("The Ordered Attribute:", cat.ordered)



(output):
Simple Categorical structure:
 ['a', 'b', 'c', 'd']
Categories (4, object): ['a', 'b', 'c', 'd']

Categorical with Categories flag:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (4, object): ['b', 'c', 'd', 'a']

Categorical with Categories and ordered flags:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (4, object): ['b' < 'c' < 'd' < 'a']

--------------------------------------------------

Categories Attribute: Index(['b', 'c', 'd', 'a'], dtype='object')
The Codes Attribute: [ 3  0  1  2  3 -1  1  2  3  0 -1]
The dtype Attribute: category
The Ordered Attribute: True
```

Now, we can use categorical structure inside the DataFrame:

```
import pandas as pd
import numpy as np

cat = pd.Categorical(['a','b','c','d','a','f','c','d','a','b','h'],
                    categories=['b','c','d','a'])
print("\nCategorical with Categories flag:\n", cat)

df = pd.DataFrame({'cat': cat, 'A': np.random.randn(11)})
print("\nDataFrame:\n", df)

#Using describe method
print("\nDataFrame Description:\n", df.describe())
print("\nCategorical Description:\n", df['cat'].describe())



(output):
Categorical with Categories flag:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (4, object): ['b', 'c', 'd', 'a']

DataFrame:
     cat         A
0     a -2.612821
1     b  0.191842
2     c -2.129864
3     d  1.630454
4     a -0.930915
5   NaN -0.189619
6     c -1.030206
7     d -0.298352
8     a  0.055784
9     b -1.559509
10  NaN  2.238140

DataFrame Description:
                A
count  11.000000
mean   -0.421370
std     1.469783
min    -2.612821
25%    -1.294857
50%    -0.298352
75%     0.123813
max     2.238140

Categorical Description:
 count     9
unique    4
top       a
freq      3
Name: cat, dtype: object
```

After creating  categorical variables, it is possible to rename, append or delete categories. To do so, we can use `categories` attribute, `.add_categories()` and `.remove_categories()`

**Renaming**
```
import pandas as pd

cat = pd.Categorical(['a','b','c','d','a','f','c','d','a','b','h'],
                    categories=['b','c','d','a'])
print("\nCategorical with Categories flag:\n", cat)

#Renaming Categories
cat.categories = ['a', 'f', 'd', 'h']
print("\nRenamed categories:\n", cat)



(output):
Categorical with Categories flag:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (4, object): ['b', 'c', 'd', 'a']

Renamed categories:
 ['h', 'a', 'f', 'd', 'h', ..., 'f', 'd', 'h', 'a', NaN]
Length: 11
Categories (4, object): ['a', 'f', 'd', 'h']
```

**Appending**
```
import pandas as pd

cat = pd.Categorical(['a','b','c','d','a','f','c','d','a','b','h'],
                    categories=['b','c','d','a'])
print("\nCategorical with Categories flag:\n", cat)

#Appending Categories
cat.add_categories('h',inplace=True)
print("\nAppended categories:\n", cat)



(output):
Categorical with Categories flag:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (4, object): ['b', 'c', 'd', 'a']

Appended categories:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (5, object): ['b', 'c', 'd', 'a', 'h']
```


**Deleting**
```
import pandas as pd

cat = pd.Categorical(['a','b','c','d','a','f','c','d','a','b','h'],
                    categories=['b','c','d','a'])
print("\nCategorical with Categories flag:\n", cat)

#Appending Categories
cat.remove_categories('a',inplace=True)
print("\nDeleted categories:\n", cat)



(output):

Categorical with Categories flag:
 ['a', 'b', 'c', 'd', 'a', ..., 'c', 'd', 'a', 'b', NaN]
Length: 11
Categories (4, object): ['b', 'c', 'd', 'a']

Deleted categories:
 [NaN, 'b', 'c', 'd', NaN, ..., 'c', 'd', NaN, 'b', NaN]
Length: 11
Categories (3, object): ['b', 'c', 'd']
```

* **Note that**: Comparison between categorical data is possible.
