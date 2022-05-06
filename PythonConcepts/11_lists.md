---
id: 11_lists
title: Lists
sidebar_label: Lists
slug: /python_Basics/11_lists
---

---

List is a kind of variable which includes of a list of comma-separated values between square brackets. No matter the values are string or numeric.

Characteristics of List:
- Ordered
- Changeable
- Allow Duplications

```
>>> list_1 = ['John', 'Sarah', 'Marry']
>>> list_2 = [12,3,15,5]
>>> list_2
[12, 3, 15, 5]
>>> list_3 = ['a', 12, 't', 45.5, 'tea']
>>> list_3
['a', 12, 't', 45.5, 'tea']
>>> type(list_1)
<class 'list'>
```

In order to access to each element of a list, slicing operator ([]) can be used.

```
>>> list_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> list_1[3]
'd'
>>> list_1[-2]
'g'
>>> list_1[2:6]
['c', 'd', 'e', 'f']
>>> list_1[:6:2] # list_1[start:stop:step]
['a', 'c', 'e']
```

By referring to index of a list, its items can be updated.

```
>>> list_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> list_1[0] = 10
>>> list_1
[10, 'b', 'c', 'd', 'e', 'f', 'g', 'h']
```

One of deleting an item in a list is to use `del` syntax.

```
>>> list_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> del(list_1[0])
>>> list_1
['b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> del(list_1[:4])
>>> list_1
['f', 'g', 'h']
```

We cannot copy a list simply by using assignment operator. In order to do it, `copy` method is used.

```
>>> list_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> list_2 = list_1.copy()
>>> list_2
['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
```

### Some Basic List Operators

- Length of List: `len(<list>)`
- Concatenation: `<list1> + <list2>`
- Repetition: `<list> * num`
- Membership: `in` or `not in`
- Iteration with loop

```
>>> list_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> list_2 = ['i', 'j', 'k']
>>> len(list_1)
8
>>> len(list_2)
3
>>> list_1 + list_2
['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k']
>>> list_2 * 3
['i', 'j', 'k', 'i', 'j', 'k', 'i', 'j', 'k']
>>> 'f' in list_1
True
>>> 'a' not in list_2
True
>>> for item in list_1:
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

### Built-in List Methods and Functions

| Function | Description |
|:-:|:-:|
| len(list) |	Length of a list |
| max(list) |	Returning maximum item of a list |
| min(list) |	Returning minimum item of a list |
| list(seq) |	Converting a tuple to list |

```
>>> list_1 = [ 2, 5, 4, 3, 1, 5, 10]
>>> len(list_1)
7
>>> max(list_1)
10
>>> min(list_1)
1
>>> list((1,2,3,5,1,3))
[1, 2, 3, 5, 1, 3]
```

| Method | Description |
|:-:|:-:|
| list.append(obj) |	Adding a new item to the list |
| list.count(obj) |	Counting the number of occurrence of an item in a list |
| list.extend(list) |	Appending a sequence to the list |
| list.index(obj) |	Returning the lower index of specified item |
| list.insert(index, obj) | Inserting object to specified position of a list |
| list.pop(index) |	Removing a specified object and returning the rest of the list |
| list.remove(obj) | Removing a specified object form a list |
| list.reverse() |	Reversing a list |
| list.sort([function]) | Sorting a list |

```
>>> list_1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
>>> list_2 = ['i', 'j', 'k']
>>> list_1.append('a')
>>> list_1
['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'a']
>>> list_1.count('a')
2
>>> list_1.extend(list_2)
>>> list_1
['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'a', 'i', 'j', 'k']
>>> list_1.index('a')
0
>>> list_1.index('e')
4
>>> list_1.insert(3,'tt')
>>> list_1
['a', 'b', 'c', 'tt', 'd', 'e', 'f', 'g', 'h', 'a', 'i', 'j', 'k']
>>> list_1.pop(4)
'd'
>>> list_1
['a', 'b', 'c', 'tt', 'e', 'f', 'g', 'h', 'a', 'i', 'j', 'k']
>>> list_1.remove('a')
>>> list_1
['b', 'c', 'tt', 'e', 'f', 'g', 'h', 'a', 'i', 'j', 'k']
>>> list_1.reverse()
>>> list_1.sort()
>>> list_1
['a', 'b', 'c', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'tt']
```

### Set

Set is a kind of list in which its items cannot be duplicated and it is even unordered and unchangeable. Despite the list, the sequence of values are enclosed between curly braces ({}).

In order to convert a list to set, `set` function can be used.

```
>>> set_1 = { 1, 4, 3, 2, 5}
>>> set_1
{1, 2, 3, 4, 5}
>>> list_1 = [1, 4, 3, 2, 4, 5, 5, 5, 1, 3]
>>> set(list_1)
{1, 2, 3, 4, 5}
```

### List Comprehension

It is possible to create new list out of the existent list in a shorter form by using the list comprehension concept.

```
>>> num_list = list(range(20))
>>> num_list
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
>>> even_list = [i for i in num_list if i%2 == 0]
>>> even_list
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
