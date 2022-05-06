---
id: 14_io_in_numpy
title: Input and Output
sidebar_label: Input and Output
slug: /14_io_in_numpy
---

---

Numpy provides some functions to save `ndarray` on the disk and load the saved one from the disk.

- `numpy.save(file, arr, allow_pickle=True, fix_imports=True)`: Saves an array to a binary file in NumPy ``.npy`` format.
  - `file`: file, str, or pathlib.Path. File or filename to which the data is saved.
  - `arr`: array data to be saved.
  - `allow_pickle`: bool (optional). it allows saving object arrays using Python pickles.
  - `fix_imports`: bool (optional). Only useful in forcing objects in object arrays on Python 3 to be pickled in a Python 2 compatible way.

```
import numpy as np

arr = np.array([[2, 4], [5, 8]])
# Save the file to current directory
np.save('output', arr)
```

- `numpy.load(file, mmap_mode=None, allow_pickle=False, fix_imports=True, encoding='ASCII')`: loads arrays or pickled objects from ``.npy``, ``.npz`` or pickled files.
  - `file`: file-like object, string, or pathlib.Path. The file to read.
  - `mmap_mode`: {None, 'r+', 'r', 'w+', 'c'} (optional). If not None, then memory-map the file, using the given mode.
  - `allow_pickle`: bool (optional). it allows loading  pickled object arrays stored in npy files.
  - `fix_imports`: bool (optional). Only useful in forcing objects in object arrays on Python 3 to be pickled in a Python 2 compatible way.
  - `encoding`: str (optional). Only useful when
    loading Python 2 generated pickled files in Python 3, which includes npy/npz files containing object arrays. Values other than 'latin1', 'ASCII', and 'bytes' are not allowed, as they can corrupt numerical
    data. Default: 'ASCII'

```
import numpy as np

#load the saved output file wiht .npy extension
load_arr = np.load('output.npy')
print(load_arr)



(output):
[[2 4]
 [5 8]]
```

- `numpy.savetxt(fname, X, fmt='%.18e', delimiter=' ', newline='\n', header='', footer='', comments='# ', encoding=None,)`: saves an array to a text file.
  - `fname`: filename or file handle. If the filename ends in ``.gz``, the file is automatically saved in compressed gzip format.  
  - `X`: 1D or 2D array_like. Data to be saved to a text file.
  - `fmt`: str or sequence of strs (optional). A single format (%10.5f), a sequence of formats, or a multi-format string.
  - `delimiter`: str (optional). String or character separating columns.
  - `newline`: str (optional). String or character separating lines.
  - `header`: str (optional). String that will be written at the beginning of the file.
  - `footer`: str (optional). String that will be written at the end of the file.
  - `comments`: str (optional). String that will be prepended to the `header` and `footer` strings, to mark them as comments.
  - `encoding`: {None, str} (optional). Encoding used to encode the outputfile.

```
import numpy as np

arr = np.array([[4,5,6], [1,4,5]])
#Save the array in text format
np.savetxt('output',arr)
```

- `numpy.loadtxt(fname, dtype=<class 'float'>, comments='#', delimiter=None, converters=None, skiprows=0, usecols=None, unpack=False, ndmin=0, encoding='bytes', max_rows=None, like=None,)`: loads data from a text file. Each row in the text file must have the same number of values.
  - `fname`: filename or file handle. File, filename, or generator to read.  If the filename extension is `.gz` or `.bz2`, the file is first decompressed.
  - `dtype`: data-type (optional).
  - `comments`: str or sequence of str  (optional). The characters or list of characters used to indicate the start of a comment.
  - `delimiter`: str (optional). The string used to separate values.
  - `converters`: dict (optional). A dictionary mapping column number to a function that will parse the column string into the desired value.
  - `skiprows`: int (optional). it skips the first `skiprows` lines, including comments.
  - `usecols`: int or sequence (optional). Which columns to read, with 0 being the first.
  - `unpack` : bool (optional). If True, the returned array is transposed, so that arguments may be unpacked using `x, y, z = loadtxt(...)`.
  - `ndmin`: int (optional). The returned array will have at least `ndmin` dimensions.
  - `encoding`: str (optional). Encoding used to decode the inputfile.
  - `max_rows`: int (optional). Read `max_rows` lines of content after `skiprows` lines.
  - `like`: array_like. Reference object to allow the creation of arrays which are not NumPy arrays.

```
import numpy as np

#Load the saved txt file
load_arr = np.loadtxt('output')
print(load_arr)



(output):
[[4. 5. 6.]
 [1. 4. 5.]]
```
