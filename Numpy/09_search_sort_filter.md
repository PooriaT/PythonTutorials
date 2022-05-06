---
id: 09_search_sort_filter
title: Search, Sort and Filter
sidebar_label: Search, Sort and Filter
slug: /09_search_sort_filter
---

---

Numpy consists of a variety of functions to sort an array or search and filter items inside an array.

### sort

Literally, sorting means the put the elements in an ordered sequence (such as numeric or alphabetical ascending or descending).

#### `numpy.sort()`
This function will return a sorted copy of an array.
- `numpy.sort(a, axis=-1, kind=None, order=None)`
- `a`: Array to be sorted.
- `axis`: int or None (optional). Axis along which to sort.
- `kind`: {'quicksort', 'mergesort', 'heapsort', 'stable'} (optional). Sorting algorithm.
- `order`: str or list of str (optional). When `a` is an array with fields defined, this argument specifies which fields to compare first, second, etc.

```
import numpy as np

print("Sorting alphabetic array...")
a = np.array(['John', 'Sarah', 'Adam'])
print(np.sort(a))

print("\nSorting 1D numeric array... ")
a = np.array([43,23,12,56,22,12,17])
print(np.sort(a))

print("\nSorting 2D numeric array... ")
a = np.array([[4,6,2,5], [3,1,3,10]])
print(np.sort(a))

print("\nSorting 2D numeric array over axis=0... ")
a = np.array([[4,6,2,5], [3,1,3,10]])
print(np.sort(a, axis=0))



(output):
Sorting alphabetic array...
['Adam' 'John' 'Sarah']

Sorting 1D numeric array...
[12 12 17 22 23 43 56]

Sorting 2D numeric array...
[[ 2  4  5  6]
 [ 1  3  3 10]]

Sorting 2D numeric array over axis=0...
[[ 3  1  2  5]
 [ 4  6  3 10]]
```

#### `numpy.argsort()`
This function will return the indices that would sort an array.
- `numpy.argsort(a, axis=-1, kind=None, order=None)`
- `a`: Array to be sorted.
- `axis`: int or None (optional). Axis along which to sort.
- `kind`: {'quicksort', 'mergesort', 'heapsort', 'stable'} (optional). Sorting algorithm.
- `order`: str or list of str (optional). When `a` is an array with fields defined, this argument specifies which fields to compare first, second, etc.

```
import numpy as np


print("Sorting alphabetic array...")
a = np.array(['John', 'Sarah', 'Adam'])
print("Indices of sorted array", np.argsort(a))

print("\nSorting 1D numeric array... ")
a = np.array([43,23,12,56,22,12,17])
print("Indices of sorted array", np.argsort(a))

print("\nSorting 2D numeric array... ")
a = np.array([[4,6,2,5], [3,1,3,10]])
print("Indices of sorted array", np.argsort(a))

print("\nSorting 2D numeric array over axis=0... ")
a = np.array([[4,6,2,5], [3,1,3,10]])
print("Indices of sorted array", np.argsort(a, axis=0))



(output):
Sorting alphabetic array...
Indices of sorted array [2 0 1]

Sorting 1D numeric array...
Indices of sorted array [2 5 6 4 1 0 3]

Sorting 2D numeric array...
Indices of sorted array [[2 0 3 1]
 [1 0 2 3]]

Sorting 2D numeric array over axis=0...
Indices of sorted array [[1 1 0 0]
 [0 0 1 1]]
```

### Search
In `numpy`, we can search for an specific values and return its index.

#### `numpy.where()`
This function will return elements chosen from `x` or `y` where `condition` is Ture.
- `numpy.where(condition, [x, y])`
- `condition`: array_like, bool. Where True, yield `x`, otherwise yield `y`.
- `x`, `y` : array_like.

```
import numpy as np

a = np.arange(30)
print("Even Number only: ", np.where(a%2 == 0))



(output):
Even Number only:  (array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28],
      dtype=int64),)
```

#### `numpy.searchsorted()`
This Function will find indices where elements should be inserted to maintain order. (Binary Search)
- `numpy.searchsorted(a, v, side='left', sorter=None)`
- `a`: 1D input array. If `sorter` is None, then it must be sorted in ascending order, otherwise `sorter` must be an array of indices that sort it.
- `v`: Values to insert into `a`.
- `side`: {'left', 'right'} (optional). If 'left', the index of the first suitable location found is given, otherwise return the last such index.
- `sorter`: 1-D array_like (optional)

```
import numpy as np

a = np.arange(30)
print('Poistion of numner 7: ', np.searchsorted(a, 7))
print('Poistion of numner 7 from right side: ', np.searchsorted(a, 7, side='right'))



(output):
Poistion of numner 7:  7
Poistion of numner 7 from right side:  8
```

#### `numpy.extract()`
This function will return the elements of an array that satisfy some condition.
- `numpy.extract(condition, arr)`
- `condition` : An array whose nonzero or True entries indicate the elements of `arr` to extract.
- `arr` : Input array of the same size as `condition`.

```
import numpy as np

a = np.arange(30)
print("Odd number: ",np.extract(a%2 == 1, a))



(output):
Odd number:  [ 1  3  5  7  9 11 13 15 17 19 21 23 25 27 29]
```

#### `numpy.argmax()` and `numpy.argmin()`
This two function will return the indices of the maximum and minimum values along an axis, respectively.
- `np.argmax(a, axis=None, out=None)`
- `np.argmin(a, axis=None, out=None)`
- `a`: Input array.
- `axis`: int (optional)
- `out`: array (optional). If provided, the result will be inserted into this array.

```
import numpy as np

a = np.array([[10,40,20,33],[55,17,19,27,]])
print("Index of maximum value: ",np.argmax(a))
print("Index of minimum value: ",np.argmin(a))
print("Index of maximum value over axis=1: ",np.argmax(a, axis=1))
print("Index of minimum value over axis=1:: ",np.argmin(a, axis=1))



(output):
Index of maximum value:  4
Index of minimum value:  0
Index of maximum value:  [1 0]
Index of minimum value:  [0 1]
```

#### `numpy.nonzero()`
This function will return the indices of the elements that are non-zero.
- `numpy.nonzero(a)`
- `a`: Input array.

```
import numpy as np

a = np.array([[4,0,4,2], [0,3,0,9]])
print(np.nonzero(a))


(output):
(array([0, 0, 0, 1, 1], dtype=int64), array([0, 2, 3, 1, 3], dtype=int64))
```

### Filter
Filtering means to get some desired elements out of the an array and creating a new array wit them. This can be done with *Boolean index list* in `numpy`. In this case, if the value of an index is `True`, the element will be contained in the filtered array, otherwise it will be excluded.

```
import numpy as np

a = np.array([10,40,20,33,55,17,19,27])

filtered_arr1 = [True, False, True, False, True, False, True, False]
print("Filter 1: ", a[filtered_arr1])

filtered_arr2 = a > 25
print("Filter 2: ", a[filtered_arr2])



(output):
Filter 1:  [10 20 55 19]
Filter 2:  [40 33 55 27]
```
