---
id: 16_ufunctions
title: Universal Functions
sidebar_label: Universal Functions
slug: /16_ufunctions
---

---

### Introduction to Universal Functions

`ufuncs` (Universal Functions) are Numpy functions that operate on `ndarray` objects. They are used for vectorization which faster than iterating over elements. In addition, they provide some features for computation such as broadcasting, reduction, accumulation.

- **Vectorization**:  Converting iterative statements into vector based operation which is faster and optimized for such operations.

For example, if we want to add the contents of two lists element by element, we can use `numpy`arrays and use `add(x+y)` function which is faster than iterating over the lists.  

### Creating Function

In Numpy, it is possible to create our own `ufuncs`. To do so, `frompyfunc()` is used.

- `numpy.frompyfunc(func, nin, nout, *[, identity])`: takes an arbitrary Python function and returnsa Numpy ufunc.
  - `func`: Python function object. An arbitrary Python function.
  - `nin`: int. The number of input arguments.
  - `nout`: int. The number of objects returned by `func`.
  - `identity`: object (optional). The value to use for the `~numpy.ufunc.identity` attribute of the resulting object. If specified, this is equivalent to setting the underlying C `identity` field to `PyUFunc_IdentityValue`. If omitted, the identity is set to `PyUFunc_None`.

```
import numpy as np

def mod_func(x,y):
    return x % y

myMod = np.frompyfunc(mod_func, 2, 1)

print("Type of function: ", type(myMod))
print("\nOutput of function:\n ", myMod([10,9,8,7], [2,3,3,2]))



(output):
Type of function:  <class 'numpy.ufunc'>

Output of function:
  [0 0 2 1]
```
