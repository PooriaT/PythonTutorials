---
id: 13_matrix_and_linear_algebra
title: Matrix Library and Linear Algebra
sidebar_label: Matrix Library and Linear Algebra
slug: /13_matrix_and_linear_algebra
---

---

### Matrix Library
There is a `matlib` in Numpy which supports to work with matrices.

- `numpy.matlib.empty(shape, dtype=None, order='C')`: returns a new matrix of given shape and type, without initializing entries.
  - `shape`: int or tuple of int.
  - `dtype`: data-type (optional).
  - `order`: {'C', 'F'} (optional). Whether to store multi-dimensional data in row-major (C-style) or column-major (Fortran-style) order in memory.


- `numpy.matlib.zeros(shape, dtype=None, order='C')`: returns a matrix of given shape and type, filled with zeros.
  - `shape`: int or tuple of int.
  - `dtype`: data-type (optional).
  - `order`: {'C', 'F'} (optional). Whether to store multi-dimensional data in row-major (C-style) or column-major (Fortran-style) order in memory.


- `numpy.matlib.ones(shape, dtype=None, order='C')`: returns a matrix of given shape and type, filled with ones.
  - `shape`: int or tuple of int.
  - `dtype`: data-type (optional).
  - `order`: {'C', 'F'} (optional). Whether to store multi-dimensional data in row-major (C-style) or column-major (Fortran-style) order in memory.


- `numpy.matlib.eye(n, M=None, k=0, dtype=<class 'float'>, order='C')`: returns a matrix with ones on the diagonal and zeros elsewhere.
  - `n`: int. Number of rows in the output.
  - `M`: int (optional). Number of columns in the output, defaults to `n`.
  - `k`: int (optional). Index of the diagonal: 0 refers to the main diagonal, a positive value refers to an upper diagonal, and a negative value to a lower diagonal.
  - `dtype`: data-type (optional).
  - `order`: {'C', 'F'} (optional). Whether to store multi-dimensional data in row-major (C-style) or column-major (Fortran-style) order in memory.


- `numpy.matlib.identity(n, dtype=None)`: returns the square identity matrix of given size.
  - `n`: int. Size of the returned identity matrix.
  - `dtype`: data-type (optional).


- `numpy.matlib.rand(*args)`: returns a matrix of random values with given shape.


Examples:
```
import numpy as np
import numpy.matlib

print("Matrix of Empty: ", numpy.matlib.empty((3,3)))
print("Matrix of Zeros: ", numpy.matlib.zeros((2,3)))
print("Matrix of Ones: ", numpy.matlib.ones((3,4)))
print("Matrix of Eye: ", numpy.matlib.eye(3,M=6,k=3))
print("Matrix of Identity: ", numpy.matlib.identity(5))
print("Matrix of Rand: ", numpy.matlib.rand((2,4)))


(output):
Matrix of Empty:  [[2.35541533e-312 2.29175545e-312 7.00258612e-313]
 [0.00000000e+000 2.16443571e-312 2.41907520e-312]
 [2.46151512e-312 2.44029516e-312 9.76118064e-313]]
Matrix of Zeros:  [[0. 0. 0.]
 [0. 0. 0.]]
Matrix of Ones:  [[1. 1. 1. 1.]
 [1. 1. 1. 1.]
 [1. 1. 1. 1.]]
Matrix of Eye:  [[0. 0. 0. 1. 0. 0.]
 [0. 0. 0. 0. 1. 0.]
 [0. 0. 0. 0. 0. 1.]]
Matrix of Identity:  [[1. 0. 0. 0. 0.]
 [0. 1. 0. 0. 0.]
 [0. 0. 1. 0. 0.]
 [0. 0. 0. 1. 0.]
 [0. 0. 0. 0. 1.]]
Matrix of Rand:  [[0.70724446 0.63362566 0.56588755 0.76886438]
 [0.88988322 0.45705195 0.40543023 0.86150816]]
```


### Linear Algebra
There is a `linalg` in Numpy, in which provide various functions to do the linear algebra.

- `numpy.dot(a, b, out=None)`: returns dot product of two arrays.
  - `a`: array_like. First argument.
  - `b`: array_like. Second argument.
  - `out`: ndarray (optional)


- `numpy.vdot(a, b)`: returns the dot product of two vectors.
  - `a`: array_like. First argument.
  - `b`: array_like. Second argument.


- `numpy.inner(a, b)`: returns inner product of two arrays.
  - `a`: array_like. First argument.
  - `b`: array_like. Second argument.


- `numpy.matmul(x1, x2)`: returns matrix product of two arrays.
  - `x1`,`x2`: Input arrays, scalars not allowed.

```
import numpy as np

a = np.array([[2, 4], [5, 8]])
b = np.array([[3, 2], [1, 6]])

print("Dot product of Matrices: ", np.dot(a,b))
print("Dot product of Vectors: ", np.vdot(a,b))
print("Inner product of Matrices: ", np.inner(a,b))
print("Matrix produc of two arrays: ", np.matmul(a,b))



(output):
Dot product of Matrices:  [[10 28]
 [23 58]]
Dot product of Vectors:  67
Inner product of Matrices:  [[14 26]
 [31 53]]
Matrix produc of two arrays:  [[10 28]
 [23 58]]
```

- `numpy.linalg.det(a)`: returns the determinant of an array.
  - `a`: (..., M, M) array_like. Input array to compute determinants for.


- `numpy.linalg.inv(a)`: returns the inverse of a matrix.
  - `a`: (..., M, M) array_like. Matrix to be inverted.


- `numpy.linalg.solve(a, b)`: returns a solution of a linear matrix equation, or system of linear scalar equations.
  - `a`: (..., M, M) array_like. Coefficient matrix.
  - `b`: {(..., M,), (..., M, K)}, array_like. Ordinate or "dependent variable" values.



```
import numpy as np

a = np.array([[2, 4], [5, 8]])
b = np.array([3, 2])

print("Determinant of a: ", numpy.linalg.det(a))
print("Inverse of a: ", numpy.linalg.inv(a))
print("Solution of linear equation: ", numpy.linalg.solve(a,b))



(output):
Determinant of a:  -3.999999999999999
Inverse of a:  [[-2.    1.  ]
 [ 1.25 -0.5 ]]
Solution of linear equation:  [-4.    2.75]
```
