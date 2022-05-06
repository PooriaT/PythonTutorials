---
id: 12_string_functions
title: String Functions
sidebar_label: String Functions
slug: /12_string_functions
---

---

In `numpy`, there are various functions in which you can work with array of strings same as what we have in built-in Python string functions.

- `numpy.char.add(x1, x2)`: returns element-wise string concatenation for two arrays of string.
  - `x1`: Input array of str or unicode
  - `x2`: Input array of str or unicode


- `numpy.char.multiply(a, i)`: returns `a * i`, that is string multiple concatenation, element-wise.
  - `a`: Input array of str or unicode
  - `i`: Input array of ints


```
import numpy as np

a = np.array(["Hello ", "This is "])
b = np.array(["World!", "for test."])
c = np.array(['Hello', 'world'])

print("Adding array of string: ", np.char.add(a,b))
print("Multiplying array of string: ", np.char.multiply(c,3))



(output):
Adding array of string:  ['Hello World!' 'This is for test.']
Multiplying array of string ['HelloHelloHello' 'worldworldworld']

```

- `numpy.char.isalnum(a)`: returns `True` for each element if all characters in the string are alphanumeric and there is at least one character, false otherwise.
  - `a`: Input array of str or unicode


- `numpy.char.isalpha(a)`: returns `True` for each element if all characters in the string are alphabetic and there is at least one character, false otherwise.
  - `a`: Input array of str or unicode


- `numpy.char.isnumeric(a)`: returns `True` if there are only numeric
characters in the element.
  - `a`: Input array of str or unicode

```
import numpy as np

a = np.array(['3432', 'T55s24A', 'Apple'])

print('Isalnum: ', np.char.isalnum(a))
print('Isalpha: ', np.char.isalpha(a))
print('Isnumeric: ', np.char.isnumeric(a))


(output):
Isalnum:  [ True  True  True]
Isalpha:  [False False  True]
Isnumeric:  [ True False False]
```

- `numpy.char.find(a, sub, start=0, end=None)`: for each element, returns the lowest index in the string where substring `sub` is found, such that `sub` is contained in the range [`start`, `end`].
  - `a`: Input array of str or unicode
  - `sub`: str or unicode
  - `start`: int (optional)
  - `end`: int (optional)


  - `numpy.char.count(a, sub, start=0, end=None)`: returns an array with the number of non-overlapping occurrences of substring `sub` in the range [`start`, `end`].
    - `a`: Input array of str or unicode
    - `sub`: str or unicode
    - `start`: int (optional)
    - `end`: int (optional)

```
import numpy as np

a = np.array(['This for a test', 'Hello world', 'Peaceful world, Beautiful world.'])

print('Finding: ', np.char.find(a, 'world'))
print('Counting: ', np.char.count(a, 'world'))


(output):
Finding:  [-1  6  9]
Counting:  [0 1 2]
```

- `numpy.char.center(a, width, fillchar=' ')`: returns a copy of `a` with its elements centered in a string of length `width`.
  - `a`: Input array of str or unicode
  - `width`: int. The length of the resulting strings.
  - `fillchar`: str or unicode (optional).


- `numpy.char.title(a)`: returns element-wise title cased version of string or unicode.
  - `a`: Input array of str or unicode


- `numpy.char.capitalize(a)`: returns a copy of `a` with only the first character of each element capitalized.
  - `a`: Input array of str or unicode


- `numpy.char.upper(a)`: returns an array with the elements converted to uppercase.
  - `a`: Input array of str or unicode


- `numpy.char.lower(a)`: returns an array with the elements converted to lowercase.
  - `a`: Input array of str or unicode


```
import numpy as np

a = np.array(['This for a test', 'hello world', 'peaceful world, beautiful world.'])

print("centering: ", np.char.center(a,20,fillchar='*'))
print("Title: ", np.char.title(a))
print("Capitalize: ", np.char.capitalize(a))
print("Uppercase: ", np.char.upper(a))
print("Lowercase: ", np.char.lower(a))



(output):
centering:  ['**This for a test***' '****hello world*****' 'peaceful world, beau']
Title:  ['This For A Test' 'Hello World' 'Peaceful World, Beautiful World.']
Capitalize:  ['This for a test' 'Hello world' 'Peaceful world, beautiful world.']
Uppercase:  ['THIS FOR A TEST' 'HELLO WORLD' 'PEACEFUL WORLD, BEAUTIFUL WORLD.']
Lowercase:  ['this for a test' 'hello world' 'peaceful world, beautiful world.']
```

- `numpy.char.split(a, sep=None, maxsplit=None)`: for each element in `a`, returns a list of the words in the string, using `sep` as the delimiter string.
  - `a`: Input array of str or unicode
  - `sep` : str or unicode (optional). it it is not specified, any whitespace string is a separator.
  - `maxsplit`: int (optional).


- `numpy.char.splitlines(a, keepends=None)`: for each element in `a`, returns a list of the lines in the element, breaking at line boundaries.
  - `a`: Input array of str or unicode
  - `keepends` : bool (optional). Line breaks are not included in the resulting list unless it is given `True`.


- `numpy.char.strip(a, chars=None)`: for each element in `a`, returns a copy with the leading and trailing characters removed.
  - `a`: Input array of str or unicode
  - `chars` : str or unicode (optional). The `chars` argument is a string specifying the set of characters to be removed.


```
import numpy as np

a = np.array([' This for a test. \nThis is the second line.', '    hello world ', 'peaceful world, beautiful world.'])

print("Spliting: ", np.char.split(a))
print("Spliting of lines: ", np.char.splitlines(a))
print("Striping: ", np.char.strip(a))



(output):
Spliting:  [list(['This', 'for', 'a', 'test.', 'This', 'is', 'the', 'second', 'line.'])
 list(['hello', 'world'])
 list(['peaceful', 'world,', 'beautiful', 'world.'])]
Spliting oflines:  [list([' This for a test. ', 'This is the second line.'])
 list(['    hello world ']) list(['peaceful world, beautiful world.'])]
Striping:  ['This for a test. \nThis is the second line.' 'hello world'
 'peaceful world, beautiful world.']
```

- `numpy.char.join(sep, seq)`: returns a string which is the concatenation of the strings in the sequence `seq`.
  - `sep`: array_like of str or unicode
  - `seq`: array_like of str or unicode


- `numpy.char.replace(a, old, new, count=None)`: for each element in `a`, returns a copy of the string with all occurrences of substring `old` replaced by `new`.
  - `a`: Input array of str or unicode
  - `old`, `new`: str or unicode
  - `count`: int (optional).  


```
import numpy as np

a = np.array(['Hello', 'World'])

print('Joining: ', np.char.join('_',a))
print('Replacing: ', np.char.replace(a, 'World', 'Mars'))


(output):
Joining:  ['H_e_l_l_o' 'W_o_r_l_d']
Replacing:  ['Hello' 'Mars']  
```


- `numpy.char.encode(a, encoding=None, errors=None)`: calls `str.encode` element-wise.
  - `a`: Input array of str or unicode
  - `encoding` : str (optional). The name of an encoding.
  - `errors` : str (optional). Specifies how to handle encoding errors.


- `numpy.char.decode(a, encoding=None, errors=None)`:calls `str.decode` element-wise.
  - `a`: Input array of str or unicode
  - `encoding` : str (optional). The name of an encoding.
  - `errors` : str (optional). Specifies how to handle encoding errors.

```
import numpy as np

a = np.array(['Hello', 'World'])
b = np.array([b'\xc8\x85\x93\x93\x96', b'\xe6\x96\x99\x93\x84'])

print("Encoding: ", np.char.encode(a, encoding='cp037')) # IBM037, IBM039 English
print("Decoding: ", np.char.decode(b, encoding='cp037'))



(output):
​

Encoding:  [b'\xc8\x85\x93\x93\x96' b'\xe6\x96\x99\x93\x84']
Decoding:  ['Hello' 'World']
```
