---
id: 02_array_creation
title: Array Creation
sidebar_label: Array Creation
slug: /02_array_creation
---

---

As it was mentioned, `ndarray` (N-dimensional array type) is the most import object of Numpy module.
In order to create an array, the below syntax can be used:
`np.array(object, dtype=None, copy=True, order='K', subok=False, ndmin=0)`

- object : An array, any object exposing the array interface,
- dtype : data-type (optional). If not given, then the type will be determined as the minimum type required to hold the objects in the sequence.
- copy : bool (optional). If it is true (default), then the object is copied.
- order : {'A', 'C', 'F'} (optional). A (any, default), C (row major) or F (column major).
- subok : bool (optional). If it is True, the sub-classes will be passed-through, otherwise it will be forced to return a base-class array (default).
- ndmin : int (optional). Specifies the minimum dimensions of resulting array.

Example:
```
import numpy as np

arr1 = np.array(17)
arr2 = np.array([1,2,3,4])
arr3 = np.array([[1,2],[3,4]])
arr4 = np.array([10,11,12,13], ndmin=3)
arr5 = np.array([7,8,9], dtype=float)
arr6 = np.array([1,2,3], dtype=complex)

print(type(arr1))
print(arr1)
print(arr2)
print(arr3)
print(arr4)
print(arr5)
print(arr6)


(output): <class 'numpy.ndarray'>
17
[1 2 3 4]
[[1 2]
 [3 4]]
[[[10 11 12 13]]]
[7. 8. 9.]
[1.+0.j 2.+0.j 3.+0.j]
```

#### Array Attributes

In working with numpy arrays, there are several attributes which return useful information about the created array.
- `ndarray.ndim`: returns the number of array dimensions
- `ndarray.shape`: returns a tuple of array's dimensions
- `numpy.itemsize`: returns the length (Bytes) of each item of array based on the data type .

Example:
```
import numpy as np

arr = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])

print(arr)
print("Dimensions: ", arr.ndim)
print("Array Shape: ", arr.shape)
print("Item size: ", arr.itemsize)


(output): [[[1 2]
  [3 4]]

 [[5 6]
  [7 8]]]
Dimensions:  3
Array Shape:  (2, 2, 2)
Item size:  4
```

#### Array Creation Routines

There are several routines in which a new template of `ndarray` object can be created.

- `numpy.empty(shape, dtype=float, order='C')`: Creating an uninitialized array.
- `numpy.zeros(shape, dtype=float, order='C')`: Creating an array which all of its items are zero.
- `numpy.ones(shape, dtype=float, order='C')`:  Creating an array which all of its items are one.

Example:
```
import numpy as np

arr_empty = np.empty([2,4])
arr_zeros = np.zeros([2,2,1])
arr_ones = np.ones(10)

print("arr_empty= ", arr_empty)
print("arr_zeros= ", arr_zeros)
print("arr_ones= ", arr_ones)


(outputs):
arr_empty=  [[0.00000000e+000 0.00000000e+000 0.00000000e+000 0.00000000e+000]
 [0.00000000e+000 6.40309077e-321 1.67793274e+243 5.29369371e+180]]
arr_zeros=  [[[0.]
  [0.]]

 [[0.]
  [0.]]]
arr_ones=  [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
```

#### Array of Existing data

It is possible to create an array from existing data. To do so, the below syntax is used. This syntax can return an array interpretation of `a`.
`np.asarray(a, dtype=None, order=None)`

- a : Input data, in any form that can be converted to an array such as Python list.
- dtype : data-type (optional). If not given, then the type will be determined as the minimum type required to hold the objects in the sequence.
- order : {'A', 'C', 'F'} (optional). A (any, default), C (row major) or F (column major).

Example:
```
import numpy as np

a1 = [1,2,3]
a2 = (4,5,6)
arr1 = np.asarray(a1)
arr2 = np.asarray(a2)

print(arr1, type(arr1))
print(arr2, type(arr2))


(output):
[1 2 3] <class 'numpy.ndarray'>
[4 5 6] <class 'numpy.ndarray'>
```

#### Array of Numerical Range

We can create a new array object out of numerical range.

- `numpy.arange([start,] stop[, step,], dtype=None)`: will return evenly spaced values within a specified interval (*[start, stop)*).
  - start : integer or real (optional). Start of interval. Default value is 0.
  - stop : integer or real.   End of interval
  - step : integer or real (optional). Spacing between values.
  - dtype : data-type (optional).


- `numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None, axis=0)`: will return `num` evenly spaced samples over a specified interval (*[start, stop]*).
  - start : array_like. The starting value of the sequence.
  - stop : The end value of the sequence, unless `endpoint` is set to False.
  - num : int (optional). Number of samples to generate which must be non-negative.
  - endpoint : bool (optional). If True, `stop` is the last sample. Otherwise, it is not included.
  - retstep : bool (optional). If True, return (`samples`, `step`), where `step` is the spacing between samples.
  - dtype : data-type (optional). The inferred dtype will never be an integer if it is not chosen.
  - axis : int (optional). he axis in the result to store the samples.


- `numpy.logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None, axis=0)`: will return `num` evenly spaced samples on a log scale.
  - start : array_like. `base`<sup>`start`</sup> is the starting value of the sequence.
  - stop : array_like. `base`<sup>`start` is the final value of the sequence, unless `endpoint` is False.
  - num : int (optional). Number of samples to generate which must be non-negative.
  - endpoint : bool (optional). If True, `stop` is the last sample. Otherwise, it is not included.
  - base: array_like (optional). The base of the log space.
  - dtype : data-type (optional). The inferred dtype will never be an integer if it is not chosen.
  - axis : int (optional). he axis in the result to store the samples.


Example:
```
import numpy as np

arr_ar = np.arange(7,30,4)
arr_line = np.linspace(2,5,5, endpoint=False)
arr_log = np.logspace(2,5,5, endpoint=False)

print("numpy.arange: ", arr_ar)
print("numpy.linspace:", arr_line)
print("numpy.logspace:", arr_log)



(output):
numpy.arange:  [ 7 11 15 19 23 27]
numpy.linspace: [2.  2.6 3.2 3.8 4.4]
numpy.logspace: [  100.           398.10717055  1584.89319246  6309.5734448
 25118.8643151 ]

```
