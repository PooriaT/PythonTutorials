---
id: 11_binary_functions
title: Binary Functions
sidebar_label: Binary Functions
slug: /11_binary_functions
---

---

Numpy supports various kinds of binary functions. We will introduce some here:

- `numpy.bitwise_and(*args, **kwargs)`: returns the bit-wise *AND* of two arrays element-wise.
- `numpy.bitwise_or(*args, **kwargs)`: returns the bit-wise *OR* of two arrays element-wise.
- `numpy.bitwise_not(*args, **kwargs)`: returns bit-wise inversion, or bit-wise NOT, element-wise.
- `numpy.bitwise_xor(*args, **kwargs)`: returns the bit-wise XOR of two arrays element-wise.
- `numpy.invert(*args, **kwargs)`: returns bit-wise inversion, or bit-wise NOT, element-wise.
- `numpy.right_shift(*args, **kwargs)`: shifts the bits of an integer to the right, by considering the desired position.
- `numpy.left_shift(*args, **kwargs)`: shifts the bits of an integer to the left, by considering the desired position.


- `arr.byteswap(inplace=False)`: swaps the bytes of the array elements. it will toggle between low-endian and big-endian data representation by returning a byteswapped array, optionally swapped in-place.
  - `inplace`: bool (optional). If True, swap bytes in-place.


- `numpy.binary_repr(num, width=None)`: returns the binary representation of the input number as a string.
  - `num`: int, Only an integer decimal number can be used.
  - `width`: int (optional). The length of the returned string if `num` is positive, or the length of the two's complement if `num` is negative.


Examples:
```
import numpy as np

a = np.array([16, 18, 64])
b = np.array([10, 22, 32])

print("Bit-wise AND: ", np.bitwise_and(a,b))
print("Bit-wise OR: ", np.bitwise_or(a,b))
print("Bit-wise NOT: ", np.bitwise_not(a))
print("Bit-wise XOR: ", np.bitwise_xor(a,b))

print("\nright Shift: ", np.right_shift(a,2))
print("Left Shift: ", np.left_shift(a,2))

print("\nByte Swap: ", a.byteswap(inplace=True))

print("\nBinary Representative: ", np.binary_repr(10, width=8))



(output):
Bit-wise AND:  [ 0 18  0]
Bit-wise OR:  [26 22 96]
Bit-wise NOT:  [-17 -19 -65]
Bit-wise XOR:  [26  4 96]

right Shift:  [ 4  4 16]
Left Shift:  [ 64  72 256]

Byte Swap:  [ 268435456  301989888 1073741824]

Binary Representative:  00001010
```
