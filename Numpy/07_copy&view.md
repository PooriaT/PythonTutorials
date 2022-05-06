---
id: 07_copy&view
title: Copy and View
sidebar_label: Copy and View
slug: /07_copy&view
---

---

The main difference between *copy* and *view* of an array is that in *copy*, we have a new array (physically stored in new memory location) but in *view*, there is just a view of the original array. As a result, any changes on the original array will not affect the copied one.


#### Assignment (No Copy)
In this case an assigned array has the same `id` with the original one. Every changes on the original array will affect the assigned one.

```
import numpy as np

a = np.array([1,2,3,4])

b = a #Assignemnt

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))

#Changes on one element of a
a[0] = 77

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))



(output):
a=  [1 2 3 4]  and its id is  1494376156016
b=  [1 2 3 4]  and its id is  1494376156016
a=  [77  2  3  4]  and its id is  1494376156016
b=  [77  2  3  4]  and its id is  1494376156016
```

#### View (Shallow Copy)
In this case, the view array will be affected by the changes of original one except changing its shape. (The `id` of each is different)

```
import numpy as np

a = np.array([1,2,3,4])

b = a.view() #View

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))

#Changes on one element of a
a[0] = 77

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))

a = a.reshape((4,1))

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))



(output):
a=  [1 2 3 4]  and its id is  1494420744880
b=  [1 2 3 4]  and its id is  1494420743248
a=  [77  2  3  4]  and its id is  1494420744880
b=  [77  2  3  4]  and its id is  1494420743248
a=  [[77]
 [ 2]
 [ 3]
 [ 4]]  and its id is  1494420742192
b=  [77  2  3  4]  and its id is  1494420743248
```

#### Copy (Deep Copy)
In this case, the copy array even have the separate memory, so any changes on the original array will not affect the copied one.

```
import numpy as np

a = np.array([1,2,3,4])

b = a.copy() #Copy

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))

#Changes on one element of a
a[0] = 77

print("a= ", a, ' and its id is ', id(a))
print("b= ", b, ' and its id is ', id(b))



(output):
a=  [1 2 3 4]  and its id is  1494420743152
b=  [1 2 3 4]  and its id is  1494420745072
a=  [77  2  3  4]  and its id is  1494420743152
b=  [1 2 3 4]  and its id is  1494420745072
```

#### `base` method
In order to check whether an array owns the data, `base` method can be applied. if it returns `None`, it means that it is a deep copy. Otherwise, it will refers to its origin.

```
import numpy as np

a = np.array([1,2,3,4])

b = a.copy() #Copy
c = a.view() #view

print(b.base)
print(c.base)



(output):
None
[1 2 3 4]
```
