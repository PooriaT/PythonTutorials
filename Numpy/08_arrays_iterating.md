---
id: 08_arrays_iteration
title: Arrays Iterating
sidebar_label: Arrays Iterating
slug: /08_arrays_iterating
---

---

As we know, iterating means to go through the array or list elements one by one.

```
import numpy as np

a = np.array([1,2,3,4])
print("Iterating over one dimensional Array:")
for i in a:
    print(a)

#########################
b = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print("\nIterating over two dimensional Array:")
print("Iterating over array")
for i in b:
    print(i)
print("Iterating over each elements")
for i in b:
    for j in i:
        print(j)


(output):
Iterating over one dimensional Array:
[1 2 3 4]
[1 2 3 4]
[1 2 3 4]
[1 2 3 4]

Iterating over two dimensional Array:
Iterating over array
[1 2 3 4]
[5 6 7 8]
[ 9 10 11 12]
Iterating over each elements
1
2
3
4
5
6
7
8
9
10
11
12
```

#### `numpy.nditer` Function

In `numpy`, there are two ways of iterating over multi-dimensional arrays:
- with nested `for` loops
- with `numpy.nditer()`: is a helping function for basic to advanced iterations.

```
import numpy as np

a = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])
print("Shape of array 'a': ", a.shape)

print("Iterating with nested for loops")
for i in a:
    for j in i:
        for k in j:
            print(k)

print("Iterating with numpy.nditer()")
for i in np.nditer(a):
    print(i)



(output):
Shape of array 'a':  (2, 2, 2)
Iterating with nested for loops
1
2
3
4
5
6
7
8
Iterating with numpy.nditer()
1
2
3
4
5
6
7
8
```

#### Broadcasting iteration
If two arrays are broadcast able, it is possible to iteration over two of them concurrently with `numpy.nditer()` function.

```
import numpy as np

a = np.array([[1,2,3,4], [5,6,7,8],[9,10,11,12],[13,14,15,16]])
b = np.array([2,4,6,8])

#Iterating:
for i,j in np.nditer([a,b]):
    print("({},{})".format(i,j))



(output):
(1,2)
(2,4)
(3,6)
(4,8)
(5,2)
(6,4)
(7,6)
(8,8)
(9,2)
(10,4)
(11,6)
(12,8)
(13,2)
(14,4)
(15,6)
(16,8)
```

#### `numpy.ndenumerate()` Function
The functionality of `numpy.ndenumerate()` is the same as `numpy.nditer()` with this difference that it specifies the index of each elements in the array as well.

```
import numpy as np

a = np.array([[1,2,3,4], [5,6,7,8],[9,10,11,12],[13,14,15,16]])

for i in np.ndenumerate(a):
    print(i)


(output):
((0, 0), 1)
((0, 1), 2)
((0, 2), 3)
((0, 3), 4)
((1, 0), 5)
((1, 1), 6)
((1, 2), 7)
((1, 3), 8)
((2, 0), 9)
((2, 1), 10)
((2, 2), 11)
((2, 3), 12)
((3, 0), 13)
((3, 1), 14)
((3, 2), 15)
((3, 3), 16)
```
