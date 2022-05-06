---
id: 04_variables
title: Variables
sidebar_label: Variables
slug: /python_Basics/04_variables
---

---

Variables are the reserved memory locations in which a value is stored. There are various types of variables such as numeric, string, list and etc.

### Assigning Values to Variables

In order to assign a values to a Python variable, it only needs to use the equal sign (=).

```
>>> number = 100 # An integer number
>>> number
100
>>> float_number = 100.7 # A float number
>>> float_number
100.7
>>> name = "John" # A string
>>> name
'John'
```

It is worth noting that in python, we can use multiple assignment:

```
>>> x = y = z = 10
>>> x,y,z
(10, 10, 10)
```

### Standard Data Types

In python, five different Standard data types can be considered:

- string
- number
- list
- Tuple
- Dictionary

#### String

A string value consists of a thread of different characters which is placed in the quotations marks (single quotation to double quotation). In order to access each character of string, it is possible to use slice operator ([]). plus sign (+) can be used for string concatenation and with multiple sign (*), repetition occurs.

```
>>> string_var = "This is a string"
>>> string_var
'This is a string'
>>> string_var[:]
'This is a string'
>>> string_var[1:3]
'hi'
>>> string_var[5]
'i'
>>> string_var * 2
'This is a stringThis is a string'
>>> string_var + ". amendment!!!"
'This is a string. amendment!!!'
```

#### Number

There are various types of number as a value:

- Integer
- Float
- Complex

```
>>> int_num = 10
>>> int_num
10
>>> float_num = 10.94
>>> float_num
10.94
```
#### List

List is a kind of variable which includes of a list of comma-separated values between square brackets. No matter the values are string or numeric. with slicing operator ([]), each element can be accessible. plus sign (+) can be used for string concatenation and with multiple sign (*), repetition occurs.

```
>>> list_1 = ["John", 25, "Doe", 180, 82]
>>> list_2 = ["abc street", "QA123", 5]
>>> list_1
['John', 25, 'Doe', 180, 82]
>>> list_2
['abc street', 'QA123', 5]
>>> list_1[0]
'John'
>>> list_1[0:2]
['John', 25]
>>> list_1 + list_2
['John', 25, 'Doe', 180, 82, 'abc street', 'QA123', 5]
>>> list_1 * 2
['John', 25, 'Doe', 180, 82, 'John', 25, 'Doe', 180, 82]
```

- `set` is a kind of list in which its items cannot be duplicated and it is even unordered.

```
>>> list_1
[17, 18, 14, 10, 10, 14, 15, 14, 13, 15]
>>> set(list_1)
{10, 13, 14, 15, 17, 18}
```

#### Tuple

Tuple is similar to list with two main differences:
- it is enclosed which in parenthesis
- Tuple is immutable

```
>>> tuple_1 = ("John", 25, "Doe", 180, 82)
>>> tuple_1
('John', 25, 'Doe', 180, 82)
```

#### Dictionary

Dictionary is a kind of Python data type which stores data values in key:value pairs. (keys cannot be duplicated). Dictionary is enclosed in curly braces ({}).

```
dict_1 = {'firstname': "John", 'age': 25, 'lastname': "Doe", 'height': 180, 'weight': 82}
>>> dict_1
{'firstname': 'John', 'age': 25, 'lastname': 'Doe', 'height': 180, 'weight': 82}
>>> dict_1['firstname']
'John'
>>> dict_1.keys()
dict_keys(['firstname', 'age', 'lastname', 'height', 'weight'])
>>> dict_1.values()
dict_values(['John', 25, 'Doe', 180, 82])
>>> dict_1.items()
dict_items([('firstname', 'John'), ('age', 25), ('lastname', 'Doe'), ('height', 180), ('weight', 82)])
```

### Functions for data type conversions

- Convert x to the integer number: `int(x)`
- Convert x to the float-point number: `float(x)`
- convert x to string: `str(x)`
- Convert a list x to set: `set(x)`
- Convert a list x to tuple: `tuple(x)`
- Convert x to a list: `list(x)`
- Convert a list of (key,value) pairs to dictionary: `dict(x)`
