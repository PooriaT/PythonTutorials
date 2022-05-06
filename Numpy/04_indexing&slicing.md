---
id: 04_indexing&slicing
title: Indexing and Slicing
sidebar_label: Indexing and Slicing
slug: /04_indexing&slicing
---

---

In order to access and modify an item or items of an array, indexing an slicing can be applied such as Python built-in container objects.

### Indexing

Same as Python lists, tuples and sets, we can access to each item of an array with its index. The syntax is the same as Python built-in container objects for one dimensional array. (An array index starts from zero.)

```
import numpy as np

arr = np.array([1,2,3,4])
print(arr[0])
print(arr[2])
print(arr[-3])



(output):
1
3
2
```

For the arrays with more than one dimensions, we can refer an item by specifying its position in each dimension in only one bracket, for instance, if we have 4-dimension array, we can refer to each element in this way: `arr[p1, p2, p3, p4]`. Note that we can use the same way of Python lists indexing as well (`arr[p1][p2][p3][p4]`).

```
import numpy as np

arr = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])
print("Array dimension: ", arr.ndim)
print("Array Shape: ", arr.shape)
print(arr[1][1][0])
print(arr[1,1,0])



(output):
Array dimension:  3
Array Shape:  (2, 2, 2)
7
7
```


### Advanced Indexing

In numpy, we can select several items of an array with advanced indexing. To do so, there are two ways: *Integer* and *Logical* indexing

- Integer Indexing: In this type of indexing, the elements are selected based on the list of indices.

```
import numpy as np

arr = np.array([[1,2,3],[4,5,6],[7,8,9]])
print("Array dimension: ", arr.ndim)
print("Array Shape: ", arr.shape)
print("Items with index of (1,0) and (2,2)"arr[[1,2],[0,2]]) ## This will choose the items with indices of (1,0) and (2,2)



(output):
Array dimension:  2
Array Shape:  (3, 3)
[4 9]
```

- Logical (Boolean) Indexing: In this type of indexing, the elements are selected based on the logical operations.

```
import numpy as np

arr = np.array([[1,2,3],[4,5,6],[7,8,9]])
print("Array dimension: ", arr.ndim)
print("Array Shape: ", arr.shape)
print("Items which are greater and equal 5: ", arr[arr >= 5])



(output):
Array dimension:  2
Array Shape:  (3, 3)
Items which are greater and equal 5:  [5 6 7 8 9]
```


### Slicing

Array slicing is same as Python built-in container object. To do so, we can use `[start:stop]` or `[start:stop:step]` with the array name.
- If we don't pass the step, it is considered as 1.
- If we don't pass the start, it is considered as 0.
- if we don't pass the stop, it s considered as the last index of the array.
- To choose are items between start and stop, we can use ellipsis (`arr[...]`)
- Slicing in n-dimension arrays is same as 1-dimenstion one by considering the slicing range for each dimension.

```
import numpy as np

# 1D array
arr1 = np.array([1,2,3,5,6,7,8,9])
print("Array dimension: ", arr1.ndim)
print("Array Shape: ", arr1.shape)
print("Examples of slicing a 1D array ...")
print(arr1[2:])
print(arr1[:6])
print(arr1[3:7:2])
print(arr1[...])

# 2D array
arr2 = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print("Array dimension: ", arr2.ndim)
print("Array Shape: ", arr2.shape)
print("Examples of slicing a 2D array ...")
print(arr2[1, 2:])
print(arr2[:2, 0:2])
print(arr2[1::2, :1])
print(arr2[..., 1])
print(arr2[0, ...])



(output):
Array dimension:  1
Array Shape:  (8,)
Examples of slicing a 1D array ...
[3 5 6 7 8 9]
[1 2 3 5 6 7]
[5 7]
[1 2 3 5 6 7 8 9]
Array dimension:  2
Array Shape:  (3, 4)
Examples of slicing a 2D array ...
[7 8]
[[1 2]
 [5 6]]
[[5]]
[ 2  6 10]
[1 2 3 4]
```
