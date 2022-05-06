---
id: 21_decorators
title: Decorators
sidebar_label: Decorators
slug: /Advanced Python/21_decorators
---

---


A decorator is a kind of design patter in Python that helps us to modify the behavior of function or class. A decorator should be called directly before the function that is to be extended.

### Functions
#### First-Class Objects
Functions can be passed around and applied as arguments like any objects.
```
def sqrt(num):
    print(num ** 0.5)

def sqrt_of_adds(sqrt_func, a, b):
    return sqrt_func(a+b)

sqrt_of_adds(sqrt, 10, 6)
sqrt_of_adds(sqrt, 12, 13)


(output) :4.0
5.0
```

#### Inner Functions
We can define a function inside another function.
```
def sqrt_of_adds(a,b):
    def sqrt(num):
        print(num ** 0.5)

    sqrt(a+b)

sqrt_of_adds(10,15)


(output): 5.0
```
#### Returning Functions from Functions
It is possible to define a function as an return expression.
```
def sqrt_of_adds(a,b):
    def sqrt(num):
        return num ** 0.5

    return sqrt(a+b)

print(sqrt_of_adds(10,15))


(output): 5.0
```

### Creating Decorators
In order to create a decorator below syntax can be used:
```
def decoratorFunc(func):
    def wrapper():
        [statements]
        func()
        [statements]
    return wrapper

def other_func():
    statements

dec = decoratorFunc(other_func)
```
Or in a simpler way;
```
def decoratorFunc(func):
    def wrapper():
        [statements]
        func()
        [statements]
    return wrapper

@decoratorFunc
def other_func():
    statements
```

- it is possible to save a decorator as a `.py` file and reuse it like a module in other code blocks.

Example:
```
def power_3(func):
    def wrapper():
        return func() ** 3

    return wrapper

@power_3
def num_func():
    return 10

print(num_func)
print(num_func())


(output): <function power_3.<locals>.wrapper at 0x00000128DB5A75E0>
1000
```

#### Decorating Functions with arguments
In order to decorating a function with arguments (passing arguments), we can use variable-length arguments (with `*`) and variable-length keyword arguments (with `**`) in the wrapper function.

syntax:
```
def decoratorFunc(func):
    def wrapper(*args, **kwargs):
        [statements]
        func(*args, **kwargs)
        [statements]
    return wrapper

@decoratorFunc
def other_func(arguments):
    statements
```

Example:
```
def power_3(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) ** 3

    return wrapper

@power_3
def num_func(num):
    return num

print(num_func(10))
print(num_func(num=4))


(output): 1000
64
```

#### Nesting Decorators
In Python, we can use more than one decorator for a single function. In the nesting decorators, the direction of running decorators are from inside to outside.

```
def power_3(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) ** 3
    return wrapper

def sqrt(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) ** 0.5
    return wrapper

@sqrt
@power_3
def num_func(num):
    return num

print(num_func(10)) # first 10 is powered by 3 then its square root is obtained. -- > sqrt(10^3)


(output): 31.622776601683793
```

#### Decorators with arguments
In Python, we can pass the arguments to the decorators as well.

```
def power_n(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            return func(*args, **kwargs) ** n
        return wrapper
    return decorator

@power_n(n=4)
def num_func(num):
    return num

print(num_func(3))


(output): 81
```
