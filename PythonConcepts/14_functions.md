---
id: 14_functions
title: Functions
sidebar_label: Functions
slug: /python_Basics/14_functions
---

---

A function is a block of code which runs only when it is called. They can be written once and called for several times.

- It begins with `def`  keyword and function name
- Arguments can be passed to a function
- The function can return a value

In order to call a written function, it just requires to write the function name and passing the arguments if required.

* All arguments in Python are passed by reference. It means that any changes on the arguments within a function will reflect back in the calling function.

##### Syntax

```
def function_name(<parameters>):
    statements
    [return <expression>]
```

Example:
```
def additon(a,b):
    c = a + b
    return c

print(additon(10,5))

(output): 15
```

### Function Arguments

There are several types of arguments in calling a function:

- Required arguments
- Keyword arguments
- Default arguments
- Variable-length arguments


#### Required arguments

Required arguments are the parameters which are passed to a function in the correct order. The number of passed arguments should be matched to what is mentioned in function definition.

```
def addtion(a,b):
    print(a + b)

addtion(10)


(output):Traceback (most recent call last):
  File "D:\Programming\Python Code\test.py", line 4, in <module>
    addtion(10)
TypeError: addtion() missing 1 required positional argument: 'b'
```

#### Keyword arguments

When keyword arguments are used in function call, it identifies the arguments by its name. In case the order of passed arguments is not important.

```
def print_name(firstname, lastname):
    print("Hello, {} {}!".format(firstname, lastname))


print_name(lastname='Doe', firstname='John')



(output): Hello, John Doe!
```

#### Default arguments

A default value for an argument is employed in function call whenever no argument is passed.

```
def addtion(a,b=5):
    print(a + b)

addtion(10)

(output): 15
```

#### Variable-length arguments

when we don't know how many arguments will be passed to a function, we can use `*` before the arguments. If we want to pass variable-length keyword arguments, `**` is used before the arguments. In case of not passing any value, it was considered an empty tuple as its default value.

```
def average(*num):
    print(num)
    print(sum(num)/len(num))

average(19, 10, 15, 20, 13)

(output):(19, 10, 15, 20, 13)
15.4
```
```
def student_name(**name):
    print(name['student1'])

student_name(student1 = 'John', student2 = 'Sarah', student3 = 'Joe')


(output): John
```

### Return Statement

In order to let a function to return a value, we can use the `return` statement.

```
def power_3(x):
    return x**3

print(power_3(2))
print(power_3(3))
print(power_3(4))


(output):8
27
64
```

### Scope Variables (Global vs. Local)

In a program, all variable can not be accessible from different part of the code. There are two basic scopes of variables in Python:

- Global: This type of variables are accessible throughout the whole program.
- Local: This type of variables is only accessible inside the function where they are defined.

```
total = 0 # This is a global variable

def addition(a, b):
    total = a + b
    print("The total amount inside the function: ", total)
    return total

addition(4, 5)
print("The total amount outside the function: ", total)


(output):The total amount inside the function:  9
The total amount outside the function:  0
```

By using `global` statement, we can define a global variable inside a function block.

```
def addition(a, b):
    global total
    total = a + b
    print("The total amount inside the function: ", total)
    return total

addition(4, 5)
print("The total amount outside the function: ", total)


(output):The total amount inside the function:  9
The total amount outside the function:  9
```

### Anonymous Function

Anonymous function is not declared as the standard way of definition. Instead of `def` keyword, `lambda` is used create such a kind of function. They can take any number of arguments but can only have on expression. Also, they cannot be a direct call to print as it requires an expression.

`lambda arguments: expression`

Example:

```
power_x_by_y = lambda x, y: x ** y
print(power_x_by_y(2,8))


(output): 256
```

### Map, Filter and Reduce Functions
All these three are the convenience functions that can replaced with list comprehension or loops, but provide more compact approach to the problem.

#### The `map()` Function
This function applies a specified function to all items of given input list.
`map(function, list_of_inputs)`

Example:
```
sqrt_func = lambda x: x ** 0.5
num_list = range(10,20)

print(list(map(sqrt_func,num_list)))


(output): [3.1622776601683795, 3.3166247903554, 3.4641016151377544, 3.605551275463989, 3.7416573867739413, 3.872983346207417, 4.0, 4.123105625617661, 4.242640687119285, 4.358898943540674]
```

#### The `filter()` Function
This function creates a list of elements from a given input list when the specified function returns `True`.
`filter(function, list_of_inputs)`

Example:
```
float_filter = lambda x: isinstance(x,float)
input_list = [10, "aa", "10", 134.2, 13.0, '13.4', 12, 'hello', 3.14]

print(list(filter(float_filter,input_list)))


(output): [134.2, 13.0, 3.14]
```

#### The `reduce()` Function
This function will apply a rolling computation on series of input list and return a single result. Note that it is a part of `functools` module.
`reduce(function, sequence[, initial])`

Example:
```
from functools import reduce

multiplication = lambda x,y: x * y
num_list = range(1,10)

print(reduce(multiplication, num_list))
# Equivalent to 1*2*3*4*5*6*7*8*9


(output): 362880
```
