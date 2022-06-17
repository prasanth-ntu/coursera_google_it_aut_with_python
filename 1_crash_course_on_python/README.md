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
- Funcitons
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
- 
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
- `:` to separate it from the field name if we hav specified one
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

# To clarify
- Does break work only on the inner most loop or all the outer loops as well?
- 