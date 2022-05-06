---
id: 17_exceptions
title: Exceptions
sidebar_label: Exceptions
slug: /python_Basics/17_exceptions
---

---


In Python, there are two ways of handling errors:
- Assertions
- Exception Handling (Exception is an event which may happen during the program run and disrupt the normal code execution)

#### Standard Exception

- **Exception**: The base class for all built-in exceptions
- **ArithmeticError**: The base class for various arithmetic errors 	
- **OverflowError**: Raised when the result of an arithmetic operation is too large to be represented
- **ZeroDivisionError**: Raised when the second argument of a division or modulo operation is zero
- **StopIteration**: Raised by built-in function `next()` that there are no further items produced by the iterator.
- **AssertionError**: Raised when an assert statement fails
- **AttributeError**: Raised when an attribute reference or assignment fails
- **EOFError**: Raised when there is no input from `input()` and the end of file is reached
- **ImportError**:Raised when an import statement fails
- **KeyboardInterrupt**: Raised when the user hits the interrupt key
- **IndexError**: Raised when a sequence subscript is out of range
- **KeyError**: Raised when the specified key is not found in the dictionary
- **NameError**:Raised when a local or global name is not found.
- **IOError**: Raised when try to open a file which does not exist.
- **SyntaxError**: Raised when the parser encounters an in Python syntax
- **IndentationError**: Raised when incorrect indentation is specified
- **TypeError**: Raised when an operation or function is applied to an object of inappropriate type
- **ValueError**: Raised when an operation or function receives an argument that has the right type but an inappropriate value
- **RuntimeError**: Raised when an error is detected that doesn’t fall in any of the other categories


### Assertions

With Assertion we can test whether a condition in our code returns True or raise an AssertionError.
- `raise-if` statement
- `assert` statement

#### assert Statement

`assert` statement check a condition or expression which is supposed to be always true; otherwise, it will return AssertionError.

`assert Expression [, Arguments]`

Example:

```
def power(a,b):
    return a ** b

assert (power(3,3)==27) # This assert is True and return nothing
assert (power(2,4) == 15),"Wrong Result!!"


(output):Traceback (most recent call last):
  File "D:\Programming\Python Code\test.py", line 6, in <module>
    assert (power(2,4) == 15),"Wrong Result!!"
AssertionError: Wrong Result!!
```

### Exception Handling

In Python, there is way in which you can handle various exceptions in order to prevent any disruption during program execution.

Syntax:
```
try:
   [main code block]
except Exception1:
   If Exception1 occurs, this part will be executed.
except Exception2[, ..., ExpressionN]:
   If any of mentioned expressions occurs, this part will be executed.
...
finally:
    This part will be always executed whether an exception happens or not.
else:
    This part will be executed if no exception happens.    
```

- A single try statement can have one or several except statements.
- Except statement can have Exception or not. Even an except statement can take several Expressions.
- Except clause, Else statement and finally statement are optional but they may be a good practice.

Example:

```
try:
    num = int(input("Please enter your age: "))
except ValueError:
    print("Oops!  That was no valid number.  Try again...")
else:
    print("You are %d year(s) old!" % (num))
finally:
    print("You see this in any occasion.")


(output1):Please enter your age: 27
You are 27 year(s) old!
You can see this in any occasion.

(output2):Please enter your age: test
Oops!  It was not a valid number.
You can see this in any occasion.
```

#### Argument of an Exception

An Exception can have an argument, which will provide more information in case of any exception happens.

```
try:
   [main code block]
except Exception as Argument:
   If Exception1 occurs, this part will be executed and Argument can be printed here.
```

Example:
```
try:
    num = int(input("Please enter your age: "))
except ValueError as arg:
    print("Oops!", arg)


(output):Please enter your age: test
Oops! invalid literal for int() with base 10: 'test'
```

### Raising an Exception
There is a way in Python to throw an exception  if a condition occurs.

`raise [Exception [, args]]`

Example:
```
num = 'test'

if not type(num) is int:
    raise TypeError("The value is not an integer")


(output):Traceback (most recent call last):
  File "D:\Programming\Python Code\test.py", line 4, in <module>
    raise TypeError("The value is not an integer")
TypeError: The value is not an integer
```

### User-Defined Exceptions

Python also allows you to create your own exceptions by deriving classes from the standard built-in exceptions.
