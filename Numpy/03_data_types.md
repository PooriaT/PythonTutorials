---
id: 03_data_types
title: Data Types
sidebar_label: Data Types
slug: /03_data_types
---

---

Compared to common data types in Python, Numpy supports more.

Below is the list of Numpy data types:
- `bool_`: Boolean
- `int_`: Integer type
- `int8`: Interger (Byte, -128 to 127)
- `int16`: Integer (-32768 to 32767)
- `int32`: Integer (-2147483648 to 2147483647)
- `int64`: Integer (-9223372036854775808 to 9223372036854775807)
- `uint8`: Unsigned integer (0 to 255)
- `uint16`: Unsigned integer (0 to 65535)
- `uint32`: Unsigned integer (0 to 4294967295)
- `uint64`: Unsigned integer (0 to 18446744073709551615)
- `float_` : Same as float64
- `float16`: float contained sign bit, 5 bits exponent and 10 bits decimal point number
- `float32`: float contained sign bit, 8 bits exponent and 23 bits decimal point number
- `float64`: float contained sign bit, 11 bits exponent and 52 bits decimal point number
- `complex_` : Same as complex128
- `complex64`: Complex number contained two 32-bit floats
- `complex128`: Complex number contained two 64-bit floats


Also, it is possible to provide the `dtype` with the first letter of each in `numpy`. Refer to below list:

- `i`: integer
- `b`: boolean
- `u`: unsigned integer
- `f`: float
- `c`: complex float
- `m`: timedelta
- `M`: datetime
- `O`: object
- `S`: string
- `U`: unicode string


In order to find the Data type of created array, `dtype` attribute can be used.

```
import numpy as np

arr1 = np.array([1,2,3,4])
arr2 = np.array(["John", "Sarah", "Joe", "Susan"])
arr3 = np.array([1.4, 1+1.3j, 15j])

print("Data Type of arr1: ", arr1.dtype)
print("Data Type of arr2: ", arr2.dtype)
print("Data Type of arr3: ", arr3.dtype)



(output):
Data Type of arr1:  int32
Data Type of arr2:  <U5
Data Type of arr3:  complex128
```


#### Creating array with non-default data types

There is `dtype` flag in `array` function which specifies the data type during the array creation.

```
import numpy as np

arr1 = np.array([1,2,3,4], dtype='float64')
arr2 = np.array([10.1,11.23], dtype='int16')

print("arr1 = ", arr1)
print("Data Type of arr1: ", arr1.dtype)
print("arr2 = ", arr2)
print("Data Type of arr2: ", arr2.dtype)



(output):
arr1 =  [1. 2. 3. 4.]
Data Type of arr1:  float64
arr2 =  [10 11]
Data Type of arr2:  int16
```

#### Converting date type of created array

There is a `astype(dtype)` in which we can convert an existing array.

```
import numpy as np

arr1 = np.array([1,2,3,4])
print("arr1 = ", arr1)
print("Date Type of arr1: ", arr1.dtype)

new_arr1 = arr1.astype('float16')
print("new_arr1 = ", new_arr1)
print("Date Type of new_arr1: ", new_arr1.dtype)



(output):
arr1 =  [1 2 3 4]
Date Type of arr1:  int32
new_arr1 =  [1. 2. 3. 4.]
Date Type of new_arr1:  float16
```
