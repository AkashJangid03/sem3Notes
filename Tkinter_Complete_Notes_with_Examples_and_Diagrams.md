# Tkinter GUI Programming --- Complete Notes with Examples and Diagrams

**Course:** Python Programming\
**Sources:** *Tkinter_Detailed_Study_Material.pdf* and
*Tkinter_Calculator_Concept_by_Concept_Study_Material.pdf*\
**Purpose:** Concept-by-concept notes, annotated programs, diagrams,
practical exercises, and exam revision.

> These notes combine the two supplied Tkinter study PDFs. The first PDF
> focuses on a basic window, Label, Button, callbacks, layout managers,
> and the event loop. The second explains a calculator using Entry,
> Frame, arithmetic operations, lambda callbacks, and error handling.

## Contents

1.  GUI and Tkinter introduction
2.  Importing Tkinter
3.  Creating and configuring a window
4.  Widgets and parent containers
5.  Label widget
6.  Entry widget and `get()`
7.  Button widget
8.  Functions and callbacks
9.  `command=function` vs `command=function()`
10. Lambda callbacks
11. Geometry managers: `pack()`, `grid()`, and `place()`
12. Frame widget
13. Updating widgets with `config()`
14. Message boxes
15. Event-driven programming and `mainloop()`
16. Complete calculator program
17. Calculator execution flow and test cases
18. Common mistakes
19. Guided practical exercises
20. Viva and exam questions
21. Quick revision sheet

------------------------------------------------------------------------

# 1. GUI and Tkinter Introduction

## 1.1 What is a GUI?

A **Graphical User Interface (GUI)** allows users to interact with a
program through visual elements such as windows, buttons, labels, text
boxes, and menus instead of entering every command in a terminal.

  GUI element   Purpose
  ------------- ---------------------------------
  Window        Main application area
  Label         Displays text or a result
  Entry         Accepts text input
  Button        Lets the user request an action
  Message box   Displays a popup message
  Frame         Groups related widgets

## 1.2 What is Tkinter?

**Tkinter** is Python's standard library for creating GUI applications.
It provides widgets and methods to build desktop interfaces.

Typical uses include simple calculators, forms, data-entry tools, and
small desktop applications.

## 1.3 How a Tkinter application works

1.  The Python program defines a main window and widgets.
2.  Tkinter creates the GUI elements.
3.  A geometry manager arranges the widgets.
4.  `mainloop()` waits for events such as button clicks.
5.  When the user interacts with the GUI, the associated callback runs.
6.  The program may update a widget or display a message.

``` text
Start Python program
        |
        v
Create main window (Tk)
        |
        v
Create widgets (Label, Entry, Button)
        |
        v
Arrange widgets (pack / grid / place)
        |
        v
Start mainloop()
        |
        v
Wait for user event
        |
        v
Run callback function
        |
        v
Update GUI / show result
        |
        +-------> Wait for next event
```

------------------------------------------------------------------------

# 2. Importing Tkinter

``` python
import tkinter as tk
from tkinter import messagebox
```

-   `import tkinter as tk` imports the Tkinter module and assigns it the
    alias `tk`.
-   `tk.Label(...)` refers to the `Label` class from Tkinter.
-   `from tkinter import messagebox` imports the popup-dialog module so
    that functions such as `messagebox.showerror()` can be called
    directly.

The alias `tk` is a naming convenience. It does not change how Tkinter
works.

------------------------------------------------------------------------

# 3. Creating and Configuring a Window

## 3.1 Basic window program

``` python
import tkinter as tk

root = tk.Tk()
root.title("My First GUI")
root.geometry("400x250")

root.mainloop()
```

## 3.2 Important statements

  -----------------------------------------------------------------------
  Code                                Meaning
  ----------------------------------- -----------------------------------
  `root = tk.Tk()`                    Creates the main application window

  `root.title("My First GUI")`        Sets the title-bar text

  `root.geometry("400x250")`          Requests a width of 400 and height
                                      of 250 pixels

  `root.mainloop()`                   Starts the event loop and keeps the
                                      GUI responsive
  -----------------------------------------------------------------------

`root` is a variable holding a reference to the main window object.

## 3.3 `title()`

``` python
root.title("Student Management System")
```

Sets the text shown in the window title bar. It does not set the text
inside the window body.

## 3.4 `geometry()`

``` python
root.geometry("500x300")
```

The string follows the format `"widthxheight"`. Here, the requested
initial width is 500 pixels and height is 300 pixels.

The `x` is a literal separator, not a multiplication operator.

## 3.5 `resizable()`

The calculator study material uses:

``` python
root.resizable(False, False)
```

This prevents resizing horizontally and vertically. The first argument
controls width resizing; the second controls height resizing. It is
optional.

------------------------------------------------------------------------

# 4. Widgets and Parent Containers

A **widget** is a GUI component such as a Label, Button, or Entry. A
widget is usually created inside a parent container.

Example:

``` python
label = tk.Label(root, text="Welcome")
```

-   `tk.Label(...)` creates the widget.
-   `root` is its parent container.
-   `text="Welcome"` sets its displayed text.
-   `label` stores a reference to the widget so it can be modified
    later.

Creating a widget and arranging it on the screen are separate actions.
For example:

``` python
label = tk.Label(root, text="Welcome")
label.pack()
```

The first statement creates the Label; the second arranges it in the
window.

``` text
root (main window)
 |
 +-- heading Label
 |
 +-- first Entry
 |
 +-- second Entry
 |
 +-- button_frame (Frame)
 |      |
 |      +-- Addition Button
 |      +-- Subtraction Button
 |      +-- Multiplication Button
 |      +-- Division Button
 |
 +-- result Label
```

------------------------------------------------------------------------

# 5. Label Widget

A **Label** displays text or an image. In the supplied examples, Labels
display welcome messages, headings, and calculator results.

## 5.1 Basic syntax

``` python
label = tk.Label(root, text="Welcome to Tkinter!")
label.pack()
```

## 5.2 Label with font and padding

``` python
label = tk.Label(
    root,
    text="Welcome to Python GUI Programming!",
    font=("Arial", 14)
)
label.pack(pady=30)
```

  Option                 Meaning
  ---------------------- --------------------------------------------------------
  `root`                 Parent container
  `text=`                Text to display
  `font=("Arial", 14)`   Font family and size
  `pady=30`              Vertical spacing around the widget when using `pack()`

## 5.3 Store the widget for later updates

``` python
result_label = tk.Label(root, text="Result: ")
result_label.pack()
```

The variable `result_label` lets the program update the existing Label
later:

``` python
result_label.config(text="Result: 15")
```

------------------------------------------------------------------------

# 6. Entry Widget and `get()`

An **Entry** widget provides a single-line text input field. In the
calculator, the user types two numbers into two Entry widgets.

``` python
entry1 = tk.Entry(root, width=25)
entry1.pack(pady=5)

entry2 = tk.Entry(root, width=25)
entry2.pack(pady=5)
```

-   `tk.Entry(root, width=25)` creates an input field in `root`.
-   `width=25` is an approximate character width, not a guaranteed pixel
    width.
-   `pack(pady=5)` arranges the field and adds vertical spacing.

## 6.1 Read input with `get()`

``` python
text_value = entry1.get()
```

`Entry.get()` returns the text entered by the user as a **string**, even
when that text looks numeric.

Example:

``` python
value = entry1.get()
number = float(value)
```

If the user enters `12.5`, `get()` returns `"12.5"` and `float()`
converts it to the number `12.5`.

For whole-number calculations, `int()` can be used. For a calculator
that should support decimal values, `float()` is more suitable.

## 6.2 Why conversion is needed

``` text
Entry field
   |
   v
entry1.get()
   |
   v
String, e.g. "12.5"
   |
   v
float("12.5")
   |
   v
Number 12.5
   |
   v
Arithmetic operation
```

If the field is empty or contains text such as `"hello"`, conversion
raises `ValueError`. The calculator catches this error with
`try/except`.

------------------------------------------------------------------------

# 7. Button Widget

A **Button** is a clickable control. The `command` option connects the
click event to a function.

``` python
def say_hello():
    label.config(text="Hello! Button clicked.")

button = tk.Button(
    root,
    text="Click Me",
    command=say_hello
)
button.pack()
```

  Part                  Meaning
  --------------------- ------------------------------------------
  `tk.Button(...)`      Creates a button
  `root`                Parent container
  `text="Click Me"`     Caption displayed on the button
  `command=say_hello`   Registers a callback to run when clicked
  `button.pack()`       Arranges the button in the parent

A button can be visible without performing a useful action. Its callback
connects the click event to Python behaviour.

------------------------------------------------------------------------

# 8. Functions and Callback Functions

A function is defined using `def`.

``` python
def say_hello():
    label.config(text="Hello! Button clicked.")
```

The indented body runs when the function is called.

A **callback** is a function passed to another part of a program so that
it can be called later when an event occurs. In Tkinter, the `command`
option commonly registers a button callback.

## 8.1 Function reference vs function call

  -----------------------------------------------------------------------
  Expression                          Behaviour
  ----------------------------------- -----------------------------------
  `command=say_hello`                 Passes the function reference;
                                      Tkinter calls it later on a click

  `command=say_hello()`               Calls the function immediately
                                      during widget setup; its return
                                      value is assigned to `command`
  -----------------------------------------------------------------------

For an ordinary button callback that takes no arguments, use:

``` python
command=say_hello
```

Do not add parentheses unless immediate execution is intentional.

------------------------------------------------------------------------

# 9. Lambda Callbacks and Arguments

The calculator's function accepts an operator:

``` python
def calculate(operator):
    print("Selected operator:", operator)
```

A Button must pass `"+"`, `"-"`, `"*"`, or `"/"` to this function when
clicked. A lambda can defer the call and supply the argument.

``` python
button = tk.Button(
    root,
    text="Addition",
    command=lambda: calculate("+")
)
```

## 9.1 Why use `lambda`?

-   `calculate(operator)` requires an argument.
-   `command=calculate("+")` calls the function immediately while the
    button is being created.
-   `command=calculate` passes the function itself but does not provide
    the operator.
-   `command=lambda: calculate("+")` creates a small function that calls
    `calculate("+")` when the button is clicked.

``` text
Button created
     |
     v
lambda callback registered
     |
     v
User clicks button
     |
     v
calculate("+") runs
```

------------------------------------------------------------------------

# 10. Geometry Managers: `pack()`, `grid()`, and `place()`

A **geometry manager** controls where and how a widget is arranged
inside its parent container.

## 10.1 `pack()`

`pack()` arranges widgets relative to available space and other packed
widgets.

``` python
label.pack()
label.pack(pady=20)
button.pack(side="left")
button.pack(side="right")
button.pack(side="bottom")
```

-   `pady` adds vertical spacing.
-   `padx` adds horizontal spacing.
-   `side` controls which side of the available area is used.

Typical use: simple vertical or horizontal layouts.

## 10.2 `grid()`

`grid()` arranges widgets in rows and columns. Row and column numbering
begins at zero.

``` python
button1.grid(row=0, column=0, padx=5, pady=5)
button2.grid(row=0, column=1, padx=5, pady=5)
button3.grid(row=1, column=0, padx=5, pady=5)
button4.grid(row=1, column=1, padx=5, pady=5)
```

Diagram:

``` text
                 column=0             column=1
row=0        [Addition (+)]       [Subtraction (-)]
row=1        [Multiplication (*)] [Division (/)]
```

-   `row=0`: first row.
-   `column=1`: second column.
-   `padx=5`: horizontal spacing.
-   `pady=5`: vertical spacing.

Typical use: forms and calculator buttons that must line up.

## 10.3 `place()`

`place()` positions widgets using coordinates relative to their parent.

``` python
button.place(x=100, y=100)
```

This places the widget at the specified coordinate location. It is
coordinate-based rather than arranging widgets in relation to available
space.

## 10.4 Comparison

  Manager     Layout                                  Typical use
  ----------- --------------------------------------- ----------------------
  `pack()`    Relative to available space and sides   Simple layouts
  `grid()`    Rows and columns                        Forms, calculators
  `place()`   Coordinates or relative positions       Specific positioning

**Important:** Do not use `pack()` and `grid()` to manage widgets inside
the same parent container. Different nested containers may use different
managers. In the calculator, `pack()` arranges `button_frame` inside
`root`, while `grid()` arranges buttons inside `button_frame`. This is
valid because the parent containers differ.

------------------------------------------------------------------------

# 11. Frame Widget

A **Frame** is a container that groups and organises other widgets.

``` python
button_frame = tk.Frame(root)
button_frame.pack(pady=10)
```

Create the buttons with `button_frame` as their parent:

``` python
tk.Button(
    button_frame,
    text="Addition (+)",
    command=lambda: calculate("+")
).grid(row=0, column=0, padx=5, pady=5)
```

Why use a Frame?

1.  It groups related widgets.
2.  It makes the layout easier to organise.
3.  The Frame can be positioned in the main window with one geometry
    manager.
4.  Its child widgets can be arranged separately inside the Frame.

------------------------------------------------------------------------

# 12. Updating Widgets with `config()`

`config()` changes the properties of an existing widget. It does not
create a new widget.

``` python
label.config(text="Hello! Button clicked.")
```

Calculator example:

``` python
result_label.config(text=f"Result: {result}")
```

The `f` before the string enables an **f-string**. Expressions inside
`{}` are evaluated and inserted into the string. If `result` is `15.0`,
the label displays `Result: 15.0`.

------------------------------------------------------------------------

# 13. Message Boxes

The calculator imports the module:

``` python
from tkinter import messagebox
```

Useful methods from the supplied calculator material:

  ------------------------------------------------------------------------------
  Method                                     Purpose
  ------------------------------------------ -----------------------------------
  `messagebox.showerror(title, message)`     Displays an error popup

  `messagebox.showwarning(title, message)`   Displays a warning popup

  `messagebox.showinfo(title, message)`      Displays an information popup

  `messagebox.askyesno(title, question)`     Asks a Yes/No question and returns
                                             a Boolean
  ------------------------------------------------------------------------------

Example:

``` python
messagebox.showerror(
    "Input Error",
    "Please enter valid numbers in both fields."
)
```

Use an error message to explain what went wrong and what the user should
do next.

------------------------------------------------------------------------

# 14. Conditional Statements in the Calculator

The `calculate()` function uses `if` and `elif` to select the arithmetic
operation.

``` python
if operator == "+":
    result = num1 + num2
elif operator == "-":
    result = num1 - num2
elif operator == "*":
    result = num1 * num2
elif operator == "/":
    result = num1 / num2
```

-   `if` checks the first condition.
-   `elif` checks another condition if earlier conditions were false.
-   `==` compares two values for equality.
-   Indentation determines which statements belong to each branch.

The supplied calculator adds a zero check before division:

``` python
if num2 == 0:
    messagebox.showerror(
        "Calculation Error",
        "Cannot divide by zero!"
    )
    return

result = num1 / num2
```

`return` exits the function immediately after showing the error. This
prevents the division and result update from continuing.

------------------------------------------------------------------------

# 15. Error Handling with `try` and `except`

Input conversion may fail if a field is empty or contains non-numeric
text.

``` python
try:
    num1 = float(entry1.get())
    num2 = float(entry2.get())
except ValueError:
    messagebox.showerror(
        "Input Error",
        "Please enter valid numbers in both fields."
    )
```

-   `try` contains code that may raise a particular error.
-   `except ValueError` catches invalid numeric conversion.
-   The message box informs the user rather than allowing an uncaught
    error to stop the program.

The supplied calculator handles both invalid numeric input and division
by zero.

------------------------------------------------------------------------

# 16. Event-Driven Programming and `mainloop()`

Tkinter applications are **event-driven**. The program waits for actions
such as mouse clicks, keyboard input, window resizing, or closing the
window.

``` python
root.mainloop()
```

`mainloop()` starts Tkinter's event loop. It keeps the window
responsive, handles user input, and redraws widgets.

Without `mainloop()`, the program generally reaches its end without
keeping the GUI open and responsive.

``` text
mainloop()
    |
    v
Wait for event
    |
    +-- Button click --> Run callback --> Update result
    |
    +-- Keyboard input --> Process input
    |
    +-- Window close --> Handle close request
    |
    +-- Wait for next event
```

It is normally placed at the end of the script.

------------------------------------------------------------------------

# 17. Complete Calculator Program

This program combines the concepts from both supplied PDFs: the main
window, Label, Entry, Frame, Button, geometry managers, callbacks,
lambda, conditional statements, `config()`, message boxes, and exception
handling.

``` python
import tkinter as tk
from tkinter import messagebox


def calculate(operator):
    try:
        # Entry.get() returns strings, so convert to numbers.
        num1 = float(entry1.get())
        num2 = float(entry2.get())

        if operator == "+":
            result = num1 + num2

        elif operator == "-":
            result = num1 - num2

        elif operator == "*":
            result = num1 * num2

        elif operator == "/":
            if num2 == 0:
                messagebox.showerror(
                    "Calculation Error",
                    "Cannot divide by zero!"
                )
                return

            result = num1 / num2

        else:
            messagebox.showerror(
                "Operation Error",
                "Unsupported operation."
            )
            return

        result_label.config(text=f"Result: {result}")

    except ValueError:
        messagebox.showerror(
            "Input Error",
            "Please enter valid numbers in both fields."
        )


# Create and configure the main window.
root = tk.Tk()
root.title("Simple Calculator")
root.geometry("380x320")
root.resizable(False, False)

# Heading label.
heading = tk.Label(
    root,
    text="SIMPLE CALCULATOR",
    font=("Arial", 16, "bold")
)
heading.pack(pady=15)

# Input fields.
tk.Label(root, text="First Number:").pack()
entry1 = tk.Entry(root, width=25)
entry1.pack(pady=5)

tk.Label(root, text="Second Number:").pack()
entry2 = tk.Entry(root, width=25)
entry2.pack(pady=5)

# Frame groups the operation buttons.
button_frame = tk.Frame(root)
button_frame.pack(pady=10)

tk.Button(
    button_frame,
    text="Addition (+)",
    width=12,
    command=lambda: calculate("+")
).grid(row=0, column=0, padx=5, pady=5)

tk.Button(
    button_frame,
    text="Subtraction (-)",
    width=12,
    command=lambda: calculate("-")
).grid(row=0, column=1, padx=5, pady=5)

tk.Button(
    button_frame,
    text="Multiplication (*)",
    width=12,
    command=lambda: calculate("*")
).grid(row=1, column=0, padx=5, pady=5)

tk.Button(
    button_frame,
    text="Division (/)",
    width=12,
    command=lambda: calculate("/")
).grid(row=1, column=1, padx=5, pady=5)

# Result display.
result_label = tk.Label(
    root,
    text="Result: ",
    font=("Arial", 12, "bold")
)
result_label.pack(pady=5)

# Start processing GUI events.
root.mainloop()
```

## 17.1 Calculator execution flow

``` text
User enters first and second numbers
                 |
                 v
       Clicks operation button
                 |
                 v
   lambda calls calculate(operator)
                 |
                 v
     entry1.get() and entry2.get()
                 |
                 v
        Convert strings to float
                 |
          +------+------+
          |             |
          v             v
     Invalid input   Valid input
          |             |
          v             v
    ValueError       Check operator
          |             |
          v             v
    Error popup    Perform arithmetic
                        |
                  +-----+-----+
                  |           |
                  v           v
              Divide by 0   Valid result
                  |           |
                  v           v
              Error popup  result_label.config()
```

## 17.2 Sample test cases

    First number   Second number Operation   Expected outcome
  -------------- --------------- ----------- --------------------------------------
              12               3 `+`         `Result: 15.0`
              12               3 `-`         `Result: 9.0`
              12               3 `*`         `Result: 36.0`
              12               3 `/`         `Result: 4.0`
              12               0 `/`         Error popup: cannot divide by zero
           `abc`               3 `+`         Error popup asking for valid numbers
           Empty               3 `+`         Error popup asking for valid numbers

------------------------------------------------------------------------

# 18. Common Beginner Mistakes

1.  **Forgetting the import:** use `import tkinter as tk` before calling
    `tk.Tk()`, `tk.Label()`, or `tk.Button()`.
2.  **Forgetting parentheses:** `root = tk.Tk()` creates the window.
3.  **Creating but not arranging a widget:** a widget normally needs a
    geometry manager such as `pack()`, `grid()`, or `place()`.
4.  **Calling a callback immediately:** use `command=say_hello`, not
    `command=say_hello()`, for a normal no-argument button callback.
5.  **Forgetting `get()`:** `entry1` is a widget; `entry1.get()`
    retrieves the entered text.
6.  **Skipping numeric conversion:** `Entry.get()` returns a string; use
    `float()` or `int()` before numeric arithmetic.
7.  **Using `grid()` and `pack()` inside the same parent:** use one
    geometry manager per parent container.
8.  **Forgetting `mainloop()`:** the GUI may not remain open and
    responsive.
9.  **Not checking division by zero:** check the divisor before
    division.
10. **Incorrect indentation:** Python uses indentation to define
    function bodies, conditions, and exception handlers.
11. **Updating a widget before it exists:** ensure the variable refers
    to a created widget before calling `config()`.
12. **Using a callback argument incorrectly:** use `lambda` when the
    callback needs an argument such as an operator.

------------------------------------------------------------------------

# 19. Guided Practical Exercises

## Exercise 1: Change the window

Set the title to `"M.Sc. Computer Applications"` and the size to
`"500x300"`.

## Exercise 2: Change the Label

Display a welcome message using:

``` python
font=("Arial", 14)
```

## Exercise 3: Add a button response

Create a button that changes a Label to:

``` text
Button clicked successfully!
```

## Exercise 4: Compare geometry managers

Try:

``` python
widget.pack(side="left")
widget.pack(side="bottom")
widget.place(x=100, y=100)
```

Observe the difference. Do not use these calls simultaneously on the
same widget as a meaningful layout strategy; test one arrangement at a
time.

## Exercise 5: Add a Clear button to the calculator

Hint:

``` python
def clear_fields():
    entry1.delete(0, tk.END)
    entry2.delete(0, tk.END)
    result_label.config(text="Result: ")
```

Create a button with `command=clear_fields`.

## Exercise 6: Round the result

Change the result display to show two decimal places:

``` python
result_label.config(text=f"Result: {result:.2f}")
```

## Exercise 7: Add an information popup

After a successful calculation, use `messagebox.showinfo()` to display a
completion message.

## Exercise 8: Extend the calculator

Add an operation or a third input field. Identify which parts of the
input-reading and calculation logic must change.

------------------------------------------------------------------------

# 20. Viva and Exam Questions

## Short-answer questions

1.  What is Tkinter?
2.  What is a GUI? Give examples of GUI components.
3.  What does `import tkinter as tk` mean?
4.  What does `root = tk.Tk()` do?
5.  Explain `title()` and `geometry()`.
6.  What is the purpose of `resizable(False, False)`?
7.  What is a widget? Give four examples.
8.  What is the difference between a Label and an Entry?
9.  Why is a widget variable stored?
10. What is the purpose of `Entry.get()`?
11. Why is `float()` used in the calculator?
12. What is a callback function?
13. Differentiate `command=say_hello` and `command=say_hello()`.
14. What is the purpose of `lambda` in the calculator?
15. Compare `pack()`, `grid()`, and `place()`.
16. What is a Frame, and why is it useful?
17. What does `config()` do?
18. What is the purpose of `messagebox.showerror()`?
19. Why is `try/except ValueError` used?
20. Why must a calculator check for division by zero?
21. What does `return` do after the division-by-zero message?
22. What is an f-string?
23. What do `row`, `column`, `padx`, and `pady` mean?
24. What is event-driven programming?
25. What does `root.mainloop()` do?

## Long-answer / practical questions

1.  Explain Tkinter and the steps involved in creating a GUI
    application.
2.  Write and explain a program to create a window with a Label and
    Button.
3.  Explain the `Label`, `Entry`, `Button`, and `Frame` widgets with
    examples.
4.  Compare `pack()`, `grid()`, and `place()` with examples.
5.  Explain callbacks and the difference between a function reference
    and function call.
6.  Explain lambda callbacks with a calculator example.
7.  Write a simple calculator using Tkinter.
8.  Explain how the calculator handles invalid input and division by
    zero.
9.  Explain the role of `mainloop()` in an event-driven application.
10. Explain how `config()` updates an existing widget.

------------------------------------------------------------------------

# 21. Quick Revision Sheet

  -----------------------------------------------------------------------
  Concept                             Remember
  ----------------------------------- -----------------------------------
  Tkinter                             Python standard library for GUI
                                      applications

  `tk.Tk()`                           Creates the main window

  `root`                              Variable referring to the window
                                      object

  `title()`                           Sets title-bar text

  `geometry("400x250")`               Requests initial width and height

  `resizable(False, False)`           Prevents horizontal and vertical
                                      resizing

  Widget                              GUI component such as Label, Entry,
                                      or Button

  `Label`                             Displays text or an image

  `Entry`                             Accepts single-line text input

  `Entry.get()`                       Retrieves input as a string

  `Button`                            Clickable control

  `command=`                          Registers a callback

  `lambda`                            Creates a delayed callback that can
                                      pass arguments

  `Frame`                             Groups widgets in a container

  `pack()`                            Arranges widgets relative to
                                      available space

  `grid()`                            Arranges widgets in rows and
                                      columns

  `place()`                           Positions widgets using coordinates

  `config()`                          Changes properties of an existing
                                      widget

  `messagebox.showerror()`            Displays an error popup

  `float()`                           Converts numeric text to a
                                      floating-point value

  `try/except ValueError`             Handles invalid numeric input

  `return`                            Exits the current function

  `mainloop()`                        Processes GUI events and keeps the
                                      window responsive
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Source alignment

These notes combine the two supplied PDFs: - **Tkinter Detailed Study
Material:** basic GUI, main window, Label, Button, layout managers,
callbacks, `config()`, `mainloop()`, beginner mistakes, and guided
exercises. - **Tkinter Calculator Concept-by-Concept Study Material:**
`Entry`, `Frame`, `messagebox`, numeric conversion, `if/elif`, lambda
callbacks, exception handling, division-by-zero protection, calculator
program, test cases, and calculator-specific review questions.

The calculator program is presented as a complete runnable teaching
example, following the concepts and structure in the supplied material.
