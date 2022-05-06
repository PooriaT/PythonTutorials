---
id: 01_numpy_intro
title: Introduction to Numpy
sidebar_label: Introduction to Numpy
slug: /01_numpy_intro
---

---

***Numpy*** is a Python library which is short for *Numerical Python*. It is a core library for scientific and mathematical computing based on working with arrays (n-dimensional arrays) in Python.
- It is an [open source project](https://github.com/numpy/numpy).
- Due to requiring fast computation, it is mostly written in C and C++.
- The array (is stored at one continuous place in the memory) provided by Numpy is several times faster than Python lists.
- The array object in Numpy is called `ndarray`. The `ndarray` is the most import object in Numpy which is an n-dimensional array type. Each item of ndarray occupies the same size of the memory block.
- This library is widely used in *Data Science*.
- It has it own built-in functions for linear algebra and random number generation.
- It helps us to reduce loops in our code block.

### Getting Started

As `numpy` is the 3<sup>rd</sup>-party python library, it should be installed on the host. The easiest way is using `pip`. However, there are several python distribution in which the *Numpy* is available such as *Anaconda*.

`pip install numpy`

After installing the library, the `numpy` module should be imported in our code block (commonly under `np` alias).

`import numpy as np`
