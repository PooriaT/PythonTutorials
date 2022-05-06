---
id: 15_randomization
title: Randomization
sidebar_label: Randomization
slug: /15_randomization
---

---

### Introduction to Random Number
An actual lack of pattern in events calls *randomness*. So, Random is something that cannot be predicted logically.

If a random number is generated via generation algorithm, it is called *pseudo random*. In contrast, if we get it from outside source such as mouse movements, it is called *truly random*.

- Here, we are working with pseudo random number.

##### Generating Random number

Numpy supports generating random number with various available functions and methods.

- `numpy.random.randint(low, high=None, size=None, dtype=int)`: returns random integers from `low` (included) to `high` (`[low,high)`) from the *discrete uniform* distribution.
  - `low`: int or array-like of ints. Lowest (signed) integers to be drawn from the distribution.
  - `high`: int or array-like of ints (optional). If provided, one above the largest (signed) integer to be drawn from the distribution.
  - `size`: int or tuple of ints (optional).
  Output shape.
  - `dtype`: dtype (optional).


- `numpy.random.rand(d0, d1, ..., dn)`: returns random values in a given shape.
  - `d0, d1, ..., dn`: int (optional). The dimensions of the returned array, must be non-negative. If no argument is given a single Python float is returned.


- `numpy.random.choice(a, size=None, replace=True, p=None)`: returns a random sample from a given 1-D array.
  - `a`: 1-D array-like or int. If an ndarray, a random sample is generated from its elements.
  - `size`: int or tuple of ints (optional).
  Output shape.
  - `replace`: boolean (optional).
  - `p`: 1-D array-like (optional). The probabilities associated with each entry in *a*. If not given the sample assumes a *uniform distribution* over all entries in *a*.

```
from numpy import random

print("Generating random arrays:\n ", random.randint(1,10,size=(3,4)))
print("\nGenerating float random number:\n ", random.rand(2,5))
print("\nGenerating random array with choice() function:\n", random.choice([2,4,6,8,10], size=(4,4)))
print("\nGenerating random array with choice() function and various probabilities:\n", random.choice([2,4,6,8,10], p=[0.1,0.1,0.5,0.2,0.1], size=(4,4)))



(output):
Generating random arrays:
  [[5 6 8 8]
 [8 9 2 8]
 [6 4 3 7]]

Generating float random number:
  [[0.34549788 0.8703314  0.6238654  0.27296101 0.15834508]
 [0.71549553 0.36217891 0.83630135 0.60373939 0.72539127]]

Generating random array with choice() function:
 [[ 2  6  8  6]
 [ 4  6  2  8]
 [ 6 10  2  8]
 [ 4  4 10  8]]

Generating random array with choice() function and various probabilities:
 [[ 8  8  6  6]
 [ 6  8  6  8]
 [ 6  6  6 10]
 [ 8  6  2  8]]
```

### Random Permutation

There are two functions available in random module of Numpy which support permutation.

- `numpy.random.permutation(x)`: returns randomly permutation of a sequence or a range.
  - `x`: int or array_like. If `x` is an integer, randomly permute `np.arange(x)`. If `x` is an array, make a copy and shuffle the elements randomly. Also, If `x` is a multi-dimensional array, it is only shuffled along its first index.


- `numpy.random.shuffle(x)`: returns a modify of a sequence in-place by shuffling its contents. This function only shuffles the array along the first axis of a
multi-dimensional array.
  - `x`: ndarray or MutableSequence


```
import numpy as np
from numpy import random

print("Permutation of an integer:\n ", random.permutation(7))
print("\nPermutation of an array:\n ", random.permutation([2,4,6,8,10,12,14]))


arr = np.array([2,4,6,8,10,12,14])
random.shuffle(arr)
print("\nShuffle of an array:\n", arr)



(output):
Permutation of an integer:
  [4 1 2 6 0 5 3]

Permutation of an array:
  [10  8  4  6  2 12 14]

Shuffle of an array:
 [10  4 12  2  6 14  8]
```

### Normal Distribution

One of the most important distribution is normal or Gaussian distribution. The normal distributions occurs often in nature.

- `numpy.random.normal(loc=0.0, scale=1.0, size=None)`: returns random samples from a normal (Gaussian) distribution.
  - `loc`  float or array_like of floats. Mean ("centre") of the distribution.
  - `scale`: float or array_like of floats. Standard deviation (spread or "width") of the distribution. Must be non-negative.
  - `size`: int or tuple of ints (optional). Output shape.  


```
from numpy import random

print("The Normal Distribution around 3 with standard deviation of 4:")
print(random.normal(loc=3, scale=4, size=(3,4)))



(output):
The Normal Distribution around 3 with standard deviation of 4:
[[5.00034573 1.42550096 6.67598197 2.48310621]
 [2.36913696 9.01602854 5.39695816 0.9437914 ]
 [4.20424586 6.50260815 2.80410564 4.4300211 ]]
```


### Binomial Distribution

This distribution is used in binary scenarios such as toss of a coin.

- `numpy.random.binomial(n, p, size=None)`: returns samples from a binomial distribution
  - `n`: int or array_like of ints (>= 0). Number of trials.
  - `p`: float or array_like of floats (>= 0 and <=1). Probability of success.
  - `size`: int or tuple of ints (optional). Output shape.


```
from numpy import random

print("The Binomial Distribution with 10 trials and probabilities of 0.3 and 0.7:")
print(random.binomial(n=10, p=0.3, size=(3,4)))



(output):
The Binomial Distribution with 10 trials and probabilities of 0.3 and 0.7:
[[4 2 1 2]
 [6 2 2 4]
 [3 4 5 4]]
```

### Poisson Distribution
The Poisson distribution is the limit of the binomial distribution for large N.

- `numpy.random.poisson(lam=1.0, size=None)`: returns samples from a Poisson distribution.
  - `lam`: float or array_like of floats ( >= 0). Rate of occurrences.
  - `size`: int or tuple of ints (optional). Output shape.


```
from numpy import random

print("The Poisson Distribution:")
print(random.poisson(lam=2, size=(3,4)))



(output):
The Poisson Distribution:
[[0 1 5 2]
 [0 4 2 0]
 [1 3 1 1]]
```


### Uniform Distribution
It is used in where each event has the equal probability of occurring.

- `numpy.random.uniform(low=0.0, high=1.0, size=None)`: returns amples from a uniform distribution.
  - `low`: float or array_like of floats (optional). Lower boundary of the output interval.
  - `high`: float or array_like of floats. Upper boundary of the output interval.  
  - `size`: int or tuple of ints (optional). Output shape.


```
from numpy import random

print("The Uniform Distribution over the half-open interval of [2,10):")
print(random.uniform(low=2, high=10, size=(3,4)))



(output):
The Uniform Distribution over the half-open interval of [2,10):
[[3.82108475 6.6015577  5.74193066 3.52954438]
 [4.26275953 2.50943183 7.35304708 2.31406859]
 [9.57765404 9.98065273 9.91051606 3.03645088]]
```

### Logistic Distribution

The Logistic distribution is used in Extreme Value problems.

- `numpy.random.logistic(loc=0.0, scale=1.0, size=None)`: returns samples are drawn from a logistic distribution with specified parameters, loc (location or mean, also median), and scale (>0).
  - `loc`: float or array_like of floats (optional). Mean, where the peak is.
  - `scale`: float or array_like of floats (optional). Standard deviation.
  - `size`: int or tuple of ints (optional). Output shape.


```
from numpy import random

print("The Logistic Distribution round 3 with standard deviation of 10:")
print(random.logistic(loc=3, scale=10, size=(3,4)))



(output):
The Logistic Distribution round 3 with standard deviation of 10:
[[  3.55404943 -17.86043375  21.43845073  12.57212143]
 [ -7.01169034  48.05271286  -2.13341119  -2.98917385]
 [ -2.25773924 -29.27277255  21.91528143   0.29985826]]
```

### Multinomial Distribution

The multinomial distribution is a multivariate generalization of the binomial distribution.

- `numpy.random.multinomial(n, pvals, size=None)`: returns samples from a multinomial distribution.
  - `n`: int. Number of experiments
  - `pvals`: sequence of floats, length p. Probabilities of each of the `p` different outcomes.
  - `size`: int or tuple of ints (optional). Output shape.


```
from numpy import random

print("The Multinomial Distribution:")
print(random.multinomial(n=10, pvals=[0.2,0.5,0.3], size=(3,4)))



(output):
The Multinomial Distribution:
[[[2 3 5]
  [3 4 3]
  [0 5 5]
  [1 5 4]]

 [[0 7 3]
  [2 5 3]
  [1 8 1]
  [3 4 3]]

 [[1 5 4]
  [2 5 3]
  [3 6 1]
  [2 3 5]]]
```

### Exponential Distribution
The exponential distribution is a continuous analogue of the geometric distribution.

- `numpy.random.exponential(scale=1.0, size=None)`: returns samples from an exponential distribution.
  - `scale`: float or array_like of floats. Inverse of rate.
  - `size`: int or tuple of ints (optional). Output shape.


```
from numpy import random

print("The Exponential Distribution:")
print(random.exponential(scale=7 , size=(3,4)))



(ouput):
The Exponential Distribution:
[[ 1.63200432  1.9825122  10.26246741  7.27488804]
 [ 4.87008655 18.70805082  0.54084412  1.47248722]
 [ 2.73844161 16.37846642  2.6627627   8.96913951]]
```
