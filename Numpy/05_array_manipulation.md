---
id: 05_array_manipulation
title: Array Manipulation
sidebar_label: Array Manipulation
slug: /05_array_manipulation
---

---

There are various functions and methods available in `numpy` module, in which you can manipulate the arrays form its shape to adding elements.

#### Changing the Array shape
We can change the shape of array with below functions:

- `reshape`: gives a new shape to an array without changing its data
  - `arr.reshape(newshape, order='C')` for any array `arr`
  - `a`: Array to be reshaped
  - `newshape`: int or tuple of ints (for more that one dimensional arrays)
  - `order` : {'A', 'C', 'F'} (optional). A (any), C (row major, default) or F (column major).


- `flat`: Flat iterator object to iterate over arrays
  - `arr.flat` for any array `arr`
Flat iterator object to iterate over arrays.


- `flatten`: returns a copy of the array collapsed into one dimension
  - `arr.flatten(order='C')` for any array `arr`
  - `order` : {'A', 'C', 'F'} (optional). A (any), C (row major, default) or F (column major).


- `resize`: changes shape and size of array in-place
  - `arr.resize(new_shape, refcheck=True)` for any array `arr`
  - `new_shape`: tuple of ints, or `n` ints shape of resized array
  - `refcheck`: bool (optional). If False, reference count will not be checked. Default is True.

Example:
```
import numpy as np

arr = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print("Current Shape: ", arr.shape)

arr = arr.reshape((2,3,2))
print("After Reshaping: ", arr.shape)
print(arr)

print("Flattier: ", arr.flat[5:8])
print("The length of Flatten array: ", len(arr.flat))

print("Flatten array: ", arr.flatten())

arr = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print("Array before resizing: ", arr)
arr.resize((2,3))
print("Array After resizing: ", arr)


(output):
Current Shape:  (3, 4)
After Reshaping:  (2, 3, 2)
[[[ 1  2]
  [ 3  4]
  [ 5  6]]

 [[ 7  8]
  [ 9 10]
  [11 12]]]
Flattier:  [6 7 8]
The length of Flatten array:  12
Flatten array:  [ 1  2  3  4  5  6  7  8  9 10 11 12]
Array before resizing:  [[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
Array After resizing:  [[1 2 3]
 [4 5 6]]
```

#### Changing the Array Dimensions
- `broadcast_to`: broadcasts an array to a new shape.
  - `numpy.broadcast_to(array, shape, subok=False)`
  - `array`: The array to broadcast
  - `shape`: the tuple of shape of the desired array.
  - `subok`: bool (optional). If True, then sub-classes will be passed-through, otherwise the returned array will be forced to be a base class array


- `expand_dims`: expands the shape of an array. Insert a new axis that will appear at the `axis` position in the expanded array shape.
  - `numpy.expand_dims(a, axis)`
  - `a`: Input array
  - `axis`: int or tuple of ints. Position in the expanded axes where the new axis (or axes) is placed.


- `squeeze`: removes axes of length one from an array.
  - `arr.squeeze(axis=None)` for any array `arr`


Example:
```
import numpy as np

arr = np.array([1,2,3,4])

#Broadcast_to
print("Broadcast to: ", np.broadcast_to(arr, (6,4)))


# expand_dims
arr = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
print("########################")
print("Current array shape: ", arr.shape)
print("Expand dimensions over axis = 0:", np.expand_dims(arr, axis=0), "\n and its shape: ", np.expand_dims(arr, axis=0).shape)
print("Expand dimensions over axis = 1: ", np.expand_dims(arr, axis=1), "\n and its shape: ", np.expand_dims(arr, axis=1).shape)

# squeeze
arr = np.array([[[1,2,3,4],[5,6,7,8],[9,10,11,12]]])
print("########################")
print("Current array shape: ", arr.shape)
print("Squeeze of arr: ", arr.squeeze(), "\n and its shape: ", arr.squeeze().shape)



(output):
Broadcast to:  [[1 2 3 4]
 [1 2 3 4]
 [1 2 3 4]
 [1 2 3 4]
 [1 2 3 4]
 [1 2 3 4]]
########################
Current array shape:  (3, 4)
Expand dimensions over axis = 0: [[[ 1  2  3  4]
  [ 5  6  7  8]
  [ 9 10 11 12]]]
 and its shape:  (1, 3, 4)
Expand dimensions over axis = 1:  [[[ 1  2  3  4]]

 [[ 5  6  7  8]]

 [[ 9 10 11 12]]]
 and its shape:  (3, 1, 4)
########################
Current array shape:  (1, 3, 4)
Squeeze of arr:  [[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
 and its shape:  (3, 4)
```

#### Adding and Removing Elements

- `append`: appends values to the end of an array
  - `numpy.append(arr, values, axis=None)`
  - `arr`: Values are appended to a copy of this array
  - `values`: array_like.
  - `axis`: int (optional). The axis along which `values` are appended.


- `insert`: inserts values along the given axis before the given indices.
  - `numpy.insert(arr, obj, values, axis=None)`
  - `arr`: Input array.
  - `obj`: int, slice or sequence of ints. Object that defines the index or indices before which `values` is inserted.
  - `values`: array_like.
  - `axis`: int (optional). The axis along which `values` are appended.


- `delete`: returns a new array with sub-arrays along an axis deleted.
  - `numpy.delete(arr, obj, axis=None)`
  - `arr`: Input array.
  - `obj`: int, slice or sequence of ints. Object that defines the index or indices before which `values` is inserted.
  - `values`: array_like.
  - `axis`: int (optional). The axis along which `values` are appended.


- `unique`: finds the unique elements of an array and returns the sorted unique elements of that array.
  - `numpy.unique(arr, return_index=False, return_inverse=False, return_counts=False, axis=None)`
  - `arr`: Input array.
  `return_index`: bool (optional). If True, returns the indices of `arr`.
  - `return_inverse`: bool (optional). If True, returns the indices of the unique array.
  - `return_counts`: bool (optional). If True, returns the number of times each unique itme appears in `arr`.
  - axis : int or None (optional). The axis to operate on.


Example:
```
import numpy as np

arr = np.array([[1,2,3,4],[5,6,7,8]])

### Appending
print("Appended array: ", np.append(arr, [9,10,11,12]))
print("Appended array, axis=0: ", np.append(arr, [[9,10,11,12]], axis=0))
print("Appended array, axis=1: ", np.append(arr, [[9],[10]], axis=1))

### Inserting
print("\nInserted array: ", np.insert(arr, 5, [9,10]))
print("Inserted array, axis=0: ", np.insert(arr, 1, [9,10,11,12], axis=0))
print("Inserted array, axis=1: ", np.insert(arr, 2, [9,10], axis=1))

### Deleting
print("\nDeleted array: ", np.delete(arr,[1,5]))
print("Deleted array, axis=1: ", np.delete(arr, 1, axis=1))

#### Unique array
arr = np.array([1,2,3,4,3,2,5,6,7,4,3,1,3,2,4,5])
print("\nUnique Array: ", np.unique(arr,return_counts = True))



(output):
Appended array:  [ 1  2  3  4  5  6  7  8  9 10 11 12]
Appended array, axis=0:  [[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
Appended array, axis=1:  [[ 1  2  3  4  9]
 [ 5  6  7  8 10]]

Inserted array:  [ 1  2  3  4  5  9 10  6  7  8]
Inserted array, axis=0:  [[ 1  2  3  4]
 [ 9 10 11 12]
 [ 5  6  7  8]]
Inserted array, axis=1:  [[ 1  2  9  3  4]
 [ 5  6 10  7  8]]

Deleted array:  [1 3 4 5 7 8]
Deleted array, axis=1:  [[1 3 4]
 [5 7 8]]

Unique Array:  (array([1, 2, 3, 4, 5, 6, 7]), array([2, 3, 4, 3, 2, 1, 1], dtype=int64))
```

#### Transpose Operation

- `transpose`: reverses the aces of an array and returns the modified one.
  - `numpy.transpose(a, axes=None)`
  - `a`: Input array
  - `axis`: tuple or list of ints (optional).


- `ndarray.T`: transposes of the array.
  - `arr.T` for any array `arr`


- `rollaxis`: rolls the specified axis backwards, until it lies in a given position
  - `numpy.rollaxis(a, axis, start=0)`
  - `a`: Input array
  - `axis`: int. The axis to be rolled. The positions of the other axes do not change relative to one another.
  - `start`: int (optional). When `start <= axis`, the axis is rolled back until it lies in this position. When `start > axis`, the axis is rolled unit it lies before this position.


- `swapaxes`: returns a view or the array with `axis1` and `axis2` interchanged.
  - `arr.swapaxes(axis1, axis2)` for any array `arr`


Example:
```
import numpy as np

arr = np.array([[1,2,3,4],[5,6,7,8]])

print("Transpose of arr: ", np.transpose(arr))
print("arr.T: ", arr.T)

print("Rollaxis of arr: ", np.rollaxis(arr,axis=1))
print("Swapxes of arr: ", arr.swapaxes(0,1))



(output):
Transpose of arr:  [[1 5]
 [2 6]
 [3 7]
 [4 8]]
arr.T:  [[1 5]
 [2 6]
 [3 7]
 [4 8]]
Rollaxis of arr:  [[1 5]
 [2 6]
 [3 7]
 [4 8]]
Swapxes of arr:  [[1 5]
 [2 6]
 [3 7]
 [4 8]]
```

#### Splitting Arrays

- `split`: splits an array into multuple sub-arrays as views into `arr`
  - `numpy.split(arr, indices_or_sections, axis=0)`
  - `arr`: Array to be splited
  - `indices_or_sections` : int or 1-D array. If `indices_or_sections` is an integer, N, the array will be divided into N equal arrays along `axis`.  If such a split is not possible, an error is raised. But if `indices_or_sections` is a 1-D array of sorted integers, the entries indicate where along `axis` the array is split.  
  - `axis`: int (optional)


- `hsplit`: Splits an array into multiple sub-arrays horizontally (column-wise).
  - `numpy.hsplit(arr, indices_or_sections)`
  - `arr`: Array to be splited
  - `indices_or_sections` : int or 1-D array. If `indices_or_sections` is an integer, N, the array will be divided into N equal arrays along `axis`.  If such a split is not possible, an error is raised. But if `indices_or_sections` is a 1-D array of sorted integers, the entries indicate where along `axis` the array is split.  


- `vsplit`: splits an array into multiple sub-arrays vertically (row-wise).
  - `numpy.vsplit(arr, indices_or_sections)`
  - `arr`: Array to be splited
  - `indices_or_sections` : int or 1-D array. If `indices_or_sections` is an integer, N, the array will be divided into N equal arrays along `axis`.  If such a split is not possible, an error is raised. But if `indices_or_sections` is a 1-D array of sorted integers, the entries indicate where along `axis` the array is split.


- `array_split`: splits an array into multiple sub-arrays. its difference with `split` is that this function allows `indices_or_sections` to be an integer that does **not** equally
divide the axis.
  - `numpy.array_split(arr, indices_or_sections, axis=0)`
  - `arr`: Array to be splited
  - `indices_or_sections` : int or 1-D array. If `indices_or_sections` is an integer, N, the array will be divided into N equal arrays along `axis`.  If such a split is not possible, an error is raised. But if `indices_or_sections` is a 1-D array of sorted integers, the entries indicate where along `axis` the array is split.  
  - `axis`: int (optional)

Example:
```
import numpy as np

arr = np.array([[1,2,3], [4,5,6],[7,8,9],[10,11,12]])

# Split
print("Split: ", np.split(arr,2))
print("Array_split: ", np.array_split(arr,2))

# hsplit
print("hsplit: ", np.hsplit(arr,3))

# vsplit
print("vplist: ", np.vsplit(arr,4))


(output):
Split:  [array([[1, 2, 3],
       [4, 5, 6]]), array([[ 7,  8,  9],
       [10, 11, 12]])]
Array_split:  [array([[1, 2, 3],
       [4, 5, 6]]), array([[ 7,  8,  9],
       [10, 11, 12]])]
hsplit:  [array([[ 1],
       [ 4],
       [ 7],
       [10]]), array([[ 2],
       [ 5],
       [ 8],
       [11]]), array([[ 3],
       [ 6],
       [ 9],
       [12]])]
vplist:  [array([[1, 2, 3]]), array([[4, 5, 6]]), array([[7, 8, 9]]), array([[10, 11, 12]])]
```

#### Joining Arrays

- `concatenate`: joins a sequence of arrays along an existing axis.
  - `numpy.concatenate((a1, a2, ...), axis=0, out=None, dtype=None)`
  - `a1, a2, ...` : sequence of array_like. The arrays must have the same shape, except in the dimension corresponding to `axis` (the first, by default).
  - `axis` : int (optional)
  - `out` : ndarray (optional). If provided, the destination to place the result.
  - `dtype`: str or dtype


- `stack`: joins a squence of arrays aling a new axis.
  - `numpy.stack(arrays, axis=0, out=None)`
  - `arrays` : sequence of array_like. Each array must have the same shape.
  - `axis` : int (optional)
  - `out` : ndarray (optional). If provided, the destination to place the result.

- `hstack`: stacks arrays in sequence horizontally (column wise). This is equivalent to concatenation along the second axis, except for 1-D arrays where it concatenates along the first axis.
  - `numpy.hstack(tup)`
  - `tup`: sequence of ndarrays. The arrays must have the same shape along all but the second axis, except 1-D arrays which can be any length.



- `vstack`: stacks arrays in sequence vertically (row wise). This is equivalent to concatenation along the first axis after 1-D arrays of shape `(N,)` have been reshaped to `(1,N)`.
  - `numpy.vstack(tup)`
  - `tup`: sequence of ndarrays. The arrays must have the same shape along all but the first axis. 1-D arrays must have the same length.


- `dstack`: stacks arrays in sequence depth wise (along third axis). This is equivalent to concatenation along the third axis after 2-D arrays of shape `(M,N)` have been reshaped to `(M,N,1)` and 1-D arrays of shape `(N,)` have been reshaped to `(1,N,1)`.
  - `numpy.dstack(tup)`
  - `tup`: sequence of arrays. The arrays must have the same shape along all but the third axis. 1-D or 2-D arrays must have the same shape.


Example:
```
import numpy as np

arr1 = np.array([1,2,3,4])
arr2 = np.array([5,6,7,8])

print("Concatenate: ", np.concatenate((arr1,arr2)))
print("stack: ", np.stack((arr1,arr2)))
print("hstack: ", np.hstack((arr1,arr2)))
print("vstack: ", np.vstack((arr1,arr2)))
print("dstack: ", np.dstack((arr1,arr2)))



(output):
Concatenate:  [1 2 3 4 5 6 7 8]
stack:  [[1 2 3 4]
 [5 6 7 8]]
hstack:  [1 2 3 4 5 6 7 8]
hstack:  [[1 2 3 4]
 [5 6 7 8]]
dstack:  [[[1 5]
  [2 6]
  [3 7]
  [4 8]]]
```
