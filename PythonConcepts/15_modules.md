---
id: 15_modules
title: Modules
sidebar_label: Modules
slug: /python_Basics/15_modules
---

---

A module can be consider same as a code library which allow us to organize our code logically. it contains set of functions, classes, variables which can be included in out application.

In order to create a module, it just requires to save our code in a file with the file extension of `.py`. This file can be later imported in our other Python application.

### Importing Modules
There are two ways of importing modules in our application:

- `import <library>`: all functions, classes an variables are imported to our application. To call a function, it requires to use `library_name.<function>`.
- `from <library> import <function/class>`: only a part of library which is desirable, is imported to our code block. To call a function, only it needs to call the function name. if we want to import all functions and classes of a module to the program and just want to write function or class name in our code, we can use `from <library_name> import *`.

```
import math

print(math.sqrt(16))
print(math.factorial(4))


(output): 4.0
24
```

```
from math import sqrt

print(sqrt(16))
print(factorial(4))


(output):4.0
Traceback (most recent call last):
  File "D:\Programming\Python Code\test.py", line 4, in <module>
    print(factorial(4))
NameError: name 'factorial' is not defined
```

Note that there is a way to rename module name in our code block by using `import <library_name> as <new_name>` statement. For example, `import numpy as np`.

#### Locating Modules Directory

When a module is imported into a code block, Python interpreter search for it based on below priorities:
1. Current directory
2. If it is not found, it will search each directory in **PYTHONPATH**
3. If the two previous steps fail, python will search the default path


#### Namespace and scoping

Namespace is a dictionary of variable names (keys) and their relating objects (values).
- if local variable and global variable have the same name, the local one has the higher priority than the global one.
- Each function or class method has it own local namespace.
- By using `global <variable_name>`, a global variable can be defined.


#### The dir() function

`dir()` is a built-in function which returnsa list of all functions of an imported module.

```
import random

names = dir(random)
print(names)


(output): ['BPF', 'LOG4', 'NV_MAGICCONST', 'RECIP_BPF', 'Random', 'SG_MAGICCONST', 'SystemRandom', 'TWOPI', '_Sequence', '_Set', '__all__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '_accumulate', '_acos', '_bisect', '_ceil', '_cos', '_e', '_exp', '_inst', '_log', '_os', '_pi', '_random', '_repeat', '_sha512', '_sin', '_sqrt', '_test', '_test_generator', '_urandom', '_warn', 'betavariate', 'choice', 'choices', 'expovariate', 'gammavariate', 'gauss', 'getrandbits', 'getstate', 'lognormvariate', 'normalvariate', 'paretovariate', 'randint', 'random', 'randrange', 'sample', 'seed', 'setstate', 'shuffle', 'triangular', 'uniform', 'vonmisesvariate', 'weibullvariate']
```

### Packages in PYTHONPATH

A package is the hierarchical file directory structure that consists of various modules and subpackages that is defined as a single application.

### PIP

PIP is a package manger for Python packages and modules. You can download 3rd party packages for your application via `pip`. In order to install `pip`, refer to this [link](https://pypi.org/project/pip/).
After installing `pip`, if the Python installation directory has been defined in environment variables, you can use below command to install new package via CMD or Terminal:

```
pip install <package_name>
```

To uninstall a package:

```
pip uninstall <package_name>
```

To query the list of installed packages:

```
pip list
```
