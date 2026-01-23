---
marp: true
theme: default
class: invert
---

# Variables and assignments

**variable** - In a program, a variable is a named item, such as x or num_people, that holds a value.

**assignment statement** - An assignment statement assigns a variable with a value, such as x = 5.

**incrementing** - Increasing a variable's value by 1, as in x = x + 1, is common and known as incrementing the variable.

---
# Identifiers

**identifier / name / underscores** - is a sequence of letters (a-z, A-Z), underscores (_), and digits (0–9), and must start with a letter or an underscore.

**case sensitive** - Python is case sensitive, meaning uppercase and lowercase letters differ. Ex: "Cat" and "cat" are different.

**Reserved words / keywords** - words that are part of the language and cannot be used as a programmer-defined name.

**PEP 8 (Python Enhancement Proposal)** - outlines the basics of how to write Python code neatly and consistently.

---
# Objects

**object** - represents a value and is automatically created by the interpreter when executing a line of code. For example, executing x = 4 creates a new object to represent the value 4.

**garbage collection** - Deleting unused objects is an automatic process called garbage collection that frees memory space.

**Name binding** - is the process of associating names with interpreter objects. An object can have more than one name bound to it, and every name is always bound to exactly one object. Name binding occurs whenever an assignment statement is executed, as demonstrated below.

---
# Object - Properties of objects

**Value** - Value: A value such as "20", "abcdef", or "55".

**Type** - Type: The type of the object, such as integer or string.

**Identity** - Identity: A unique identifier that describes the object.

**type()** - The built-in function type() returns the type of an object.

**Mutability** - Mutability indicates whether the object's value is allowed to be changed.

**immutable** - Integers and strings are immutable; meaning integer and string values cannot be changed.

**id** - Python provides a built-in function id() that gives the value of an object's identity.

---
# Numeric types: Floating-point

**floating-point number** - A floating-point number is a real number, like 98.6, 0.0001, or -666.667.

**float** - Thus, float is a data type for floating-point numbers.

**floating-point literal** - A floating-point literal is written with the fractional part even if that fraction is 0, as in 1.0, 0.0, or 99.0.

**scientific notation** - A floating-point literal using scientific notation is written using an "e" preceding the power-of-10 exponent, as in 6.02e23 to represent 6.02x10<sup>23</sup>.

---
# Numeric types: Floating-point - Overflow

**OverflowError** - Assigning a floating-point value outside of this range generates an OverflowError.

**Overflow** - Overflow occurs when a value is too large to be stored in the memory allocated by the interpreter.

---
# Arithmetic expressions

**expression** - An expression is a combination of items, like variables, literals, operators, and parentheses, that evaluates to a value, like 2 * (x + 1).

**literal** - A literal is a specific value in code like 2.

**operator** - An operator is a symbol that performs a built-in calculation, like +, which performs addition.

**evaluates** - An expression evaluates to a value, which replaces the expression. Ex: If x is 5, then x + 1 evaluates to 6, and y = x + 1 assigns y with 6.

**precedence rules** - An expression is evaluated using the order of standard mathematics, and is also known in programming as precedence rules.

---
# Python expressions

**unary minus** - Minus (-) used as negative is known as unary minus.

**compound operators / += / -= / *= / /= / %=** - Special operators called compound operators provide a shorthand way to update a variable, such as age += 1 being shorthand for age = age + 1. Other compound operators include -=, *=, /=, and %=.

---
# Division and modulo
**Division: Integer rounding** 
The division operator / performs division and returns a floating-point number. Ex: 7 / 2 is 3.5

The floor division operator // can be used to round down the result of a floating-point division to the closest smaller whole number value. Ex: 7 // 2 is 3


**modulo operator / %** - The modulo operator (%) evaluates the remainder of the division of two integer operands. Ex: 23 % 10 is 3

---

# Module basics

**script** - Programmers typically write Python program code in a file called a script.

**module** - A module is a file containing Python code that can be used by other modules or scripts.

**import** - A module is made available for use via the import statement.

**dot notation** - Once a module is imported, any object defined in that module can be accessed using dot notation.

**__name__** - Python programs often use the built-in special name __name__ to determine if the file was executed as a script by the programmer or imported by another module.

---
# Math Module

**math module** - Python comes with a standard math module to support such advanced math operations.

**module** - A module is Python code located in another file.

**function** - A function is a list of statements that can be executed simply by referring to the function's name.

**function call** - The process of invoking a function is referred to as a function call.

**argument** - The item passed to a function is referred to as an argument.

--- 
# Random Numbers

**random** - The random module, in the Python Standard Library, provides methods that return random values.

**random()** - The random() method returns a random floating-point value each time the function is called, in the range 0 (inclusive) to 1 (exclusive).

**randrange()** - Python's randrange() method generates random integers within a specified range.

**seed** - For the first call to any random method, no previous random number exists, so the method uses a built-in integer based on the current time, called a seed, to help generate a random number.

---
# Representing Text
**Unicode / code point** - Python uses Unicode to represent every possible character as a unique number, known as a code point.

**newline** - A newline character, which indicates the end of a line of text, is encoded as 10.

**backslash** - The \ is known as a backslash.

**escape sequence** - The two-item sequence is called an escape sequence.

**ord()** - The built-in function ord() returns an encoded integer value for a string of length one.

**chr()** - The built-in function chr() returns a string of one character for an encoded integer.