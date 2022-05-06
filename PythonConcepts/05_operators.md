---
id: 05_operators
title: Operators
sidebar_label: Operators
slug: /python_Basics/05_operators
---

---

Types of Operators in Python:
- Arithmetic operators
- Comparison operators
- Assignment
- Logical operators
- Bitwise operators
- Membership operators
- Identity operators

### Arithmetic Operators  

```
>>> x = 17
>>> y = 15
>>> x + y # Addition
32
>>> x - y # Subtraction
2
>>> x * y # Multiplication
255
>>> x / y # Division
1.1333333333333333
>>> x % y # Modulus
2
>>> x // y # Floor Division
1
>>> x ** 2 # Exponent
289
```

### Comparison Operators

```
>>> x = 17
>>> y = 19
>>> x == y # Equal
False
>>> x != y # Not Equal
True
>>> x > y # Greater than
False
>>> x < y # Less than
True
>>> x >= y # Greeter than or equal
False
>>> x <= y # Less than or equal
True
```

### Assignment

```
>>> x = 20 # Assign operator
>>> x += 10 # Addition with assignment
>>> x
30
>>> x -= 12 # Subtraction with assignment
>>> x
18
>>> x *= 2 # Multiplication with assignment
>>> x
36
>>> x /= 3 # Division with assignment
>>> x
12.0
>>> x %= 5 # Modulus with assignment
>>> x
2.0
>>> x **= 4 # Exponent with modulus
>>> x
16.0
>>> x //= 3 # Floor Division with assignment
>>> x
5.0
```

### Logical Operators

```
>>> x = True
>>> y = False
>>> x and y # Logical AND
False
>>> x or y # Logical OR
True
>>> not x # Logical NOT
False
```

### Bitwise Operators

```
>>> x = 55 # 00110111
>>> y = 74 # 01001010
>>> x & y # Binary AND
2 # 00000010
>>> x | y # Binary OR
127 # 01111111
>>> x ^ y # Binary XOR
125 # 01111101
>>> ~x # Binary Ones Complement
-56
>>> x << 3 # Binary Left Shift
440
>>> x >> 2 # Binary Right Shift
13
```

### Membership Operators

This type of operators is used to test the membership of values in a list, tuple, string and etc.

```
>>> x = 10
>>> list_1 = [1,4,3,7,1,10,5,34]
>>> x in list_1
True
>>> x not in list_1
False
```

### Identity Operators

Identity operators are used to compare the memory locations of two variables or objects.

```
>>> x = 10
>>> y = 10
>>> x is y
True
>>> x is not y
False
```

### Python Operator Precedence

1. Parentheses (grouping)
2. Function call
3. Slicing
4. Subscription
5. Attribute reference
6. Exponentiation
7. Bitwise not
8. Positive, negative
9. Multiplication, division, remainder
10. Addition, subtraction
11. Bitwise shifts
12. Bitwise AND
13. Bitwise XOR
14. Bitwise OR
15. Comparisons, membership, identity
16. Boolean NOT
17. Boolean AND
18. Boolean OR
19. Lambda expression
