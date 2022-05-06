---
id: 20_generators
title: Generators
sidebar_label: Generators
slug: /Advanced Python/20_generators
---

---

A generator in Python is a kind of function that generates a sequence of results. Actually, it saves the local state then, the function can resume again from its last state. As a result, generators are a kind of powerful iterator. To do so, `yield [Expressions]` syntax is used. This keyword is much like `return`. A generator can simplify our code and cause to consume lower memory. Thus, they can be used when we are working on large amount of data or concurrency. 

Example:
```
def fibonacci():
    x1, x2 = 1, 1
    while True:
        yield  x1
        x1, x2 = x2, x1+x2

f = fibonacci()
print(next(f))
print(next(f))
print(next(f))
print(next(f))
print(next(f))
print(next(f))


(output):1
1
2
3
5
8
```
- As it can be seen from this example, the last state is saved and when the function is called, it will be resumed from its last state.
- The `next()` function will return the next item in an iterator.
- The difference between `yield` and `return` is that `yield` can save its last local state. In contrast, `return` will lose its local state
- The `return` statement can be used in the generator if it does not return any value.


### Generator Expression
Generator expression are like list comprehensions just they use parenthesis instead and return a generator instead of a list.

```
g = (i for i in range(1,10))
print(g)
print(next(g))
print(next(g))
print(next(g))
print(list(g))
print(next(g)) # Will return error as the sequence had been finished.

(output): <generator object <genexpr> at 0x0000023949AC9A50>
1
2
3
[4, 5, 6, 7, 8, 9]
Traceback (most recent call last):
  File "D:\Programming\Python Code\test.py", line 7, in <module>
    print(next(g))
StopIteration
```

### Sending values to Generators
In order to send a values to a generator that is yielded, `send` keyword is used.

```
def powerBy3():
    while True:
        n = yield
        yield n ** 3

g = powerBy3() # Create the generator
next(g)  # run up the first yield
print(g.send(10))
next(g)  # run up the next yield
print(g.send(3))


(output): 1000
27
```

### Connecting Generators
There is a possibility to connect several generators to each other. To do so, the below syntax can be used:
`yield from [Expression which refers to other generator]`

Example:
```
def fibonacci(n):
    x1, x2 = 1, 1
    i = 0
    while i < n:
        yield  x1
        x1, x2 = x2, x1+x2
        i += 1

def gen_child(n):
    yield from fibonacci(n)
    yield from fibonacci(n+10)

print(list(gen_child(5)))



(output): [1, 1, 2, 3, 5, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610]
```
