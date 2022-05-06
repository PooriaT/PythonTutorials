---
id: 02_environment_setup
title: Environment Setup
sidebar_label: Environment Setup
slug: /02_environment_setup
---

---

There are two available Python version, Python 2 and Python 3. The latest version of python 2 (2.7.18) was released on April 20, 2020 and it will not updated anymore[^1]. As a result, the best choice is to use Python 3.

If you are a Python 2 user, there is a useful guide on [Python](https://docs.python.org/3/howto/pyporting.html) official website to guide how to migrate from Python 2 to Python 3[^2].

### Python 3 setup

Python 3 is available for Windows, most distribution of Linux and Mac OS. The information related to latest version of Python is available on this [link](https://www.python.org/downloads/)

#### Widows setup

- installing the downloaded binary source which is available in this [link](https://www.python.org/downloads/windows/)
- Adding the path of installing directory of python to Environment variable.


#### Linux setup

- For Ubuntu, it is possible to use the below command to install the latest Python from trusted repositories

```
$ sudo apt-get update
$ sudo apt-get install python3.x
```
or you can download the latest version of python from this [link](https://www.python.org/downloads/source/) and install it with available package manger for your Linux distribution.
- Don't forget to add the Python directory to the path variable:

`export PYTHONPATH=/usr/local/bin/python3.x`

 #### Mac OS setup

 - Download the latest version of Python from this [link](https://www.python.org/downloads/mac-osx/) and install it by double clicking on the package.





[^1]: https://www.python.org/doc/sunset-python-2/
