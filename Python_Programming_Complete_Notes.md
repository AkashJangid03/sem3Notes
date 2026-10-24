# Python Programming --- Complete Exam Notes

**Based on the six PDFs shared for Python Programming**\
**Purpose:** Semester exam preparation, concept revision, and practical
coding.

> These notes reorganize the topics covered in the supplied PDFs. Code
> examples are written in standard Python 3. Some examples clarify
> syntax where the slide formatting was ambiguous.

## Contents

1.  Introduction to Python
2.  Python Execution, Compiler and Interpreter
3.  Variables, Objects, `id()` and Data Types
4.  Operators and Type Conversion
5.  Input and Output
6.  Control Structures and Loops
7.  Strings and String Methods
8.  Functions
9.  Modules and Imports
10. Object-Oriented Programming (OOP)
11. Exception Handling
12. Important Differences
13. Practical Programs
14. Exam/Viva Questions
15. Quick Revision Sheet

------------------------------------------------------------------------

# 1. Introduction to Python

## 1.1 What is Python?

Python is a high-level, general-purpose programming language known for
readable syntax. It supports procedural, object-oriented, and functional
programming styles.

### Features of Python

-   **High-level:** syntax is relatively close to human-readable
    language.
-   **Interpreted execution model:** Python implementations execute
    Python code through a runtime; CPython compiles source to bytecode
    and executes it on the Python Virtual Machine.
-   **Open source:** freely available to use and distribute under its
    licence.
-   **Portable:** available on Windows, macOS, Linux and other
    platforms.
-   **Object-oriented:** supports classes and objects.
-   **Interactive:** statements can be tested in an interactive shell.
-   **Large standard library:** includes modules such as `math`,
    `random`, `datetime`, `os` and \`sys.
-   **Versatile:** used for scripting, web development, automation, data
    analysis, scientific computing, testing and many other tasks.

## 1.2 Applications of Python

Examples of areas in which Python is used: - Web applications and APIs -
Automation and scripting - Data analysis and visualisation - Scientific
and numerical computing - Artificial intelligence and machine learning -
Software testing - Desktop utilities and games - Scripting within some
design and engineering tools

## 1.3 System software vs application software

  -----------------------------------------------------------------------
  Basis                   System software         Application software
  ----------------------- ----------------------- -----------------------
  Purpose                 Manages computer        Performs tasks for end
                          hardware and resources  users

  Role                    Provides a platform for Uses services provided
                          applications            by system software

  Examples                Operating systems,      Web browsers, word
                          device drivers,         processors,
                          compilers, utilities    spreadsheets

  Hardware interaction    Generally manages       Usually accesses
                          hardware more directly  hardware through system
                                                  services
  -----------------------------------------------------------------------

## 1.4 Basic Python program

``` python
print("Hello, Python!")
```

`print()` displays information. Python uses indentation to mark code
blocks.

### Comments

``` python
# This is a single-line comment
print("Hello")
```

Comments explain code and are ignored during normal execution.

### Identifiers and naming rules

An identifier is a name used for a variable, function, class, etc. - May
contain letters, digits and underscores. - Cannot begin with a digit. -
Cannot be a Python keyword. - Names are case-sensitive: `marks`, `Marks`
and `MARKS` are different. - Use meaningful names such as `total_marks`.

## 1.5 Indentation

Python uses indentation to group statements instead of braces.

``` python
marks = 75
if marks >= 50:
    print("Pass")
    print("Condition was true")
print("Program finished")
```

The two indented statements belong to the `if` block. The final
statement is outside it.

------------------------------------------------------------------------

# 2. Python Execution, Compiler and Interpreter

## 2.1 Compiler vs interpreter

  -----------------------------------------------------------------------
  Compiler (general model)            Interpreter (general model)
  ----------------------------------- -----------------------------------
  Commonly translates a program or    Commonly executes code through a
  large unit before execution         runtime, often statement by
                                      statement

  May produce a separate executable   May execute without creating a
  or intermediate code                standalone executable

  Errors may be reported during       Runtime errors may appear when the
  compilation                         affected code is executed

  Example languages often taught with Python is commonly described as
  this model: C, C++                  interpreted
  -----------------------------------------------------------------------

**Important nuance:** "Python is interpreted" is a useful introductory
description, but CPython first compiles source code to bytecode (`.pyc`
may be cached) and then executes bytecode in the Python Virtual Machine
(PVM).

## 2.2 Python implementations

An implementation is software that implements the Python language and
runs Python programs.

  -----------------------------------------------------------------------
  Implementation                      Key point
  ----------------------------------- -----------------------------------
  CPython                             Main and most widely used
                                      implementation; written in C

  PyPy                                Uses a Just-In-Time (JIT) compiler
                                      to speed up frequently executed
                                      code

  Jython                              Python implementation for the Java
                                      ecosystem/JVM

  IronPython                          Python implementation designed for
                                      the .NET ecosystem
  -----------------------------------------------------------------------

### CPython execution flow

`Python source (.py) → bytecode → Python Virtual Machine (PVM) → execution/output`

## 2.3 `id()` and object identity

`id(object)` returns an integer that is unique and constant for that
object's lifetime. In CPython, it commonly corresponds to the object's
memory address, but Python's language definition does **not** guarantee
that interpretation for every implementation.

``` python
x = 100
print(id(x))
```

The exact number can vary between runs and implementations. Use `id()`
to inspect identity, not to assume a portable memory address.

------------------------------------------------------------------------

# 3. Variables, Objects and Data Types

## 3.1 Variables and objects

A variable name refers to an object. Assignment binds a name to an
object.

``` python
x = 10
name = "Rahul"
percentage = 82.5
```

Here `x` refers to an integer object, `name` to a string object and
`percentage` to a floating-point object.

Python is dynamically typed: the type is associated with the object, and
a name can later refer to an object of another type.

``` python
value = 10
value = "Python"
```

## 3.2 Common built-in data types

  Type          Description                                 Example
  ------------- ------------------------------------------- -----------------------------------------
  `int`         Integer numbers                             `age = 21`
  `float`       Floating-point numbers                      `percentage = 82.5`
  `complex`     Complex numbers                             `z = 2 + 3j`
  `bool`        Boolean values                              `is_valid = True`
  `str`         Text/character sequence                     `name = "Rahul"`
  `list`        Ordered, mutable collection                 `marks = [70, 80, 90]`
  `tuple`       Ordered, immutable collection               `point = (2, 5)`
  `range`       Sequence of integers, often used in loops   `range(5)`
  `dict`        Key-value mapping                           `student = {"name": "Asha", "age": 21}`
  `set`         Unordered collection of unique elements     `ids = {1, 2, 3}`
  `frozenset`   Immutable set                               `frozenset({1, 2})`
  `NoneType`    Represents absence of a value               `result = None`
  `bytes`       Immutable byte sequence                     `data = b"ABC"`
  `bytearray`   Mutable byte sequence                       `data = bytearray(b"ABC")`

Check a value's type with:

``` python
x = 10
print(type(x))       # <class 'int'>
```

## 3.3 Mutable and immutable objects

-   **Immutable:** object cannot be changed in place after creation.
    Examples: `int`, `float`, `bool`, `str`, `tuple`, `frozenset`,
    `bytes`.
-   **Mutable:** object can be changed in place. Examples: `list`,
    `dict`, `set`, `bytearray`.

Example:

``` python
text = "cat"
# text[0] = "b"   # TypeError: strings are immutable
text = "bat"      # valid: name now refers to a new string

items = [1, 2, 3]
items[0] = 9      # valid: list is mutable
print(items)      # [9, 2, 3]
```

## 3.4 Important object concepts

-   **Object:** a value managed by Python.
-   **Type/class:** describes an object's kind and the operations
    supported by it.
-   **Identity:** distinguishes one object from another; inspected with
    `id()`.
-   **Value:** the data represented by an object.
-   `is` checks identity; `==` checks equality of values in most
    ordinary comparisons.

``` python
a = [1, 2]
b = [1, 2]
print(a == b)  # True: equal contents
print(a is b)  # False: different list objects
```

Avoid using `is` to compare ordinary values; use `==`. `is` is commonly
used for singleton checks such as `value is None`.

## 3.5 Type conversion

Conversion functions include `int()`, `float()`, `str()`, `bool()`,
`list()`, `tuple()`, `set()` and `dict()` (where input shape permits).

``` python
age_text = "21"
age = int(age_text)
price = float("45.50")
message = str(100)
print(age + 1)       # 22
```

Invalid conversion can raise `ValueError`:

``` python
# int("hello")  # ValueError
```

`input()` returns text, so convert numeric input before arithmetic:

``` python
age = int(input("Enter age: "))
print(age + 1)
```

## 3.6 Truth values

Values such as `False`, `None`, numeric zero, and empty
collections/strings are false-like. Most other values are true-like.

``` python
name = ""
if name:
    print("Name entered")
else:
    print("Name is empty")
```

------------------------------------------------------------------------

# 4. Operators and Input/Output

## 4.1 Arithmetic operators

  Operator   Meaning          Example/result
  ---------- ---------------- -----------------
  `+`        Addition         `5 + 2` → `7`
  `-`        Subtraction      `5 - 2` → `3`
  `*`        Multiplication   `5 * 2` → `10`
  `/`        True division    `5 / 2` → `2.5`
  `//`       Floor division   `5 // 2` → `2`
  `%`        Remainder        `5 % 2` → `1`
  `**`       Exponentiation   `2 ** 3` → `8`

## 4.2 Comparison operators

`==`, `!=`, `>`, `<`, `>=`, `<=` compare values and return a Boolean
result.

## 4.3 Logical operators

-   `and`: true when both conditions are true.
-   `or`: true when at least one condition is true.
-   `not`: reverses the truth value.

``` python
age = 25
experience = 3
if age >= 21 and experience >= 2:
    print("Eligible")
```

## 4.4 Assignment and membership

-   Assignment: `=`, `+=`, `-=`, `*=`, `/=`, etc.
-   Membership: `in`, `not in`.

``` python
skills = ["Python", "SQL"]
print("SQL" in skills)  # True
```

## 4.5 Input and output

``` python
name = input("Enter name: ")
print("Hello", name)
print(f"Hello, {name}")
```

An f-string embeds expressions inside `{}`:

``` python
marks = 85
print(f"Marks: {marks}")
```

------------------------------------------------------------------------

# 5. Control Structures and Loops

Control structures determine which statements execute and how often.

## 5.1 `if` statement

Executes a block when a condition is true.

``` python
marks = 75
if marks >= 50:
    print("Pass")
```

## 5.2 `if-else`

Chooses between two alternatives.

``` python
age = 20
if age >= 18:
    print("Eligible")
else:
    print("Not eligible")
```

## 5.3 `if-elif-else`

Tests multiple conditions in order. The first true branch executes.

``` python
salary = 75000
if salary >= 100000:
    grade = "A"
elif salary >= 70000:
    grade = "B"
elif salary >= 40000:
    grade = "C"
else:
    grade = "D"
print(grade)  # B
```

## 5.4 Nested `if`

An `if` statement inside another conditional.

``` python
username = "admin"
password = "1234"

if username == "admin":
    if password == "1234":
        print("Login successful")
    else:
        print("Invalid password")
else:
    print("Invalid username")
```

This is a syntax illustration, not a secure authentication system; real
passwords should not be hard-coded or stored as plain text.

## 5.5 `for` loop

Iterates over items in a sequence or other iterable.

``` python
skills = ["Python", "SQL", "Java"]
for skill in skills:
    print(skill)
```

## 5.6 `range()`

`range()` generates a sequence of integers, commonly for loops.

Syntax: `range(start, stop, step)`; `stop` is excluded.

``` python
for i in range(5):
    print(i)          # 0 to 4

for i in range(1, 6):
    print(i)          # 1 to 5

for i in range(2, 11, 2):
    print(i)          # 2, 4, 6, 8, 10

for i in range(10, 0, -1):
    print(i)          # 10 down to 1

for i in range(1, 10, 3):
    print(i)          # 1, 4, 7
```

## 5.7 `while` loop

Repeats while the condition remains true. Update the loop variable to
avoid an unintended infinite loop.

``` python
count = 1
while count <= 5:
    print(count)
    count += 1
```

## 5.8 `break`, `continue` and `pass`

-   `break`: terminates the nearest enclosing loop.
-   `continue`: skips the rest of the current iteration and proceeds to
    the next.
-   `pass`: does nothing; used as a placeholder where a statement is
    syntactically required.

``` python
employees = ["Amit", "Neha", "Ravi", "Priya"]
for employee in employees:
    if employee == "Ravi":
        break
    print(employee)
# Amit
# Neha
```

Skip one item with `continue`:

``` python
for employee in employees:
    if employee == "Ravi":
        continue
    print(employee)
# Amit, Neha, Priya (each on a separate line)
```

## 5.9 Nested loops

A loop inside another loop. The inner loop runs for each iteration of
the outer loop.

``` python
for row in range(1, 4):
    for col in range(1, 3):
        print(row, col)
```

## 5.10 Common loop mistakes

-   Forgetting the colon `:`.
-   Incorrect indentation.
-   Using a step that moves away from the loop's stopping condition.
-   Forgetting to update the condition variable in a `while` loop.
-   Assuming `range(1, 5)` includes `5`; it does not.

------------------------------------------------------------------------

# 6. Strings and String Methods

## 6.1 Definition

A string (`str`) is a sequence of Unicode characters written using
single quotes, double quotes or triple quotes. Python does not have a
separate character type; a single character is a string of length one.

``` python
a = 'hello'
b = "world"
letter = 'A'
paragraph = """This is
multiple-line text."""
```

## 6.2 Indexing

Indexing starts at `0`; negative indexes count from the end.

``` python
s = "Python"
print(s[0])   # P
print(s[3])   # h
print(s[-1])  # n
print(s[-2])  # o
```

An index outside the valid range raises `IndexError`.

## 6.3 Slicing

Syntax: `string[start:stop:step]`. The stop position is excluded.

``` python
s = "Python"
print(s[:3])    # Pyt
print(s[2:])    # thon
print(s[1:4])   # yth
print(s[::-1])  # nohtyP
```

## 6.4 Immutability

Strings cannot be changed in place. Methods create and return a new
string.

``` python
s = "python"
# s[0] = "P"  # TypeError
s = "P" + s[1:]
print(s)        # Python
```

## 6.5 Concatenation and repetition

``` python
first = "Hello"
last = "World"
print(first + ", " + last)  # Hello, World
print("Ha" * 3)             # HaHaHa
```

A string cannot be concatenated directly with an integer:

``` python
age = 25
print("Age: " + str(age))   # convert integer to string
print(f"Age: {age}")        # or use an f-string
```

## 6.6 Common string methods

  ---------------------------------------------------------------------------------
  Method                  Purpose                 Example
  ----------------------- ----------------------- ---------------------------------
  `lower()`               Converts to lowercase   `"PyThOn".lower()` → `"python"`

  `upper()`               Converts to uppercase   `"python".upper()` → `"PYTHON"`

  `capitalize()`          Capitalizes first       `"hello world".capitalize()`
                          character               

  `title()`               Capitalizes words       `"hello world".title()`

  `strip()`               Removes                 `"  hi  ".strip()`
                          leading/trailing        
                          whitespace              

  `lstrip()`              Removes leading         `"  hi".lstrip()`
                          whitespace              

  `rstrip()`              Removes trailing        `"hi  ".rstrip()`
                          whitespace              

  `replace(old, new)`     Replaces occurrences    `"banana".replace("a", "o")`

  `split(sep)`            Splits into a list      `"a,b,c".split(",")`

  `join(iterable)`        Joins strings using     `"-".join(["a", "b"])` → `"a-b"`
                          separator               

  `find(sub)`             First index or `-1` if  `"python".find("th")` → `2`
                          absent                  

  `index(sub)`            First index; raises     `"python".index("th")` → `2`
                          `ValueError` if absent  

  `count(sub)`            Counts non-overlapping  `"banana".count("a")` → `3`
                          occurrences             

  `startswith(prefix)`    Checks prefix           `"python".startswith("py")`

  `endswith(suffix)`      Checks suffix           `"report.pdf".endswith(".pdf")`

  `isalpha()`             True if all characters  `"Hello".isalpha()`
                          are letters and         
                          non-empty               

  `isdigit()`             True if all characters  `"123".isdigit()`
                          are digits and          
                          non-empty               

  `isalnum()`             True if all characters  `"abc123".isalnum()`
                          are letters/digits and  
                          non-empty               
  ---------------------------------------------------------------------------------

String methods are case-sensitive unless the text is normalized first:

``` python
stored = "Python"
entered = "PYTHON"
print(stored == entered)  # False
print(stored.lower() == entered.lower())  # True
```

## 6.7 Escape sequences

Common escape sequences: - `\n`: newline - `\t`: horizontal tab - `\\`:
backslash - `\'`: single quote - `\"`: double quote

``` python
print("Hello\nWorld")
print("Name:\tRahul")
```

A raw string, such as `r"C:\new\test"`, treats backslashes largely as
literal characters, useful for paths and patterns.

## 6.8 Formatting strings

``` python
name = "Asha"
marks = 91
print(f"{name} scored {marks} marks.")
print("Name: {}, Marks: {}".format(name, marks))
```

## 6.9 Practical text-cleaning example

``` python
raw_email = "  Student@Example.com \n"
email = raw_email.strip().lower()
print(email)  # student@example.com
```

For validation, cleaning and checking are separate steps; a normalized
string is not automatically a valid email address.

------------------------------------------------------------------------

# 7. Functions

## 7.1 Definition and advantages

A function is a named, reusable block of code that performs a particular
task. It can receive data, process it and return a result.

Advantages: - Reduces repeated code. - Makes programs easier to read and
test. - Improves reuse and maintenance. - Breaks a large task into
smaller tasks.

## 7.2 Defining and calling a function

Use `def` to define a function. The body is indented. Defining a
function does not normally execute its body; call it to run it.

``` python
def greet():
    print("Hello")

greet()
```

## 7.3 Parameters and arguments

-   **Parameter:** variable listed in the function definition.
-   **Argument:** actual value supplied when calling the function.

``` python
def greet(name):       # name is a parameter
    print("Hello", name)

greet("Rahul")         # "Rahul" is an argument
```

## 7.4 Return value vs print

`print()` displays a value. `return` sends a result back to the caller
and ends that function call.

``` python
def calculate_sum(a, b):
    return a + b

result = calculate_sum(10, 20)
print(result)          # 30
```

If a function reaches the end without a `return` value, it returns
`None`.

## 7.5 Function arguments

### Positional arguments

Values are assigned according to position.

``` python
def student(name, age):
    print("Name:", name)
    print("Age:", age)

student("Rahul", 21)
```

### Keyword arguments

Parameter names are specified, so order can differ.

``` python
student(age=21, name="Rahul")
```

### Default arguments

A parameter can have a default value.

``` python
def show_student(name, course="M.Sc. CA"):
    print("Name:", name)
    print("Course:", course)

show_student("Rahul")
show_student("Amit", "M.Sc. Computer Science")
```

### Variable-length positional arguments: `*args`

Extra positional arguments are collected into a tuple.

``` python
def add(*numbers):
    total = 0
    for n in numbers:
        total += n
    return total

print(add(10, 20))          # 30
print(add(10, 20, 30, 40))  # 100
```

### Variable-length keyword arguments: `**kwargs`

Extra keyword arguments are collected into a dictionary.

``` python
def student_details(**details):
    print(details)

student_details(name="Rahul", age=21, course="M.Sc. CA")
# {'name': 'Rahul', 'age': 21, 'course': 'M.Sc. CA'}
```

## 7.6 Multiple return values

Python allows returning multiple values; they are packed into a tuple.

``` python
def calculate(a, b):
    return a + b, a - b, a * b

total, difference, product = calculate(10, 5)
print(total, difference, product)  # 15 5 50
```

## 7.7 Scope: local and global variables

A local variable is created inside a function and is normally available
only there. A global variable is defined at module level.

``` python
college = "Fergusson College"

def display():
    course = "M.Sc. CA"   # local
    print(college, course)

display()
```

Use `global` only when a function must rebind a module-level variable;
generally, returning values is easier to test and maintain.

## 7.8 Recursion

Recursion occurs when a function calls itself. A recursive function
needs a base case to stop.

``` python
def factorial(n):
    if n <= 1:       # base case
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # 120
```

For negative input, this example does not implement a meaningful
factorial; production code should validate input.

## 7.9 Lambda function

A lambda is a small anonymous function containing a single expression.

``` python
square = lambda x: x * x
print(square(5))  # 25
```

Use `def` for functions that need multiple statements or clearer
documentation.

## 7.10 Docstrings

A docstring documents what a function, class or module does.

``` python
def square(n):
    """Return the square of n."""
    return n * n
```

------------------------------------------------------------------------

# 8. Modules and Imports

## 8.1 What is a module?

A module is a Python file (`.py`) containing code such as variables,
functions, classes, constants and statements that can be reused in
another program.

Example project structure:

``` text
college_management/
    student.py
    faculty.py
    attendance.py
    examination.py
    fees.py
    main.py
```

Splitting a large program into modules makes it easier to understand,
debug, maintain, reuse and develop collaboratively.

## 8.2 Module-related terminology

  Term        Meaning
  ----------- ------------------------------------------------------------
  Module      A Python file containing reusable code
  Import      Making a module's names available to another module
  Package     A way to organise related modules in a directory hierarchy
  Library     A collection of reusable modules/packages
  Namespace   Mapping in which names are associated with objects

## 8.3 Types of modules

-   **Standard-library modules:** included with Python, e.g. `math`,
    `random`, `datetime`, `os`, `sys`.
-   **User-defined modules:** created by the programmer,
    e.g. `student.py`, `calculation.py`.
-   **Third-party modules:** installed separately, e.g. `numpy`,
    `pandas`, `matplotlib`.

## 8.4 Importing modules

### Import the whole module

``` python
import math
print(math.sqrt(25))      # 5.0
print(math.pi)
print(math.factorial(5))  # 120
```

### Import a specific function

``` python
from math import sqrt
print(sqrt(25))
```

### Import multiple names

``` python
from math import sqrt, factorial
print(sqrt(25))
print(factorial(5))
```

### Alias

``` python
import math as m
print(m.sqrt(25))
```

`from module import *` is possible, but it is usually discouraged
because it can make the origin of names unclear and can cause naming
conflicts.

## 8.5 Creating a user-defined module

File `calculation.py`:

``` python
def add(a, b):
    return a + b

PI = 3.14159
```

File `main.py` in the same directory:

``` python
import calculation
print(calculation.add(10, 20))
print(calculation.PI)
```

## 8.6 The `if __name__ == "__main__"` guard

When a file is run directly, its `__name__` is set to `"__main__"`. When
imported, its `__name__` is normally the module name.

``` python
def main():
    print("Program started")

if __name__ == "__main__":
    main()
```

This allows test/demo code to run directly without automatically running
when the module is imported.

------------------------------------------------------------------------

# 9. Object-Oriented Programming (OOP)

## 9.1 Basic concepts

-   **Class:** a blueprint describing attributes and behaviours.
-   **Object:** an instance of a class.
-   **Attribute:** data associated with an object or class.
-   **Method:** a function defined inside a class.
-   **Instantiation:** creating an object from a class.
-   **Constructor/initialisation:** `__init__()` is commonly used to
    initialise a newly created instance.

## 9.2 Class and object example

``` python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def display(self):
        print("Name:", self.name)
        print("Marks:", self.marks)

s1 = Student("Rahul", 85)
s1.display()
```

Explanation: - `class Student:` defines a class. - `__init__()`
initialises attributes. - `self` refers to the current instance and is
written explicitly in instance-method definitions. - `self.name` and
`self.marks` are instance attributes. - `s1` is an object of `Student`.

## 9.3 Instance attributes and class attributes

``` python
class Student:
    college = "Fergusson College"  # class attribute

    def __init__(self, name):
        self.name = name            # instance attribute

s1 = Student("Rahul")
s2 = Student("Asha")
print(s1.college, s1.name)
print(s2.college, s2.name)
```

Class attributes are shared through the class unless shadowed; instance
attributes belong to individual objects.

## 9.4 The four commonly taught OOP principles

### Encapsulation

Combines data and methods in a class and controls how an object's state
is accessed. Python uses naming conventions such as `_name` for
non-public use and name-mangling for `__name`; these are not the same as
strict private access in some other languages.

### Inheritance

A class can derive behaviour and attributes from another class.

``` python
class Person:
    def __init__(self, name):
        self.name = name

class Student(Person):
    def study(self):
        print(self.name, "is studying")

s = Student("Rahul")
s.study()
```

### Polymorphism

The same interface or method name can work with objects of different
types.

``` python
class Dog:
    def speak(self):
        print("Bark")

class Cat:
    def speak(self):
        print("Meow")

for animal in (Dog(), Cat()):
    animal.speak()
```

### Abstraction

Shows essential operations while hiding implementation details. Python
supports abstract base classes through the `abc` module.

``` python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

A concrete subclass must implement the abstract method before it can be
instantiated.

## 9.5 Method types

-   **Instance method:** takes `self` and operates on an instance.
-   **Class method:** decorated with `@classmethod`; takes `cls` and
    works with class-level state or alternate constructors.
-   **Static method:** decorated with `@staticmethod`; does not
    automatically receive `self` or `cls`.

``` python
class Example:
    count = 0

    def instance_method(self):
        return "instance"

    @classmethod
    def class_method(cls):
        return cls.count

    @staticmethod
    def add(a, b):
        return a + b
```

## 9.6 Special methods

Special methods (often called dunder methods because of double
underscores) let objects integrate with Python syntax. - `__init__`:
initialise an instance. - `__str__`: user-friendly string
representation. - `__repr__`: developer-oriented representation. -
`__len__`: behaviour for `len(obj)`. - `__add__`: behaviour for `+` in
appropriate classes.

``` python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return self.title

print(Book("Python Basics"))
```

------------------------------------------------------------------------

# 10. Exception Handling

## 10.1 What is an exception?

An exception is an event/error that interrupts the normal flow of a
program. Exception handling allows a program to respond to anticipated
errors rather than terminating unexpectedly.

Examples: - `ZeroDivisionError`: division by zero. - `ValueError`: value
has the right general type but is unsuitable, e.g. `int("abc")`. -
`TypeError`: operation applied to an incompatible type. - `IndexError`:
sequence index out of range. - `KeyError`: dictionary key not found. -
`NameError`: name not defined. - `FileNotFoundError`: requested file
does not exist.

## 10.2 `try` and `except`

``` python
try:
    number = int(input("Enter a number: "))
    print(100 / number)
except ValueError:
    print("Enter a valid integer.")
except ZeroDivisionError:
    print("Number must not be zero.")
```

Put risky operations inside `try`. Use specific exceptions where
possible.

## 10.3 `else` and `finally`

-   `else`: runs if no exception occurs in the `try` block.
-   `finally`: runs whether or not an exception occurs, commonly for
    cleanup.

``` python
try:
    number = int(input("Enter a number: "))
    result = 100 / number
except (ValueError, ZeroDivisionError) as error:
    print("Problem:", error)
else:
    print("Result:", result)
finally:
    print("Execution finished")
```

## 10.4 Raising an exception

Use `raise` when a program detects an invalid condition.

``` python
def check_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age

print(check_age(21))
```

## 10.5 User-defined exceptions

Custom exceptions can represent application-specific errors.

``` python
class InvalidMarksError(Exception):
    pass

def validate_marks(marks):
    if not 0 <= marks <= 100:
        raise InvalidMarksError("Marks must be between 0 and 100")
    return marks
```

## 10.6 Exception-handling best practices

-   Catch specific exceptions instead of using a bare `except`.
-   Do not silently ignore errors.
-   Keep the `try` block limited to operations that may fail.
-   Use `finally` or context managers for resource cleanup.
-   Do not display sensitive internal details to end users.

------------------------------------------------------------------------

# 11. Important Differences

## 11.1 List vs tuple

  -----------------------------------------------------------------------
  List                                Tuple
  ----------------------------------- -----------------------------------
  Written with `[]`                   Written with `()`

  Mutable                             Immutable

  Suitable for collections that       Suitable for fixed collections
  change                              

  Example: `[1, 2, 3]`                Example: `(1, 2, 3)`
  -----------------------------------------------------------------------

## 11.2 Set vs dictionary

-   A **set** stores unique elements: `{1, 2, 3}`.
-   A **dictionary** stores key-value pairs:
    `{"name": "Rahul", "age": 21}`.
-   `{}` creates an empty dictionary; use `set()` for an empty set.

## 11.3 `break` vs `continue` vs `pass`

  Statement    Effect
  ------------ -----------------------------
  `break`      Exits the nearest loop
  `continue`   Skips to the next iteration
  `pass`       Performs no operation

## 11.4 `print()` vs `return`

  -----------------------------------------------------------------------
  `print()`                           `return`
  ----------------------------------- -----------------------------------
  Displays data to output             Sends a value back to the caller

  Does not by itself provide a result Result can be stored or used in an
  to assign                           expression

  Used for display/debugging          Used to communicate a function
                                      result
  -----------------------------------------------------------------------

## 11.5 Parameter vs argument

-   Parameter: name in the function definition, e.g. `name` in
    `def greet(name):`.
-   Argument: value supplied in the call, e.g. `"Rahul"` in
    `greet("Rahul")`.

## 11.6 Module vs package

-   Module: a single Python file.
-   Package: a directory structure that organises related modules
    (modern Python also supports namespace packages).

## 11.7 Class vs object

-   Class: blueprint/type definition.
-   Object: particular instance created from a class.

## 11.8 Syntax error vs exception

-   Syntax error: code does not follow Python grammar and cannot be
    parsed correctly.
-   Exception: an error condition raised during execution, such as
    `ZeroDivisionError`; it may be handled.

------------------------------------------------------------------------

# 12. Practical Programs

## Program 1: Check even or odd

``` python
n = int(input("Enter a number: "))
if n % 2 == 0:
    print("Even")
else:
    print("Odd")
```

## Program 2: Find the largest of three numbers

``` python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))
c = int(input("Enter third number: "))

if a >= b and a >= c:
    largest = a
elif b >= a and b >= c:
    largest = b
else:
    largest = c

print("Largest:", largest)
```

## Program 3: Sum of first `n` natural numbers

``` python
n = int(input("Enter n: "))
total = 0
for i in range(1, n + 1):
    total += i
print("Sum:", total)
```

## Program 4: Factorial using a loop

``` python
n = int(input("Enter a non-negative integer: "))
if n < 0:
    print("Factorial is not defined for negative integers.")
else:
    fact = 1
    for i in range(1, n + 1):
        fact *= i
    print("Factorial:", fact)
```

## Program 5: Reverse a string

``` python
text = input("Enter text: ")
print("Reversed:", text[::-1])
```

## Program 6: Palindrome check

``` python
text = input("Enter text: ").strip().lower()
if text == text[::-1]:
    print("Palindrome")
else:
    print("Not a palindrome")
```

This simple version treats spaces and punctuation as significant.

## Program 7: Count vowels in a string

``` python
text = input("Enter text: ").lower()
count = 0
for ch in text:
    if ch in "aeiou":
        count += 1
print("Vowels:", count)
```

## Program 8: Function to calculate rectangle area

``` python
def calculate_area(length, width):
    return length * width

print(calculate_area(10, 5))  # 50
print(calculate_area(20, 10)) # 200
print(calculate_area(15, 8))  # 120
```

## Program 9: Simple module example

Create `calculator.py`:

``` python
def add(a, b):
    return a + b
```

In another file in the same directory:

``` python
import calculator
print(calculator.add(10, 20))
```

## Program 10: Handle division safely

``` python
try:
    a = float(input("Enter numerator: "))
    b = float(input("Enter denominator: "))
    print("Result:", a / b)
except ValueError:
    print("Please enter numeric values.")
except ZeroDivisionError:
    print("Denominator cannot be zero.")
```

## Program 11: Basic class and object

``` python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def display(self):
        print(f"Name: {self.name}")
        print(f"Marks: {self.marks}")

student1 = Student("Asha", 92)
student1.display()
```

------------------------------------------------------------------------

# 13. Exam and Viva Questions

## Short-answer questions

1.  Define Python and list any five features.
2.  What is the difference between system software and application
    software?
3.  What is an interpreter? Explain Python's execution model briefly.
4.  What is a Python implementation? Name four implementations.
5.  What does `id()` return?
6.  Define variable, object, identity and data type.
7.  List common built-in Python data types with examples.
8.  What is the difference between mutable and immutable objects?
9.  What is the difference between `==` and `is`?
10. Define type conversion and give examples.
11. What is indentation and why is it important in Python?
12. Explain `if`, `if-else` and `if-elif-else`.
13. What is the purpose of `range()`?
14. Differentiate `for` and `while` loops.
15. Explain `break`, `continue` and `pass`.
16. Define a string. Explain indexing and slicing.
17. What does it mean that strings are immutable?
18. Explain any five string methods with examples.
19. Define a function. State its advantages.
20. Differentiate parameters and arguments.
21. Explain positional, keyword and default arguments.
22. Explain `*args` and `**kwargs`.
23. Differentiate `print()` and `return`.
24. What is recursion? What is a base case?
25. Define module, package and library.
26. Explain different ways to import a module.
27. What is the purpose of `if __name__ == "__main__"`?
28. Define class, object, attribute and method.
29. Explain the four principles of OOP.
30. What is the role of `self` and `__init__()`?
31. Define exception handling.
32. Explain `try`, `except`, `else`, `finally` and `raise`.
33. Give examples of five built-in exceptions.

## Long-answer questions

1.  Explain the features and applications of Python.
2.  Explain Python's data types and illustrate mutable and immutable
    objects.
3.  Explain conditional statements and loops with suitable programs.
4.  Explain string indexing, slicing, immutability and commonly used
    string methods.
5.  Define functions and explain the different types of arguments with
    examples.
6.  Explain modules and demonstrate importing a user-defined module.
7.  Explain class and object concepts and the four OOP principles with
    examples.
8.  Explain exception handling with a program using multiple exception
    types.
9.  Compare compiler and interpreter; describe CPython's
    source-to-bytecode execution flow.
10. Write programs for factorial, palindrome, vowel counting and
    largest-of-three.

## Output-prediction practice

Try to predict the output before running each program.

### Question 1

``` python
for i in range(1, 10, 3):
    print(i)
```

**Answer:** `1`, `4`, `7` on separate lines.

### Question 2

``` python
s = "Python"
print(s[1:4])
print(s[-1])
print(s[::-1])
```

**Answer:** `yth`, `n`, `nohtyP`.

### Question 3

``` python
x = [1, 2]
y = x
y.append(3)
print(x)
```

**Answer:** `[1, 2, 3]`, because both names refer to the same list
object.

### Question 4

``` python
def add(a, b):
    return a + b

print(add(4, 6))
```

**Answer:** `10`.

### Question 5

``` python
try:
    print(10 / 0)
except ZeroDivisionError:
    print("Cannot divide by zero")
finally:
    print("Done")
```

**Answer:**

``` text
Cannot divide by zero
Done
```

------------------------------------------------------------------------

# 14. Common Mistakes to Avoid

1.  Writing `=` when comparing values instead of `==`.
2.  Forgetting the colon after `if`, `for`, `while`, `def` or `class`.
3.  Using inconsistent indentation.
4.  Forgetting that `range()` excludes the stop value.
5.  Trying to modify a string character by index.
6.  Forgetting to convert `input()` text before numeric calculations.
7.  Expecting a function to run merely because it has been defined.
8.  Printing a result when it needs to be returned to the caller.
9.  Using `is` instead of `==` for ordinary value comparison.
10. Catching every exception without knowing what error occurred.
11. Forgetting a termination condition or update in a `while` loop.
12. Using mutable default arguments such as `def f(items=[]):` without
    understanding that the same list is reused across calls.

------------------------------------------------------------------------

# 15. Quick Revision Sheet

  Topic                Remember
  -------------------- -------------------------------------------
  Output               `print(value)`
  Input                `input()` returns a string
  Type                 `type(value)`
  Identity             `id(value)`
  Conditional          `if condition:`
  Multiple branches    `if` / `elif` / `else`
  Loop                 `for item in iterable:`
  Integer sequence     `range(start, stop, step)`; stop excluded
  While loop           Repeats while condition is true
  Exit loop            `break`
  Skip iteration       `continue`
  Placeholder          `pass`
  String length        `len(text)`
  String index         `text[0]`; negative index from end
  String slice         `text[start:stop:step]`
  Function             `def name(parameters):`
  Return               `return value`
  Positional extras    `*args` → tuple
  Keyword extras       `**kwargs` → dictionary
  Import               `import math`
  Class                `class Student:`
  Initialisation       `def __init__(self, ...):`
  Instance reference   `self`
  Exception handling   `try` / `except`
  No-error branch      `else` after `try`
  Cleanup branch       `finally`
  Raise error          `raise ValueError("message")`

------------------------------------------------------------------------

## Study strategy

1.  Learn the definitions and comparison tables.
2.  Type and run every code example; do not only read the output.
3.  Practise control-flow and string output questions by hand.
4.  Write one program each for functions, modules, classes and
    exceptions without copying.
5.  Revise the Quick Revision Sheet and answer the viva questions aloud.

**Source scope:** These notes are based on the six supplied PDFs:
*Introduction to Python*, *Data Type in Python & Object*, *Control
Structures and Loops*, *Python Function*, *Strings in Python:
Functions*, and *Python Module, OOP, Exception*. The examples and study
questions are organised for learning and revision; they are not a claim
about the exact exam paper.
