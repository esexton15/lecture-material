---
marp: true
theme: gaia
# class: invert
paginate: true
---

<style>
h1 {
	font-size: 2.5em;
	height: 100%;
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>

# SDEV140 Lecture 4 - Python Basics: Sequence Types

---

# String Basics

---

## Strings and string literals

- **string** - A string is a sequence of characters that represents textual data like a person's name, a location, or a message to the user.
- **string literal** - A string literal is a string defined in the source code of a program by surrounding the text value with single or double quotes, like 'MARY' or "MARY".
- **sequence type** - Sequence type: a type that orders a collection of objects into a sequence from first to last.

---

## Finding the length of a string

- **len()** - The len() built-in function can be used to find the length of a string (and any other sequence type like a list).

```py
name = "MARY"
length = len(name)
print(length)  # Output: 4
```

---

## String indexing

- brackets
  A programmer can reference a character at a specific index by appending brackets [ ] containing the desired index after the name of a string variable.

```py
name = "MARY"
first_letter = name[0]
last_letter = name[3]
print(first_letter) # Output: M
print(last_letter)  # Output: Y
```

---

## Changing string variables

Strings are immutable objects and a string variable cannot change once created.

```py
name = "MARY"
name[0] = "J"  # This will raise an error
```

**Correct Way**
Create a new string and reassign the variable.

```py
name = "MARY"
name = "JARY"   # Create a new string and reassign the variable
```

---

## Concatenating strings

- **string concatenation** - A program can add new characters to the end of a string in a process known as string concatenation.
- String concatenation **does not contradict the immutability** of strings because the **result of concatenation is a new string**; the original strings are not altered.

```py
first_name = "MARY"
last_name = "SMITH"
full_name = first_name + " " + last_name
print(full_name)  # Output: MARY SMITH
```

---

## Formatted string literals (f-strings)

- **formatted string literal / f-string** - A formatted string literal, or f-string, allows a programmer to create a string with placeholder expressions that are evaluated as the program executes.
- **replacement field** - A placeholder expression is also called a replacement field, as its value replaces the expression in the final output.

```py
number = 6
amount = 32

print(f"{number} burritos cost ${amount}.") # Output: 6 burritos cost $32.
```

---

## Format Specification and Presentation Type

- **format specification** - A format specification inside a replacement field allows a value's formatting in the string to be customized.
- **presentation type** - A presentation type is part of a format specification that determines how to represent a value in text form, such as an integer (4), a floating point (4.0), a fixed precision decimal (4.000), a percentage (4%), a binary (100), etc.

```py
number = 6
amount = 32.4567

print(f"{number} burritos cost ${amount:.2f}.") # Output: 6 burritos cost $32.46.
```

---

## Common Format Specifiers

| Format Specifier | Description                        | Example  |
| ---------------- | ---------------------------------- | -------- |
| s                | String                             | "Hello"  |
| d                | Decimal Integer                    | 42       |
| 0[n]d            | Decimal Integer with leading zeros | 0042     |
| b                | Binary representation              | 101010   |
| x,X              | Hexadecimal representation         | 2a, 2A   |
| f                | Fixed Point (six decimal places)   | 3.141593 |
| .[n]f            | Fixed Point (n decimal places)     | 3.14     |

---

# List Basics

---

## Creating a List

- **container** - A container is a construct used to group related values together and contains references to other objects instead of data.
- **list** - A list is a container created by surrounding a sequence of variables or literals with brackets [ ].
- **element** - A list item is called an element.
- **index** - Elements are ordered by position in the list, known as the element's index, starting with 0.

```py
fruits = ["apple", "banana", "cherry"]
print(fruits)  # Output: ['apple', 'banana', 'cherry']
```

---

## Accessing List Elements

Elements in a list can be accessed using their index inside brackets [ ] appended to the list variable name.

```py
fruits = ["apple", "banana", "cherry"]
first_fruit = fruits[0]
second_fruit = fruits[1]
print(first_fruit)   # Output: apple
print(second_fruit)  # Output: banana
```

---

## Updating List Elements

Lists are mutable, meaning that a programmer can change a list's contents. An element can be updated with a new value by performing an assignment to a position in the list.

```py
fruits = ["apple", "banana", "cherry"]
print( fruits )  # Output: ['apple', 'banana', 'cherry']
fruits[1] = "blueberry"
print(fruits)  # Output: ['apple', 'blueberry', 'cherry']
```

---

## Adding List Elements

- **method** - A method instructs an object to perform some action and is specified by providing the object name followed by a "." symbol and then the method name.
- **append()** - The append() list method is used to add new elements to a list.

```py
fruits = ["apple", "banana", "cherry"]
fruits.append("date")
print(fruits)  # Output: ['apple', 'banana', 'cherry', 'date']
```

---

## Removing List Elements

- **list.pop(i)** - Removes the element at index i from list.
- **list.remove(v)** - Removes the first element whose value matches v.

```py
fruits = ["apple", "banana", "cherry"]
fruits.pop(1)  # Removes "banana"
print(fruits)  # Output: ['apple', 'cherry']
fruits.remove("apple")  # Removes "apple"
print(fruits)  # Output: ['cherry']
```

---

## Sequence-type methods and functions

- **Sequence-type methods** - Sequence-type methods are functions built into the Python language definitions of sequence types like lists and strings.
- **Sequence-type functions** - Sequence-type functions are functions built into the Python language that take sequences like lists or strings as arguments and operate on the given sequences.

---

## Sequence-type methods and functions

| Operation     | Description                                  |
| ------------- | -------------------------------------------- |
| len(s)        | Returns the length of s                      |
| list1 + list2 | Concatenates two lists                       |
| min(list)     | Returns the smallest element                 |
| max(list)     | Returns the largest element                  |
| sum(list)     | Returns the sum of elements                  |
| list.index(v) | Returns the index of value v                 |
| list.count(v) | Returns the number of occurrences of value v |

---

## List Example Problem

What is the output of the following code?

```py
numbers = [10, 20, 30, 40, 50]
numbers.append(60)
numbers[2] = 35
numbers.pop(0)
numbers.remove(40)
print(numbers)
```

---

## List Example Problem - Solution

The output of the code will be: `[20, 35, 50, 60]`

**Here's the step-by-step breakdown:**

1. Start with the initial list: `[10, 20, 30, 40, 50]`
2. After `numbers.append(60)`: `[10, 20, 30, 40, 50, 60]`
3. After `numbers[2] = 35`: `[10, 20, 35, 40, 50, 60]`
4. After `numbers.pop(0)`: `[20, 35, 40, 50, 60]`
5. After `numbers.remove(40)`: `[20, 35, 50, 60]`
6. Finally, `print(numbers)` outputs `[20, 35, 50, 60]`.

---

# Tuple Basics

---

## Creating a Tuple

- **tuple** - A tuple, usually pronounced "tuhple" or "toople," stores a collection of data, like a list, but is immutable – once created, the tuple's elements cannot be changed.

```py
point = (3, 4)
print(point)  # Output: (3, 4)
```

---

## Named Tuples

**named tuple** - Named tuple allows the programmer to define a new simple data type that consists of named attributes.
**namedtuple** - The namedtuple container must be imported to create a new named tuple.

```py
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(p.x)  # Output: 3
print(p.y)  # Output: 4
```

---

# Set Basics

---

## Creating a Set

**set** - A set is an unordered collection of **unique elements**.
**set()** - A set can be created using the set() function, which accepts a sequence-type iterable object (list, tuple, string, etc.) whose elements are inserted into the set.
**set literal** - A set literal can be written using curly braces { } with commas separating set elements.

```py
# Creating a set using set() function
fruits = {"apple", "banana", "cherry"}
print(fruits)  # Output: {'banana', 'cherry', 'apple'}
```

---

## Modifying a Set

**add()** - The add() method places a new element into the set if the set does not contain an element with the provided value.
**remove() / pop()** - The remove() and pop() methods remove an element from the set.

```py
fruits = {"apple", "banana", "cherry"}
fruits.add("date")
print(fruits)  # Output: {'banana', 'cherry', 'apple', 'date'}
fruits.remove("banana")
print(fruits)  # Output: {'cherry', 'apple', 'date'}
fruits.add("apple")  # No effect, 'apple' is already in the set
print(fruits)  # Output: {'cherry', 'apple', 'date'}
```

---

## Common Set Operations

| Operation         | Description                               |
| ----------------- | ----------------------------------------- |
| len(set)          | Returns the number of elements in the set |
| set1.update(set2) | Adds all elements from set2 to set1       |
| set.add(v)        | Adds value v to the set                   |
| set.remove(v)     | Removes value v from the set              |
| set.pop()         | Removes and returns an arbitrary element  |
| set.clear()       | Removes all elements from the set         |

---

## Common Set Theory Operations

| Operation                      | Description                                                |
| ------------------------------ | ---------------------------------------------------------- |
| set.intersection(set2)         | Returns a new set with elements common to both sets        |
| set.union(set2)                | Returns a new set with all elements from both sets         |
| set.difference(set2)           | Returns a new set with elements in set1 not in set2        |
| set.symmetric_difference(set2) | Returns a new set with elements in either set but not both |

---

## Set Theory Examples

```py
setA = {1, 2, 3, 4}
setB = {3, 4, 5, 6}
print(setA.intersection(setB))         # Output: {3, 4}
print(setA.union(setB))                # Output: {1, 2, 3, 4, 5, 6}
print(setA.difference(setB))           # Output: {1, 2}
print(setA.symmetric_difference(setB)) # Output: {1, 2, 5, 6}
```

---

## Example Problem

What is the output of the following code?

```py
nums = {1, 2, 3, 4}

nums.add(5)
nums.remove(2)
nums.add(3)

print(nums)
```

---

## Example Problem - Solution

The output of the code will be: `{1, 3, 4, 5}`
**Here's the step-by-step breakdown:**

1. Start with the initial set: `{1, 2, 3, 4}`
2. After `nums.add(5)`: `{1, 2, 3, 4, 5}`
3. After `nums.remove(2)`: `{1, 3, 4, 5}`
4. After `nums.add(3)`: No effect, since 3 is already in the set.
5. Finally, `print(nums)` outputs
   `{1, 3, 4, 5}`.

---

# Dictionary Basics

---

## Creating a Dictionary

- **dictionary** - A dictionary is a Python container used to describe associative relationships.
- **dict** - A dictionary is represented by the dict object type.
- **key** - A key is a term that can be located in a dictionary, such as the word "cat" in the English dictionary.
- **value** - A value describes some data associated with a key, such as a definition.
- **curly braces / key:value pairs** - A dict object is created using curly braces { } to surround the key:value pairs that comprise the dictionary contents.

---

## Creating a Dictionary Example

```py
caffeine_content_mg = {
	"coffee": 95,
	"tea": 47,
	"soda": 40,
	"energy drink": 80
}
print(caffeine_content_mg)
# Output: {'coffee': 95, 'tea': 47, 'soda': 40, 'energy drink': 80}
```

---

## Accessing Dictionary Values

- A dictionary value can be accessed by providing the key inside brackets [ ] appended to the dictionary variable name.
- **KeyError** - If no entry with a matching key exists in the dictionary, then a KeyError runtime error occurs.

```py
caffeine_content_mg = {
	"coffee": 95,
	"tea": 47,
	"soda": 40,
	"energy drink": 80
}
coffee_caffeine = caffeine_content_mg["coffee"]
print(coffee_caffeine)  # Output: 95
```

---

## Updating Dictionary Values

- A dictionary value can be updated by performing an assignment to the key inside brackets [ ] appended to the dictionary variable name.

```py
caffeine_content_mg = {
	"coffee": 95,
	"tea": 47,
	"soda": 40,
	"energy drink": 80
}
caffeine_content_mg["tea"] = 50
print(caffeine_content_mg)
# Output: {'coffee': 95, 'tea': 50, 'soda': 40, 'energy drink': 80}
```

---

## Adding Dictionary Entries

- A new dictionary entry can be added by performing an assignment to a new key inside brackets [ ] appended to the dictionary variable name.

```py
caffeine_content_mg = {
	"coffee": 95,
	"tea": 47,
	"soda": 40,
	"energy drink": 80
}
caffeine_content_mg["matcha"] = 70
print(caffeine_content_mg)
# Output: {'coffee': 95, 'tea': 47, 'soda': 40, 'energy drink': 80, 'matcha': 70}
```

---

## Deleting Dictionary Entries

**del** - The del keyword is used to remove entries from a dictionary: del prices["papaya"] removes the entry whose key is "papaya".

```py
caffeine_content_mg = {
	"coffee": 95,
	"tea": 47,
	"soda": 40,
	"energy drink": 80
}
del caffeine_content_mg["soda"]
print(caffeine_content_mg)
# Output: {'coffee': 95, 'tea': 47, 'energy drink': 80}
```

---

# Date Types Summary

---

| Data Type | Mutable / Immutable | Description                             |
| --------- | ------------------- | --------------------------------------- |
| int       | Immutable           | Integer numbers                         |
| float     | Immutable           | Floating-point numbers                  |
| str       | Immutable           | Sequence of characters (text)           |
| list      | Mutable             | Ordered collection of elements          |
| tuple     | Immutable           | Ordered collection of elements          |
| set       | Mutable             | Unordered collection of unique elements |
| dict      | Mutable             | Collection of key:value pairs           |
