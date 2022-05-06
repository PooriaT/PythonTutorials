---
id: 19_classes
title: Classes and Objects
sidebar_label: Classes and Objects
slug: /Advanced Python/19_classes
---

---

Python is an Object-Oriented Programming (OOP) language. Almost everything in python is an object with its properties and methods.

### Object-Oriented Programming (OOP) Overview
Here we look at terminology which is used in OOP concepts:
- **Class**: A user-defined structure for an object which characterize any objects with relevant attributes.
- **Object**: A unique instance created by its class which is a kind of a data structure. An object includes both variables (class variables and instance variables) and methods.
- **Class variable**: They are defined within a class structure but outside the class's methods and shared by all instances of that class.
- **Instance**: An individual object of a specified class.
- **Instance variable**: A variable which is defined inside the class method and belongs to the current instance of a class
- **Inheritance**: transferring the characteristics and features of a class to another classes.
- **Instantiation**: The creation of an instance of a class.
- **Method**: A special kind of function that is defined in a class definition.

### Class Creation

In order to create a class, `class` keyword is used. Based on a convention among programmer, they use the capital letter for the first letter of the class name.

Syntax:
```
class ClassName:
   statements (Variable, Initialization and Methods)
```

Example:
```
class Student:
    # Class Variable
    student_num = 0

    # Initialization
    def __init__(self,name, id):
        self.name = name
        self.id = id
        Student.student_num += 1

    # Method
    def getName(self):
        print("The id of ", self.name, " is ", self.id)

    def getNumberOfStudnet(self):
        print("Total number of students is ", Student.student_num)
```

- The `__init__()` function: it is used when the class is initiated (class constructor).
- The `self` parameter: is reference to the current instance of the class and is used to access variables belongs to the class

### Object Creation
Now, by using the created class (ClassName), an instance of class can be created.

```
## Creating an instance object
student_1 = Student("John", "EE202130M")
student_2 = Student("Sarah", "CS202180F")
```

### Accessing to Attributes
In order to access to the object attributes, a dot operator can be used.

```
## Accessing Attributes
student_1.getName()
student_2.getName()
```

The whole example together:
```
class Student:
    # Class Variable
    student_num = 0

    # Initialization
    def __init__(self,name, id):
        self.name = name
        self.id = id
        Student.student_num += 1

    # Methods
    def getName(self):
        print("The id of ", self.name, " is ", self.id)

    def getNumberOfStudnet(self):
        print("Total number of students is ", Student.student_num)


## Creating an instance object
student_1 = Student("John", "EE202130M")
student_2 = Student("Sarah", "CS202180F")

## Accessing Attributes
student_1.getName()
student_2.getName()
print("Total number of students is ", Student.student_num)



(output): The id of  John  is  EE202130M
The id of  Sarah  is  CS202180F
Total number of student is  2
```

### Built-In Class Attributes
All Python classes can use some specified built-in attributes which can be accessible by dot operator.
- **\_\_dict\_\_**: Dictionary containing the class's namespace
- **\_\_doc\_\_**: Class documentation string if it is defined.
- **\_\_name\_\_**: Class name
- **\_\_module\_\_**: Module name
- **\_\_bases\_\_**: Tuple containing the base classes if applicable

```
class Student:
    '''
    This is a simple Student class to show the basic concepts.
    1- Class creation
    2- Object creation
    3. Accesing to attributes
    '''
    # Class Variable
    student_num = 0

    # Initialization
    def __init__(self,name, id):
        self.name = name
        self.id = id
        Student.student_num += 1

    # Methods
    def getName(self):
        print("The id of ", self.name, " is ", self.id)

    def getNumberOfStudnet(self):
        print("Total number of students is ", Student.student_num)


## Creating an instance object
student_1 = Student("John", "EE202130M")
student_2 = Student("Sarah", "CS202180F")

## Built-in attributes
print("Student.__dict__:", Student.__dict__)
print("Student.__doc__:", Student.__doc__)
print("Student.__name__:", Student.__name__)
print("Student.__module__:", Student.__module__)
print("Student.__bases__:", Student.__bases__)



(output): Student.__dict__: {'__module__': '__main__', '__doc__': '\n    This is a simple Student class to show the basic concepts.\n    1- Class creation\n    2- Object creation\n    3. Accesing to attributes\n    ', 'student_num': 2, '__init__': <function Student.__init__ at 0x00000232918275E0>, 'getName': <function Student.getName at 0x0000023291827670>, 'getNumberOfStudnet': <function Student.getNumberOfStudnet at 0x00000232918273A0>, '__dict__': <attribute '__dict__' of 'Student' objects>, '__weakref__': <attribute '__weakref__' of 'Student' objects>}
Student.__doc__:
    This is a simple Student class to show the basic concepts.
    1- Class creation
    2- Object creation
    3. Accesing to attributes

Student.__name__: Student
Student.__module__: __main__
Student.__bases__: (<class 'object'>,)
```

### Destroying Object and Object Properties

in order to delete the object or its properties, `del` keyword can be used.

```
del student_1.name # Deleting the object property
del student_1 # deleting the object itself
```

### Class Inheritance
Inheritance helps us to create class that inherits all the properties and methods from another class.
- **Parent Class**: a class being inherited (base class)
- **Child Class:**: a class inherits from another class (derived class)

Syntax:
```
class ChildClassName(ParentClass_1 [, ParentClass_2, ...]):
    Statements
```

Example:
```
# Creating the Parent Class
class Person():
    # Initialization
    def __init__(self, firstname, lastname):
        self.firstname = firstname
        self.lastname = lastname

    # Methods
    def getName(self):
        print("Hello,", self.firstname, self.lastname)

# Creating the Child Class
class Student(Person):
    def __init__(self,firstname,lastname, id):
        self.id = id
        Person.__init__(self,firstname,lastname)
        # or we can use the following statement instead
        # super().__init__(firstname, lastname)

    def getInfo(self):
        print("Hello,", self.firstname, self.lastname)
        print("Your Id is", self.id)


# Creating objects
student_1 = Student("John", "Doe", "EE2021M")
student_1.getName()
student_1.getInfo()


(output): Hello, John Doe
Hello, John Doe
Your Id is EE2021M
```

- The `super()` function will also make the child class inherits all the methods and properties of its parent.
- The `issubclass(sub, suo)` function: is the Boolean function that returns True if the mentioned subclass is the child of the specified super class.
- the `isinstance(obj, Class)` function: is the Boolean function that returns True if the mentioned object is the instance of te specified class.

### Overriding Methods
It is possible to override the methods of parent class in the child class structure.

```
# Creating the Parent Class
class Person():
    # Initialization
    def __init__(self, firstname, lastname):
        self.firstname = firstname
        self.lastname = lastname

    # Methods
    def getName(self):
        print("Hello,", self.firstname, self.lastname, "from Person Class!!")

# Creating the Child Class
class Student(Person):
    def __init__(self,firstname,lastname, id):
        self.id = id
        Person.__init__(self,firstname,lastname)
        # or we can use the following statement instead
        # super().__init__(firstname, lastname)

    def getName(self):
        print("Hello,", self.firstname, self.lastname, "from Student Class!!")



# Creating objects
student_1 = Student("John", "Doe", "EE2021M")
student_1.getName()


(output): Hello, John Doe from Student Class!!
```

### Overloading Operators
In python, it is possible to overloading the operators based on our necessities.

```
class Vector:
    #Initialization
    def __init__(self,x,y):
        self.x = x
        self.y = y

    def __str__(self):
        return "The vector is {}i+{}j".format(self.x,self.y)

v1 = Vector(10,15)
print(str(v1))


(output): The vector is 10i+15j
```

### Data Hiding
Except C programming, Python does not have private member variable. To do so, we can use double underline (__) before the name attributes.


```
class MyClass:
    __invisibleVariable = "test"

    def changeContent(self):
        self.__invisibleVariable = "hello"
        print(self.__invisibleVariable)

obj_1 = MyClass()
obj_1.changeContent()
print(obj_1.__invisibleVariable)


(output): hello
Traceback (most recent call last):
  File "D:\Programming\Python Code\test.py", line 10, in <module>
    print(obj_1.__invisibleVariable)
AttributeError: 'MyClass' object has no attribute '__invisibleVariable'
```

- In order to access this kind of variables, we can use this statement, `obj._ClassName__attrName`.
