---
id: 10_strings
title: Strings
sidebar_label: Strings
slug: /python_Basics/10_strings
---

---

A string value consists of a thread of different characters which is placed in the quotations marks (single quotation to double quotation).

```
str_1 = 'Hello World!'
str_2 = "This is the test..."
```

To access each part of the string, it is possible to use slicing operator ([]).

```
>>> str_1 = "Hello World!"
>>> str_1[0]
'H'
>>> str_1[3]
'l'
>>> str_1[:5]
'Hello'
>>> str_1[:8:2] # str_1[start:stop:step]
'HloW'
```

It is possible to concatenate two string with plus sign (+).

```
>>> str_1 = "My name is John"
>>> str_2 = "Joe"
>>> str_1[:11] + str_2
'My name is Joe'
```

#### Escape Characters

With escape character, it is possible to use special characters inside a string. An escape character is a backslash `\` followed by the desired character.

- `\'`: Single quotation
- `\"`: Double quotation
- `\\`: Backslash
- `\r`: Carriage return
- `\n`: New Line
- `\t`: Tab
- `\b`: Backspace
- `\ooo`: Octal Value
- `\xhh`: Hex Value

#### Triple Quotes

If we want to insert a string in multiple lines, triple quotes can be used.

```
>>> str_1 = """Hello World,
This is a test to
show how to insert a string in multiple lines."""
>>> str_1
'Hello World,\nThis is a test to\nshow how to insert a string in multiple lines.'
```

### String Operators

| Operators | Description |
|:-:|:-:|
| + |	Concatenation |
| *	| Repetition |
| [] 	| Slicing |
| [start:stop:step] | Range Slicing |
| in | Membership (exist) |
| not in | Membership (not exist) |
| % |	Format |

```
>>> str_1 = "Hello"
>>> str_2 = "World"
>>> str_1 + str_2
'HelloWorld'
>>> str_1*3
'HelloHelloHello'
>>> str_1[4]
'o'
>>> str_1[-2]
'l'
>>> str_1[1:4]
'ell'
>>> 'f' in str_1
False
>>> 'a' not in str_1
True
```

### String Formatting

With `%` operator, we can do formatting on a given string.

| Format Symbol | Description |
|:-:|:-:|
| %c | Character |
| %i | Signed decimal integer |
| %d 	| Signed decimal integer |
| %u | Unsigned decimal integer |
| %x | Lowercase Hexadecimal integer |
| %X | Uppercase Hexadecimal integer |
| %f | Floating point real number |
| %e | Exponential notation |

```
>>> "Hello %s, I thought you are %d years old" % ('John', 17)
'Hello John, I thought you are 17 years old'
```

### Built-in String Methods and Functions

| Method & Function | Description |
|:-:|:-:|
| capitalize() | Converting the first character of a string to uppercase |
| lower()	| Converts a string into lower case |
| upper() |	Converts a string into upper case |
| casefold() |	Converting the string to the lowercase |
| len(<string value>) | Returning the size of the string value |
| center() | Aligning the string |
| count()	| Counting the number of specified value inside a string |
| startswith() | Returning true in case the string starts with the specified value |
| endswith() | Returning true in case the string ends with the specified value |
| find() | returning the position of specified value in case of being found |
| format() | Formatting specified values in a string |
| index() |	returning the position of specified value in case of being found |
| isalnum()	| Returning True if all characters in the string are alphanumeric |
| isalpha() |	Returning True if all characters in the string are in the alphabet |
| isdecimal()	| Returning True if all characters in the string are decimals |
| isdigit()	| Returning True if all characters in the string are digits |
| islower()	| Returning True if all characters in the string are lowercase |
| isnumeric()	| Returning True if all characters in the string are numeric |
| isspace() |	Returning True if all characters in the string are whitespaces |
| isupper() |	Returning True if all characters in the string are uppercase |
| join() | Joining the elements of an iterable to the end of the string |
| ljust()	| Returning a left justified version of the string |
| rjust()	| Returning a right justified version of the string |
| partition()	| Returning a tuple data type where the string is parted into three parts |
| replace()	| Returning a string where a specified value is replaced with another specified value|
| split()	| Splitting the string at the specified separator and returning in list data type |
| splitlines() | Splitting the string at line breaks and returning in list data type |
| strip()	| Returning a trimmed version of the string |
| swapcase() |	Swapping cases |
| title()	| Converting the first character of all word to uppercase |
| zfill() |	Filling the string with a specified number of 0 values at the beginning |

```
>>> str_1 = "this is a test to show how string methods work!!!"
>>> str_2 = "John"
>>> str_1.capitalize()
'This is a test to show how string methods work!!!'
>>> str_2.lower()
'john'
>>> str_2.upper()
'JOHN'
>>> str_2.casefold()
'john'
>>> len(str_2)
4
>>> str_1.count('s')
6
>>> str_1.index("show")
18
>>> str_1.find("show")
18
>>> str_1.startswith('t')
True
>>> str_2.endswith('a')
False
>>> str_2.islower()
False
>>> str_2.isalnum()
True
>>> str_2.isdigit()
False
>>> str_1.isspace()
False
>>> str_1.split(' ')
['this', 'is', 'a', 'test', 'to', 'show', 'how', 'string', 'methods', 'work!!!']
>>> str_2.swapcase()
'jOHN'
>>> str_2.zfill(5)
'0John'
>>> str_2.zfill(10)
'000000John'
>>> str_1.partition('string')
('this is a test to show how ', 'string', ' methods work!!!')
>>> str_2.center(10)
'   John   '
```
