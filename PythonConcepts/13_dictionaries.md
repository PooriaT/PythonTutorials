---
id: 13_dictionaries
title: Dictionaries
sidebar_label: Dictionaries
slug: /python_Basics/13_dictionaries
---

---

Dictionary is a kind of Python data type which stores data values in key:value pairs. (keys cannot be duplicated). Dictionary is enclosed in curly braces ({}).

```
dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1
{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}
```

In order to access to each item of dictionary, a slicing operator ([]) is used. Compared to list which an index is employed to access a value, in dictionary, a key parameter is used.

```
dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1['firstname']
'John'
>>> dict_1.keys()
dict_keys(['firstname', 'age', 'lastname', 'height', 'weight'])
>>> dict_1.values()
dict_values(['John', 25, 'Doe', 180, 82])
>>> dict_1.items()
dict_items([('firstname', 'John'), ('age', 25), ('lastname', 'Doe'), ('height', 180), ('weight', 82)])
```

By accessing to specified item, its updating is possible.

```
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1['firstname'] = 'Sarah'
>>> dict_1
{'firstname': 'Sarah', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}
```

There are several ways of deleting an item in dictionary:
- `pop` method: remove the specified key:value pair
- `popitem` method: remove the last key:value pair
- `del` syntax: delete the dictionary completely
- `clear` method: Clear all items of a dictionary

```
>>> # Using pop method
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1.pop('firstname')
'John'
>>> dict_1
{'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}
>>> # Using popitem method
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1.popitem()
('weight', 82)
>>> dict_1
{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180}
# Using del syntax
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> del dict_1
>>> dict_1
Traceback (most recent call last):
  File "<pyshell#450>", line 1, in <module>
    dict_1
NameError: name 'dict_1' is not defined
# Using clear method
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1.clear()
>>> dict_1
{}
```

We cannot copy a list simply by using assignment operator. In order to do it, `copy` method is used.

```
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_2 = dict_1.copy()
>>> dict_2
{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}
```

### Some Basic Dictionary Operators

- Length of dictionary: `len(<dict>)`
- Membership of keys: `in` or `not in`
- Iteration with loop

```
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> len(dict_1)
5
>>> 'firstname' in dict_1
True
>>> 'Doe' in dict_1
False
>>> 'Doe' in dict_1.values()
True
>>> for key,value in dict_1.items():
	print((key,value))


('firstname', 'John')
('age', 25)
('lastname', 'Doe')
('height', 180)
('weight', 82)
```

#### Nested Dictionaries

A value of each item in dictionary can be string, number, list, tuple and even another dictionary.

```
>>> mathClass_dict = { 'student1': { 'name' : 'John' , 'grade': 'A'}, 'student2': { 'name': 'Sarah', 'grade': 'A+'}}
```

### Built-in Dictionary Methods and Functions

| Function | Description |
|:-:|:-:|
| len(dict) | Returning the number of item in a dictionary |
| str(dict) | Converting the dictionary to a string value |

```
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1
{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}
>>> str(dict_1)
"{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}"
>>> len(dict_1)
5
```

| Method | Description |
|:-:|:-:|
| dict.items() | Returning a list of (key, vlaue) pairs |
| dict.keys() | Returning a list of all keys |
| dict.values() | Returning a list of all values |
| dict.clear() | Clearing all items of a dictionary |
| dict.copy(dict) | assigning one dictionary to other |
| dict.fromkeys(seq) | creating a new dictionary with keys from seq  |
| dict.get(key, default=None) | Returning a value for a specified key |
| dict.setdefault(key, default = None) | If the key is not available in the dictionary, it will added with None value unless changing the default value. |
| dict1.update(dict2) | Updating dict1 with key:value pairs of dict2 |

```
>>> dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_2 = {'sex': 'male'}
>>> dict_1.items()
dict_items([('firstname', 'John'), ('age', 25), ('lastname', 'Doe'), ('height', 180), ('weight', 82)])
>>> dict_1.keys()
dict_keys(['firstname', 'age', 'lastname', 'height', 'weight'])
>>> dict_1.values()
dict_values(['John', 25, 'Doe', 180, 82])
>>> dict_1.get('firstname')
'John'
>>> dict_1.get('sex', 'NA')
'NA'
>>> dict_1.update(dict_2)
>>> dict_1
{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82, 'sex': 'male'}
>>> seq = ['name', 'age', 'sex']
>>> new_dict = dict.fromkeys(seq)
>>> new_dict
{'name': None, 'age': None, 'sex': None}
>>> new_dict.setdefault('height')
>>> new_dict
{'name': None, 'age': None, 'sex': None, 'height': None}
```
