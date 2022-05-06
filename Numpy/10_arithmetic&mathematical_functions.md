---
id: 10_math_functions
title: Mathematical and Statistical Functions
sidebar_label: Mathematical and Statistical Functions
slug: /10_math_functions
---

---

### Arithmetic Functions
There are several arithmetic operations in `numpy` which can be applied on arrays.

- `numpy.add(*args, **kwargs)`: adds arguments element-wise.
- `numpy.subtract(*args, **kwargs)`: subtracts arguments, element-wise.
- `numpy.multiply(*args, **kwargs)`: multiplies arguments element-wise
- `numpy.divide(*args, **kwargs)`: returns a true division of the inputs, element-wise.
- `numpy.mod(*args, **kwargs)`: returns element-wise remainder of division.
- `numpy.power(*args, **kwargs)`: first array elements raised to powers from second array, element-wise.
- `numpy.reciprocal(*args, **kwargs)`: return the reciprocal of the argument, element-wise.



- `numpy.real(val)`: returns the real part of the complex argument. `val ` is an input array.
- `numpy.imag(val)`: Return the imaginary part of the complex argument. `val ` is an input array.
- `numpy.conj(*args, **kwargs)`: returns the complex conjugate, element-wise.
- `numpy.angle(z, deg=False)`: returns the angle of the complex argument. `z` is an array of complex numbers. `deg` is a bool flag which the output will be in degrees if it is True, otherwise it will be radians

Examples:
```
import numpy as np

a = np.arange(1,5)
b = np.arange(11,15)

print("a= ", a)
print("b= ", b)
print("\nBasic Arithmetic Operations ...")
print("Addition: ", np.add(a,b))
print("Subtraction: ", np.subtract(a,b))
print("Multiplication: ", np.multiply(a,b))
print("Division: ", np.divide(a,b))
print("b Power by a", np.power(b,a))
print("b mod a: ", np.mod(b,a))
print("Reciprocal of a: ", np.reciprocal(a))

a = np.array([1+1j, 5j, 4.5, 12+2.5j])
print("\na= ", a)
print("Real part of elements: ", np.real(a))
print("Imaginary part of elemenst: ", np.imag(a))
print("Conjugate of a: ", np.conj(a))
print("Degree of elements: ", np.angle(a, deg=True))



(output):
a=  [1 2 3 4]
b=  [11 12 13 14]

Basic Arithmetic Operations ...
Addition:  [12 14 16 18]
Subtraction:  [-10 -10 -10 -10]
Multiplication:  [11 24 39 56]
Division:  [0.09090909 0.16666667 0.23076923 0.28571429]
b Power by a [   11   144  2197 38416]
b mod a:  [0 0 1 2]
Reciprocal of a:  [1 0 0 0]

a=  [ 1. +1.j   0. +5.j   4.5+0.j  12. +2.5j]
Real part of elements:  [ 1.   0.   4.5 12. ]
Imaginary part of elemenst:  [1.  5.  0.  2.5]
Conjugate of a:  [ 1. -1.j   0. -5.j   4.5-0.j  12. -2.5j]
Degree of elements:  [45.         90.          0.         11.76828893]
```
### Mathematical Functions

Numpy supports various mathematical operations and functions, such as trigonometric functions, rounding functions and so on.

#### Trigonometric Functions
This function works with **Radians**.

```
import numpy as np

pi = np.pi #PI number

a = np.array([0, 30, 45, 60, 90])

# Converting degrees to radinas
a_rad = np.radians(a)
print("Radians of a: ", a_rad)

print("sin(x): ", np.sin(a_rad))
print("cos(x): ", np.cos(a_rad))
print("tan(x): ", np.tan(a_rad))


b = np.array([0 , 0.5, 0.707, 0.866, 1])
# In order to convert radian to degree, np.degrees() function can be used
print("arcsin(x): ", np.degrees(np.arcsin(b)))
print("arccos(x): ", np.degrees(np.arccos(b)))
print("arctan(x): ", np.degrees(np.arctan(b)))



(output):
Radians of a:  [0.         0.52359878 0.78539816 1.04719755 1.57079633]
sin(x):  [0.         0.5        0.70710678 0.8660254  1.        ]
cos(x):  [1.00000000e+00 8.66025404e-01 7.07106781e-01 5.00000000e-01
 6.12323400e-17]
tan(x):  [0.00000000e+00 5.77350269e-01 1.00000000e+00 1.73205081e+00
 1.63312394e+16]
arcsin(x):  [ 0.         30.         44.99134834 59.99708907 90.        ]
arccos(x):  [90.         60.         45.00865166 30.00291093  0.        ]
arctan(x):  [ 0.         26.56505118 35.26031074 40.89256291 45.        ]
```

#### Rounding Functions
There are several rounding functions in `numpy`:
- `numpy.around(a, decimals=0, out=None)`: evenly round to the given number of decimals
  - `a`: Input array
  - `decimals`: int (optional). Number of decimal places to round to. If
    decimals is negative, it specifies the number of positions to the left of the decimal point.
  - `out`: ndarray (optional). Alternative output array in which to place the result.


- `numpy.ceil(*args, **kwargs)`: returns the ceiling of the input, element-wise.
- `numpy.floor(*args, **kwargs)`: returns the floor of the input, element-wise.

```
import numpy as np

a = np.array([1.5, 1766, 1.73, -2.3, -3.15, 0.47])

print("around with default decimals: ", np.around(a))
print("around with decimals=1: ", np.around(a, decimals = 1))
print("around with decimals=-1: ", np.around(a, decimals = -1))

print("Ceil of a:", np.ceil(a))
print("floor of a:", np.floor(a))



(output):
around with default decimals:  [   2. 1766.    2.   -2.   -3.    0.]
around with decimals=1:  [ 1.500e+00  1.766e+03  1.700e+00 -2.300e+00 -3.200e+00  5.000e-01]
around with decimals=-1:  [   0. 1770.    0.   -0.   -0.    0.]
Ceil of a: [ 2.000e+00  1.766e+03  2.000e+00 -2.000e+00 -3.000e+00  1.000e+00]
floor of a: [ 1.000e+00  1.766e+03  1.000e+00 -3.000e+00 -4.000e+00  0.000e+00]
```

### Statistical Functions

- `numpy.amin(a, axis=None, out=None, keepdims=<no value>, initial=<no value>, where=<no value>)`: returns the minimum of an array or minimum along an axis.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left in the result as dimensions with size one.
  - `initial`: scalar (optional). The maximum value of an output element.
  - `where`: array_like of bool (optional). Elements to compare for the minimum.


- `numpy.amax(a, axis=None, out=None, keepdims=<no value>, initial=<no value>, where=<no value>)`: returns the maximum of an array or maximum along an axis.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left
  in the result as dimensions with size one.
  - `initial`: scalar (optional). The minimum  value of an output element.
  - `where`: array_like of bool (optional). Elements to compare for the maximum.


- `numpy.ptp(a, axis=None, out=None, keepdims=<no value>)`: returns the range of values (maximum - minimum) along an axis.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left
  in the result as dimensions with size one.


- `numpy.median(a, axis=None, out=None, overwrite_input=False, keepdims=False)`: returns the median of the array elements along the specified axis.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `overwrite_input`: bool (optional). If True, then allow use of memory of input array `a` for calculations.
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left
  in the result as dimensions with size one.


- `numpy.mean(a, axis=None, dtype=None, out=None, keepdims=<no value>, where=<no value>)`: returns the arithmetic mean of the array elements along the specified axis.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `dtype` : data-type (optional). Type to use in computing the mean.
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left in the result as dimensions with size one.
  - `where`: array_like of bool (optional). Elements to include in the mean.


- `numpy.average(a, axis=None, weights=None, returned=False)`: returns the weighted average along the specified axis in an array.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `weights` : array_like (optional). An array of weights associated with the values in `a`. *`avg = sum(a * weights) / sum(weights)`*.
  - `returned` : bool (optional). If `True`, the tuple (`average`, `sum_of_weights`) is returned, otherwise only the average is returned.


- `numpy.std(a, axis=None, dtype=None, out=None, ddof=0, keepdims=<no value>, where=<no value>,)`: returns the standard deviation, a measure of the spread of a distribution, of the array elements along the specified axis
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `dtype` : data-type (optional). Type to use in computing the mean.
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `ddof` : int (optional). Means Delta Degrees of Freedom
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left in the result as dimensions with size one.
  - `where`: array_like of bool (optional). Elements to include in the standard deviation.


- `numpy.var(a, axis=None, dtype=None, out=None, ddof=0, keepdims=<no value>, where=<no value>,)`: returns the variance of the array elements, a measure of the spread of a distribution, along the specified axis.
  - `a`: Input array.
  - `axis`: None, int or tuple of int (optional).
  - `dtype` : data-type (optional). Type to use in computing the mean.
  - `out`: ndarray (optional). Alternative output array in which to place the result.
  - `ddof` : int (optional). Means Delta Degrees of Freedom
  - `keepdims` : bool (optional). If it is True, the axes which are reduced are left in the result as dimensions with size one.
  - `where`: array_like of bool (optional). Elements to include in the variance.


Examples:
```
import numpy as np

arr = np.array([[45,68,32,87], [44,17,73,59], [33,29,96,18]])

print("Amin: ", np.amin(arr))
print("Amin in axis=0: ", np.amin(arr, axis=0))
print("Amin in axis=1: ", np.amin(arr, axis=1))
print("Amax: ", np.amax(arr))
print("Amax in axis=0: ", np.amax(arr, axis=0))
print("Amax in axis=1: ", np.amax(arr, axis=1))
print("Ptp: ", np.ptp(arr))
print("Ptp in axis=0: ", np.ptp(arr, axis=0))
print("Ptp in axis=1: ", np.ptp(arr, axis=1))

print("\nMedian: ", np.median(arr))
print("Median in axis=0: ", np.median(arr, axis=0))
print("Median in axis=1: ", np.median(arr, axis=1))


print("\nMean: ", np.mean(arr))
print("Mean in axis=0: ", np.mean(arr, axis=0))
print("Mean in axis=1: ", np.mean(arr, axis=1))
print("Average: ", np.average(arr))
print("Average in axis=0: ", np.average(arr, axis=0))
print("Average in axis=1: ", np.average(arr, axis=1))

wt = np.array([[1,1,1,1], [2,2,2,1], [3,1,4,1]])
print("Average with considering weight: ", np.average(arr, weights=wt))
print("Average with considering weight in axis=0: ", np.average(arr, axis=0, weights=wt))
print("Average with considering weight in axis=1: ", np.average(arr, axis=1, weights=wt))

print("\nStandard Deviation: ", np.std(arr))
print("Standard Deviation in axis=0: ", np.std(arr, axis=0))
print("Standard Deviation in axis=1: ", np.std(arr, axis=1))

print("\nVariance: ", np.var(arr))
print("Variance in axis=0: ", np.var(arr, axis=0))
print("Variance in axis=1: ", np.var(arr, axis=1))



(output):
Amin:  17
Amin in axis=0:  [33 17 32 18]
Amin in axis=1:  [32 17 18]
Amax:  96
Amax in axis=0:  [45 68 96 87]
Amax in axis=1:  [87 73 96]
Ptp:  79
Ptp in axis=0:  [12 51 64 69]
Ptp in axis=1:  [55 56 78]

Median:  44.5
Median in axis=0:  [44. 29. 73. 59.]
Median in axis=1:  [56.5 51.5 31. ]

Mean:  50.083333333333336
Mean in axis=0:  [40.66666667 38.         67.         54.66666667]
Mean in axis=1:  [58.   48.25 44.  ]
Average:  50.083333333333336
Average in axis=0:  [40.66666667 38.         67.         54.66666667]
Average in axis=1:  [58.   48.25 44.  ]
Average with considering weight:  54.45
Average with considering weight in axis=0:  [38.66666667 32.75       80.28571429 54.66666667]
Average with considering weight in axis=1:  [58.         46.71428571 58.88888889]

Standard Deviation:  25.243673574889126
Standard Deviation in axis=0:  [ 5.43650214 21.77154106 26.47010893 28.33529405]
Standard Deviation in axis=1:  [21.13054661 20.75301183 30.52048492]

Variance:  637.2430555555555
Variance in axis=0:  [ 29.55555556 474.         700.66666667 802.88888889]
Variance in axis=1:  [446.5    430.6875 931.5   ]
```
