---
marp: true
theme: gaia
class: invert
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

# SDEV Lecture 5 - More about Lists & Dictionaries

---

# Lists

---

## Lists

- **container** - A container is an object that groups related objects together.
- **list / mutable** - A list is a mutable container, meaning the size of the list can grow or shrink and elements within the list can change.
- **list()** - The list() function accepts a single iterable object argument, such as a string, list, or tuple, and returns a new list object.
- **index** - An index is a zero-based integer matching to a specific position in the list's sequence of elements.

---

## List - Common Operations

| Operations        | Description                    |
| ----------------- | ------------------------------ |
| my_list = [1,2,3] | Create a list                  |
| list(iter)        | Create a list from an iterable |
| len(my_list)      | Get the length of the list     |
| my_list[i]        | Access element at index i      |
| my_list[i] = x    | Modify element at index i      |
| my_list.append(x) | Add element x to end of list   |
| del my_list[i]    | Remove element at index i      |

---

# List Methods

---

## List Methods - Adding Elements

| Method           | Description                                          |
| ---------------- | ---------------------------------------------------- |
| list.append(x)   | Adds element x to the end of the list                |
| list.extend([x]) | Extends list by appending elements from the iterable |
| list.insert(i,x) | Inserts element x at index i                         |

---

## List Methods - Removing Elements

| Method         | Description                                           |
| -------------- | ----------------------------------------------------- |
| list.remove(x) | Removes first occurrence of element x                 |
| list.pop()     | Removes and returns element at index i (default last) |
| list.pop(i)    | Removes and returns element at index i                |

---

## List Method - Modifying elements

| Method         | Description                                |
| -------------- | ------------------------------------------ |
| list.sort()    | Sorts the elements of the list in place    |
| list.reverse() | Reverses the elements of the list in place |

---

## List Methods - Misc

| Method        | Description                                    |
| ------------- | ---------------------------------------------- |
| list.index(x) | Returns the index of the first occurrence of x |
| list.count(x) | Returns the number of occurrences of x         |

---

## Example - List Methods

```python
fruits = ['apple', 'banana', 'cherry']
fruits.append('orange')      # ['apple', 'banana', 'cherry', 'orange']
fruits.insert(1, 'kiwi')     # ['apple', 'kiwi', 'banana', 'cherry', 'orange']
fruits.remove('banana')      # ['apple', 'kiwi', 'cherry', 'orange']
fruits.pop()                 # ['apple', 'kiwi', 'cherry']
fruits.sort()                # ['apple', 'cherry', 'kiwi']
```

---

## Exercise - List Methods

Is there a better way to get the lowest score from the list below?

```python
scores = [88, 92, 79, 93, 85]
scores.sort()
lowest_score = scores[0]
print("The lowest score is:", lowest_score)
```

---

## Exercise Solutions

You can use the built-in min() function to get the lowest score. Arguable this is more readable:

```python
scores = [88, 92, 79, 93, 85]
lowest_score = min(scores)
print("The lowest score is:", lowest_score)
```

---

## List Exercise

What code can I write to calculate the average score from the list below?

```python
scores = [88, 92, 79, 93, 85]

# Your code here
```

---

## Exercise Solutions

You can calculate the average score by summing the scores and dividing by the number of scores:

```python
scores = [88, 92, 79, 93, 85]
average_score = sum(scores) / len(scores)
print("The average score is:", average_score) # Output: The average score is: 87.4
```

---

# Iterating over a list

---

## List iteration

_A programmer accesses each element of a list. Thus, learning how to iterate through a list using a loop is critical._

- **for loop** - Looping through a sequence such as a list is so common that Python supports a construct called a for loop, specifically for iteration purposes.

```python
for my_var in my_list:
    # Loop body statements go here
```

_Each iteration of the loop creates a new variable by binding the next element of the list to the name my_var._

---

## Simple List Iteration Example

```python
deductions = [10, 20, 30, 40, 50]
credit_score = 700

for deduction in deductions:
	credit_score -= deduction

print("Final credit score is:", credit_score) # Output: Final credit score is: 550
```

---

## List Iteration Example

```python
print("Input numbers:")
user_input = input("> ")

tokens = user_input.split() # Split input into list of strings

numbers = []
for token in tokens:
	if token.isdigit():
		number = int(token)
		numbers.append(number)
	else:
		print(f"'{token}' is not a valid number. Ignoring.")

## find heighest multiple of 10
highest_multiple_of_10 = None
for number in numbers:
	if number % 10 == 0 and (highest_multiple_of_10 is None) or (number > highest_multiple_of_10):
		highest_multiple_of_10 = number

if highest_multiple_of_10 is not None:
	print(f"The highest multiple of 10 is: {highest_multiple_of_10}")
else:
	print("No multiples of 10 were entered.")

```

---

## IndexError and enumerate()

A common error is to try to access a list with an index that is out of the list's index range

- **IndexError** - Accessing an index that is out of range causes the program to automatically abort execution and generate an IndexError

- **enumerate()** - The built-in enumerate() function iterates over a list and provides an iteration counter.

---

## Enumerate Example

```python
fruits = ['apple', 'banana', 'cherry']
for index, fruit in enumerate(fruits):
	print(f"Index {index}: {fruit}")

# Output:
# Index 0: apple
# Index 1: banana
# Index 2: cherry
```

---

## Enumerate Example - Every Other Element

```python
grades = [85, 90, 78, 92, 88, 76]

# print out every other grade
for index, grade in enumerate(grades):
	if index % 2 == 0:
		print(f"Grade at index {index}: {grade}")

# Output:
# Grade at index 0: 85
# Grade at index 2: 78
# Grade at index 4: 88
```

---

# List Nesting

---

## List Nesting

- **list nesting** - Such embedding of a list inside another list is known as list nesting.

```python
my_list = [[10, 20], [30, 40]]
print(f"First nested list: {my_list[0]}")
print(f"Second nested list: {my_list[1]}")
print(f"Element 0 of first nested list: {my_list[0][0]}")
```

The number of levels of nesting is unlimited or arbitrary. You can nest as little or a much as you need to represent your data.

---

## Multi-dimensional Data Structures

- **multi-dimensional data structure** - List nesting allows for a programmer to also create a multi-dimensional data structure, the simplest being a two-dimensional table, like a spreadsheet or tic-tac-toe board.

```python
tic_tac_toe = [
    ["X", "O", "X"],
    [" ", "X", " "],
    ["O", "O", "X"]
]

print(tic_tac_toe[0][0], tic_tac_toe[0][1], tic_tac_toe[0][2])
print(tic_tac_toe[1][0], tic_tac_toe[1][1], tic_tac_toe[1][2])
print(tic_tac_toe[2][0], tic_tac_toe[2][1], tic_tac_toe[2][2])
```

---

## Nested List Iteration

**nested for loops** - A programmer can access all of the elements of nested lists by using nested for loops.

```python
matrix = [
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9]
]

for row in matrix:
	for element in row:
		print(element, end=' ')
	print()  # New line after each row
```

---

# List Slicing

---

## List Slicing

**slice notation** - A programmer can use slice notation to read multiple elements from a list, creating a new list that contains only the desired elements. `[start:end]` - The slice notation `[start:end]` extracts elements from index `start` up to, but not including, index `end`.

```python
my_list = [10, 20, 30, 40, 50]
sub_list = my_list[1:4]  # Extracts elements at index 1, 2, and 3
print(sub_list)  # Output: [20, 30, 40]
```

_Negative indices can also be used to count backward from the end of the list._

---

## List Slicing - Stride

**stride** - An optional third parameter, called the stride, can be added to the slice notation to specify the step size between elements to be extracted. The syntax is `[start:end:stride]`.

```python
my_list = [10, 20, 30, 40, 50, 60, 70, 80]
sub_list = my_list[1:7:2]  # Extracts elements at index 1, 3, 5
print(sub_list)  # Output: [20, 40, 60]
```

---

## Common Slicing Operations

| Operation                   | Description                                                 |
| --------------------------- | ----------------------------------------------------------- |
| `my_list[start:end]`        | Extracts elements from index start to end-1                 |
| `my_list[start:end:stride]` | Extracts elements from start to end-1 with step size stride |
| `my_list[:end]`             | Extracts elements from start to end-1                       |
| `my_list[start:]`           | Extracts elements from start to the end of the list         |
| `my_list[:]`                | Creates a shallow copy of the entire list                   |

---

# Loops modifying lists

---

## Changing elements' values

_You can change the values of elements in a list while iterating over it using their indices._

```python
my_list = [3.2, 5.0, 16.5, 12.25]

for i in range(len(my_list)):
    my_list[ i ] += 5
```

---

## Changing list size

_Adding elements to a list while iterating over it can lead to unexpected behavior._

```python
my_list = [1, 3, 3, 4, 5, 7, 7, 8, 9]
for item in my_list[:]:
	if item % 2 != 0:
		my_list.remove(item)
```

_This code may not remove all odd numbers as expected because the list size changes during iteration._

---

# List Comprehensions

---

## List Comprehensions

- **list comprehension** - The Python language provides a convenient construct, known as list comprehension, that iterates over a list, modifies each element, and returns a new list of the modified elements.

```python
new_list = [expression for loop_variable_name in iterable]
```

---

## List Comprehension Example

_Explain what the code does:_

_What is this codes output?_

```python
numbers = [5, 10, 15, 20]

new_nums = [num / 5 for num in numbers]

print(new_nums)
```

---

## Conditional list comprehensions

- **conditional list comprehension** - A conditional list comprehension includes an if statement to filter elements from the original list before applying the expression.

```python
user_input = input("Enter numbers separated by spaces: ")
tokens = user_input.split()
numbers = [int(token) for token in tokens if token.isdigit()]
print("Valid numbers are:", numbers)
```

---

## List Comprehension Exercises

```python
def square_even_numbers(numbers):
	# Your code here

squares = square_even_numbers([1, 2, 3, 4, 5, 6])
```
