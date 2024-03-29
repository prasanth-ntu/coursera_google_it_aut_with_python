# Notes

- [Notes](#notes)
- [Notes: Week 1](#notes-week-1)
  - [A Note on Syntax and Code Blocks](#a-note-on-syntax-and-code-blocks)
  - [Functions and Keywords](#functions-and-keywords)
- [Notes: Week 2](#notes-week-2)
  - [Building blocks of python syntax](#building-blocks-of-python-syntax)
  - [Implicit vs. explicit conversion](#implicit-vs-explicit-conversion)
  - [Functions](#functions)
  - [Code style](#code-style)
- [Notes: Week 3](#notes-week-3)
  - [Recursion](#recursion)
- [Notes: Week 4](#notes-week-4)
  - [Methods](#methods)
    - [string `format`](#string-format)
  - [Lists](#lists)
    - [List comprehension](#list-comprehension)
- [Notes: Week 5](#notes-week-5)
  - [OOP](#oop)
  - [Classes and Methods](#classes-and-methods)
  - [Code Reuse](#code-reuse)
- [Notes: Week 6](#notes-week-6)
  - [Writing a Script from Ground Up](#writing-a-script-from-ground-up)
  - [Final Project](#final-project)
- [To clarify](#to-clarify)

# Notes: Week 1
## A Note on Syntax and Code Blocks
When writing code, using correct syntax is super important. Even a small typo, like a missing parentheses or an extra comma, can cause a syntax error and the code won't execute at all. Yikes. If your code results in an error or an exception, pay close attention to syntax and watch out for minor mistakes.

If your **syntax** is correct, but the script has unexpected behavior or output, this may be due to a semantic problem. Remember that syntax is the rules of how code is constructed, while **semantics** are the overall effect the code has. It is possible to have syntactically correct code that runs successfully, but doesn't do what we want it to do.

When working with the code blocks in exercises for this course, be mindful of syntax errors, along with the overall result of your code. Just because you fixed a syntax error doesn't mean that the code will have the desired effect when it runs! Once you’ve fixed an error in your code, don't forget to submit it to have your work checked.

## Functions and Keywords
Functions and keywords are the building blocks of a language’s syntax.

Functions are pieces of code that perform a unit of work (e.g., `print`).

Keywords are reserved words that are used to construct instructions (e.g., `for`).

# Notes: Week 2
## Building blocks of python syntax
- Variables
  - Used to store values 
- Expressions
  - Combination of numbers, symbols or other variables that produce a reslt when evaluated
- Functions
- Conditional blocks

## Implicit vs. explicit conversion
- Implicit: Interpreter automatically converts one data type into another
- Explicit: Manually convert between one data type and another by calling relevant function

## Functions
- `None` is a special data type in Python used to indicate that things are empty or that they returned nothing

## Code style
- Self documented (Else, we need to refactor it)
- Explanatory Text (Comment in python)
  
# Notes: Week 3
## Recursion
- 2 components: Base case and Recursive case
- In some languages, there will usually be a limit on how many times we can call a recursive funciton recursively
  - In Python, we can call a recursive function 1000 times

# Notes: Week 4
## Methods
A function that applies to a specific class. Let's look at an example
 ```
  fruit = 'apple'
  fruit.index('p') # Returns 1
  fruit.index('le') # Returns 3
  ```

### string `format` 
- `format` method automatically handles any conversion between data types
 
```
>>> name = 'Batman'
>>> number = len(name)
>>> print('{} has {} letters in it'.format(name, number))
Batman has 6 letters in it
>>> print('{name} has {no} letters in it'.format(name=name, no=number))
Batman has 6 letters in it
>>> print('{name} has {no} letters in it, wohoo {name}!'.format(name=name, no=number))
Batman has 6 letters in it, wohoo Batman!
```

`{:>.2f}`
- `:` to separate it from the field name if we have specified one
- `>` aligns text to the right
- `.2` means 2 digits after deicmal .
- `f` means float number

```
>>> print ('{:>10.2f} value formatted'.format(pi))
      3.14 value formatted
>>> print ('{:<10.2f} value formatted'.format(pi))
3.14       value formatted

```
*For more details, refer the files in the corresponding folder.*

## Lists
- In python, `string` and `list` are both examples of sequences of data. There are other sequences too, which share bunch of similar operations, such as
  - Iterating over for loops
  - Indexing
  - `len` function
  - `+` to concatenate 2 elements
  - `in` to verify the presence of element inside the sequences. 

### List comprehension
*For more details, refer the files in the corresponding folder.*

<br>

# Notes: Week 5
## OOP
In OOP, concepts are modelled as classes and objects.
- **Classes** represents and define concepts/ideas, **objects** are instances of classes
- Almost everything we have seen so far in Python is an object, including
  - Numbers (`int`, `float`)
  - Lists (`list`)
  - Strings (`str`)
  - Dictionaries (`dict`)
## Classes and Methods
- Classes also have attributes and methods associated with it: 
  - **Attributes**: Characteristics associated to a type/class
  - **Methods**: Functions associated to a type/class, that operates on the attributes of a specific (and single) instance of a class
- **Instance variables**: Variables that have different values for different instances of the same class.
- Some of the Special methods of a Class
  - `__init__()` - Constructor method
  - `__str__()`
- **Doc string**: a short text explanation of what something does. Can be added to a method, function, or class 

## Code Reuse
- **Inheritance**:  Lets you reuse code written for one class in other classes.
- **Composition**: You can have a situation where two different classes are related, but there is no inheritance going on. This is referred to as composition -- where one class makes use of code contained in another class.
  > Always initialize the mutable attributes in the constructor (and not on  class level)
- **Modules**: Used to organize functions, classes, and other data together in a structured way
    
The official [Python documentation](https://docs.python.org/3/) lists all the modules included in the standard library. It even has a turtle in it. 

Pypi is the Python repository and index of an impressive number of modules developed by Python programmers around the world. [Pypi](https://pypi.org/) is the Python repository and index of an impressive number of modules developed by Python programmers around the world. 

*For more details, refer the files in the corresponding folder.*

# Notes: Week 6
## Writing a Script from Ground Up
- Few stages
  - Problem statement
  - Research
  - Planning/Approach
  - Writing the Script
  - Putting it all together

```
names = ['Charles', 'Alex', 'Kelly', 'Ray']
sorted(names) # ['Alex', 'Charles', 'Kelly', 'Ray']
sorted (names, key=len) # ['Ray', 'Alex', 'Kelly', 'Charles']
```

## Final Project
> A journey of 1000 miles starts with a single step!

----

# To clarify
- Does break work only on the inner most loop or all the outer loops as well?
- `self` in `class` methods
  -  These instance methods (methods defined inside the class) can take a parameter called `self`  which represents the instance the method is being executed on.
  -  > `self` represents the instance