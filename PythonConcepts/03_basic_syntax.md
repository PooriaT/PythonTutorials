---
id: 03_basic_syntax
title: Basic Syntax
sidebar_label: Basic Syntax
slug: /python_Basics/03_basic_syntax
---

---

### First Programming

There are two available method for Python programming:
1. **Interactive Mode Programming** which can be accessible via CMD/Terminal. Enter `python` in CMD/Terminal and new environment which can interpret the python command will be appeared.

  ``>>> print("Welcome to Python Programming!")``

  After pressing the enter, what will be displayed as an input is:

  ``Welcome to Python Programming!``

2. **Script Mode Programing** in which it is possible to run and interpret the whole written script.

  In an text editor enter `print("Welcome to Python Programming!")` and save the file with `.py` extension (e.g. test.py). Then, run the script in the CMD/Terminal by entering `python test.py`. The output will be as below:

  ``Welcome to Python Programming!``

#### Integrated Development Environment (IDE)

There are various types of IDE in which you can write, run and even debug your Python scripts. Some of them are only text editor which can enhance to interpret your codes by adding some packages to them:

- PyCharm (IDE)
- Eclipse (IDE)
- Microsoft Visual Studio (IDE)
- Atom (Editor + required packages)


### Python Identifiers

Python identifiers are the names given to variables, functions, classes, modules and other objects which consist of lowercase letters (a-z), uppercase letters (A-Z), underscore (_) and digits (0-9). They cannot start with a digit and cannot contain the special symbols such as !, @, #, $, % and etc. **Python is a case sensitive programming language.**

There are several conventions among Python programmer which make your script more legible:
- Except classes, all other variables start with lowercase letter.
- If an identifier starts with a single underscore, it indicates that the identifier is private.
- If the identifier ends with two underscores, this identifier defined as a special name.

### Reversed Words

There are several words in Python programming which are reserved for specific purposes and cannot used as a variable or constants.

| Keywords | | | |
|:-:|:-:|:-:|:-:|
| False |	def |	if | 	raise |
| None 	| del |	import |	return |
| True 	| elif |	in | try |
| and 	| else |	is | while |
| as 	 | except |	lambda |	with |
| assert | finally |	nonlocal | yield |
| break |	for | not | class |
| from | or | continue | global | 	
| pass | | | |


### Indentations

Python does not user braces (**{}**) like C programming to indicate the code blocks for functions, classes and flow control. In order to specify these blocks, the line indentation is applied.


### Multi-Line Statements

In order to write a statement in several lines instead of one line, line continuation character (\\) can be used.

```
sum = number_1 + \
      number_2 + \
      number_3
```

### Commenting

Comments in python start with hash (#) character and continue to the end of the line.

`# This is a comment. `
