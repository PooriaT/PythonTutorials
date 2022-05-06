---
id: 09_numbers
title: Numbers
sidebar_label: Numbers
slug: /python_Basics/09_numbers
---

---

Number data types store numeric values:

```
num_1 = 10
nume_2 = 10.4
```

With `del` syntax, it is possible to delete the reference to number object.

```
>>> num_1 = 10
>>> num_1
10
>>> del num_1
>>> num_1
Traceback (most recent call last):
  File "<pyshell#134>", line 1, in <module>
    num_1
NameError: name 'num_1' is not defined
```
### Numerical Types

There are several numerical types in Python:

- Integer `int(x)`: `num_1 = 123`
- Float point values `float(X)`: `num_2 = 17.85`
- Complex `complex(x,y)` number which are includes real and imaginary parts: `num_3 = 10.1 + 12j`

#### Converting different types to each other

```
>>> num_1 = 10 # integer
>>> num_2 = 123.65 # float
>>> num_3 = 14.2 + 4j # complex
>>> float(num_1)
10.0
>>> complex(num_1)
(10+0j)
>>> complex(num_1, num_2)
(10+123.65j)
>>> int(num_2)
123
```

### Integer Forms

In addition, in integer type, it is possible to consider different forms:

- Decimal `int(x, base=10)`
- Binary `bin(x)`
- Octal `oct(x)`
- Hexa-decimal `hex(x)`

```
>>> num = 33
>>> bin(num)
'0b100001'
>>> oct(num)
'0o41'
>>> hex(num)
'0x21'
```

In order to convert binary, octal and hexa-decimal number, `int` method can be used. There are two ways for this conversion.
1. `int(num, base=[2/8/16])`, note that in this method num should be string
2. `int(num)``
  - Converting binary to decimal, the num should begin with `0b`
  - Converting octal to decimal, the num should begin with `0o`
  - Converting hexa-decimal to decimal, the num should begin with `0x`

```
>>> bin_num = 0b1110011
>>> oct_num = 0o7631
>>> hex_num = 0x1a3b
>>> int(bin_num)
115
>>> int(oct_num)
3993
>>> int(hex_num)
6715
>>> int('1110011',2)
115
>>> int('7631',8)
3993
>>> int('1a3b',16)
6715
```

### Mathematical Functions

```
>>> import math # Built-in mathematical library
>>> abs(-19) # Absolute value of numerical value
19
>>> math.floor(10.3)
10
>>> math.ceil(10.3) # The ceiling of numerical value
11
>>> math.log(3) # The natural logarithm of numerical value
1.0986122886681098
>>> math.log10(3) # The base-10 logarithm of numerical value
0.47712125471966244
>>> max([1,25,3,1,33,2]) # The largest amount of series
33
>>> min([1,25,3,1,33,2]) # The smallest amount of series
1
>>> pow(2,4) # pow(x,y) --> x**y
16
>>> round(23.2) # The rounded number
23
>>> math.sqrt(16) # The Square root of numerical value
4.0
>>> math.sin(30) # The sine of numerical value (radians)
-0.9880316240928618
>>> math.asin(0.4) # The arc sine of numerical value
0.41151684606748806
>>> math.degrees(3) # Converting angle from radians to degrees
171.88733853924697
>>> math.radians(180) # # Converting value from degrees to radians
3.141592653589793

################################
#### Mathematical constants ####
>>> math.pi
3.141592653589793
>>> math.e
2.718281828459045
```
