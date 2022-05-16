---
id: 16_file_io
title: File I/O
sidebar_label: File I/O
slug: /python_Basics/16_file_io
---

---


### Printing on the Screen

In order to print on the screen, `print` statement can be used. This statement can take zero or more expressions.

```
>>> print("Hello, Python.", "This is a simple test!!")
Hello, Python. This is a simple test!!
```

### Reading Keyboard Input

In order to take an input from Keyboard, `input` statement is used. This statement can be take a prompt as well to show on the screen before inserting any input.

```
>>> name = input("Please, insert your name: ")
Please, insert your name: John
>>> name
'John'
```

### File handling in Python

Python provides some functions and methods to manipulate files.

#### The Open Function

Before Reading and writing any file, it requires to be opened first with Built-in `open()` function. This function creates a file object which can be called with other supported methods later in the code block. (Note that file directory should be completely mentioned in filename.)

`file_obj = open(filename [, access_mode])`

- **access_mode**: determines the mode of opening file. For example, read-only, write, append and etc. refer to below to find various access modes.

  - `r`: Read - Default value (if access_mode is not inserted). Opens a file for reading, error will be returned if the file does not exist.
  - `w`: Write - Opens a file for writing, creates the file if the file does not exist.
  - `a`: Append - Opens a file for appending, creates the file if the file does not exist.
  - `x`: Create - Creates a file and will return error if the file exists.
  - `t`: Text - Default value
  - `b`: Binary - Binary mode such as images


Note that these modes can be inserted all together. For instance, `rb` is a read and binary mode. In addition, if we want to both read and write a file we can use `r+` or `w+`.

#### The Close Function

The `close()` method of a file flushes an unwritten information and closes the file object then no more item can be written on the file.

`file_obj.close()`

Example:

```
f_obj = open('test.txt', 'r+') # Open the file

print("File name: ", f_obj.name)
print("File is opened or closed: ", f_obj.closed)
print("File access mode: ", f_obj.mode)

f_obj.close() # Close the file


(output):File name:  test.txt
File is opened or closed:  False
File access mode:  r+
```

#### The Read Function

By `read()` method, a string can be read from an opened file.

`file_obj.read([count])`

* If we want to specify the number of bytes which should be read, we pass a parameter to the `read()` method (`count`). Otherwise, it will read as mush as possible.

In order to read one line. `readline()` method can be applied.

```
f_obj = open('test.txt', 'r+') # Open the file
text = f_obj.read()
print(text)
f_obj.close() # Close the file


(output): This is a test.
```

#### The Write Function

In order to write any string to a specified file, `write()` method can be used. Escape characters can be applied to use special characters inside the string. For instance, to add new line, we can use `\n`.

`file_obj.write(<string>)`


```
f_obj = open('test.txt', 'r+') # Open the file
f_obj.write("I am writing ...!!!\n")
f_obj.close() # Close the file
```

#### File Position

If we want to check the current position of pointer in our file, `tell()` method can be used. In order to change the pointer position, we can use `seek(offset[, from])` method. In this method, `offset` means the number of bytes which we need to move and `from` shows the reference position.

```
f_obj = open('test.txt', 'r+') # Open the file

text = f_obj.read(23)
print(text, "\n")
# Showing hte Current position
print("Current position of the pointer: ", f_obj.tell(), "\n")
# Changing the pointer position
position = f_obj.seek(24,0)
text = f_obj.read()
print("After chaning the poinster position:\n" + text)

f_obj.close() # Close the file


(output):This is the first line.

Current position of the pointer:  23

After chaning the poinster position:
This is the second line.
This is the third line.
This is the fourth line.
```

#### Renaming and Deleting Files

In order to rename or delete a file, a useful built-in Python module `os` can be used.

- Rename: `os.rename(current_file_name, desired_file_name)`
- Delete: `os.remove(file_name)`

In both method, if the file does not exist, they return an error.

```
import os

os.rename('test.txt', 'new_test.txt')
os.remove('new_test.txt')
```

#### Creating, removing and Changing Directory

Python `os` module provides several methods to create, change, remove and get the current directory.

- Create the directory: `os.mkdir(<new_dir_name>)`
- Change the directory: `os.chdir(<new_dir>)`
- Displaying the current working directory: `os.getcwd`
- Deleting the directory: `os.rmdir(<dir>)`
