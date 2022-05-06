---
id: 12_tuples
title: Tuples
sidebar_label: Tuples
slug: /python_Basics/12_tuples
---

---

Tuple is similar to list with two main differences:
- it is enclosed which in parenthesis
- Tuple is immutable

```
>>> tuple_1 = ('John', 'Sarah', 'Marry')
>>> tuple_1
('John', 'Sarah', 'Marry')
>>> tuple_2 = (12, 3, 15, 5)
>>> tuple_2
(12, 3, 15, 5)
>>> tuple_3 = ('a', 'b', 17, 'h', 4.7, 'tt')
>>> tuple_3
('a', 'b', 17, 'h', 4.7, 'tt')
>>> type(tuple_1)
<class 'tuple'>
```

In order to access to each element of a tuple, slicing operator ([]) can be used.

```
>>> tuple_1 = ('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h')
>>> tuple_1[3]
'd'
>>> tuple_1[-2]
'g'
>>> tuple_1[3:7]
('d', 'e', 'f', 'g')
>>> tuple_1[1:7:2] # tuple_1[start:stop:step]
('b', 'd', 'f')
```

* Note That as tuple is an immutable data type, its items cannot updated or deleted.

### Some Basic Tuple Operators

- Length of List: `len(<tuple>)`
- Concatenation: `<tuple1> + <tuple2>`
- Repetition: `<tuple> * num`
- Membership: `in` or `not in`
- Iteration with loop

```
>>> tuple_1 = ('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h')
>>> tuple_2 = ('i', 'j', 'k')
>>> len(tuple_1)
8
>>> len(tuple_2)
3
>>> tuple_1 + tuple_2
('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k')
>>> tuple_2 * 3
('i', 'j', 'k', 'i', 'j', 'k', 'i', 'j', 'k')
>>> 'f' in tuple_1
True
>>> 'a' not in tuple_2
True
>>> for item in tuple_1:
	print(item)


a
b
c
d
e
f
g
h
```


### Built-in List Functions and Methods

| Function | Description |
|:-:|:-:|
| len(tuple) |	Length of a list |
| max(tuple) |	Returning maximum item of a list |
| min(tuple) |	Returning minimum item of a list |
| tuple(seq) |	Converting a list to tuple |

```
>>> tuple_1 =(2, 5, 4, 3, 1, 5, 10)
>>> len(tuple_1)
7
>>> max(tuple_1)
10
>>> min(tuple_1)
1
>>> tuple([2,5,3,6,7,3])
(2, 5, 3, 6, 7, 3)
```

| Method | Description |
|:-:|:-:|
| list.count(obj) |	Counting the number of occurrence of an item in a tuple |
| list.index(obj) |	Returning the lower index of specified item |

```
>>> tuple_1 = ('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h')
>>> tuple_1.count('c')
1
>>> tuple_1.index('g')
6
```
