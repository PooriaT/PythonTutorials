---
id: 06_broadcasting
title: Broadcasting
sidebar_label: Broadcasting
slug: /06_broadcasting
---

---

Broadcasting in Numpy is the ability to do the arithmetic operations on the arrays with different shape.

In case of two arrays have the same dimension, the operation will be element-by-element.
```
import numpy as np

a = np.array([3, 4, 5, 6])
b = np.array([1, 2, 3, 4])

print("result: ", a*b)



(output):
result:  [ 3  8 15 24]
```

In contrast, if the dimensions are different, the smaller array will be broadcasted to the size of the larger one. The below rules is essential in broadcasting:
- Array with smaller dimension than the other is prepended with '1' in its shape.
- The output shape is the maximum of the input sizes in that dimension.

```
import numpy as np

a = np.array([[1,2,3,4], [5,6,7,8],[9,10,11,12],[13,14,15,16]])
b = np.array([2,4,6,8])

print("result: ", a*b)



(output):
result:  [[  2   8  18  32]
 [ 10  24  42  64]
 [ 18  40  66  96]
 [ 26  56  90 128]]
```
