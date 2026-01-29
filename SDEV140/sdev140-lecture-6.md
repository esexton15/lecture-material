---
marp: true
theme: gaia
class: invert
paginate: true
---

# Chapter 7.1 – Basic Graphics (TKinter)

---

## 7.1 Basic Graphics

- Python supports graphical applications
- Graphical applications display drawings and visual objects
- TKinter is Python’s standard graphics package
- Graphics are displayed inside a window called a **Frame**

---

## What Is a Frame?

- A **Frame** is a window that holds graphical content
- Frames are created using the `tk.Frame` class
- A frame does **not** appear automatically when created

---

## Creating a Graphics Frame

Key steps to display a frame:

1. Create a `Tk()` object
2. Set the frame size using `geometry()`
3. Set the title using `title()`
4. Call `mainloop()` to display the window

---

## Example: Creating an Empty Frame

```python
import tkinter as tk

class Application(tk.Frame):
   def __init__(self, master=None):
       super().__init__(master)
       self.master = master

       # Set the frame's title
       self.master.title("An Empty Frame")
       self.pack()

app_frame = tk.Tk()

# Set the frame's width (400) and height (250) in pixels
app_frame.geometry("400x250")

# Make the frame visible to the user
app = Application(master=app_frame)
app.mainloop()
```

---

## Important Frame Configuration Methods

- `geometry("widthxheight")`
  - Sets frame size in pixels
  - If omitted, the frame may be too small to see

- `title("String")`
  - Sets the window title

- `mainloop()`
  - Makes the frame visible and interactive

---

## Participation Activity 7.1.1

**Configuring a Frame**

Assume an empty Frame object named `appFrame`.

1. The frame window lacks a title. The title should be "My program".
2. The frame is not visible. The size should be 500 x 300 pixels.

---

## Drawing Graphical Objects

- Frames can display shapes like:
  - Rectangles
  - Circles (ovals)
  - Lines

- Shapes are drawn using a **Canvas** object

---

## What Is a Canvas?

- A Canvas is added inside a Frame
- Used for drawing 2D graphics
- Supports basic shapes and colors

---

## Creating a Canvas

```python
import tkinter as tk
from tkinter import Canvas, Frame, BOTH

class Application(tk.Frame):
   def __init__(self, master=None):
       super().__init__(master)
       self.master = master
       self.pack(fill=BOTH, expand=1)

       canvas = Canvas(self)
       # Write your drawing instructions

app_frame = tk.Tk()
app_frame.geometry("400x250")
app = Application(master=app_frame)
app.mainloop()
```

---

## Filling the Frame with the Canvas

```python
self.pack(fill=BOTH, expand=1)
```

- Ensures the canvas uses all available space
- Important for correct layout and scaling

---

## Drawing Rectangles

Use `create_rectangle()`

Arguments:

1. x0 – top-left x
2. y0 – top-left y
3. x1 – bottom-right x
4. y1 – bottom-right y
5. outline (optional)
6. fill (optional)

---

## Example: Drawing a Filled Rectangle

```python
canvas = Canvas(self)
canvas.create_rectangle(10, 75, 160, 125,
         outline="cyan", fill="cyan")
```

---

## What Happens Internally?

- Canvas object is created
- Rectangle size and color data are stored
- Canvas updates its internal state
- Rectangle is drawn on the frame

---

## Canvas Coordinate System

- Top-left corner is (0, 0)
- x increases to the right
- y increases downward

Understanding coordinates is critical for positioning shapes

---

## Participation Activity 7.1.3

**Drawing Colored Rectangles**

Assume `canvas` is a Canvas object.

1. Draw a rectangle starting at (5, 5) with size 100 x 100
2. Draw a pink rectangle with a blue outline

---

## Example: Drawing a Histogram

- Multiple rectangles represent data values
- Each bar is a rectangle on the canvas

---

## Histogram Example Code

```python
import tkinter as tk
from tkinter import Canvas, Frame, BOTH

class HistogramViewer(tk.Frame):
   def __init__(self, master=None):
       super().__init__(master)
       self.master = master
       self.master.title("Histogram Viewer")
       self.pack(fill=BOTH, expand=1)

       canvas = Canvas(self)
       canvas.create_rectangle(10, 10, 210, 60, outline="darkolivegreen4", fill="darkolivegreen4")
       canvas.create_rectangle(10, 75, 160, 125, outline="cyan", fill="cyan")
       canvas.create_rectangle(10, 140, 360, 190, outline="gray40", fill="gray40")

       canvas.pack(fill=BOTH, expand=1)
       self.pack()

app_frame = tk.Tk()
app_frame.geometry("400x250")
histogram_viewer = HistogramViewer(master=app_frame)
histogram_viewer.mainloop()
```

---

## Participation Activity 7.1.4

**Drawing Rectangles**

Which code segment performs the operation?

1. Draws a filled-in square
2. Draws a rectangle 50 pixels wide and 150 pixels tall
3. Draws a rectangle starting at the origin
4. Draws a rectangle with a black outline

---

## Common Canvas Shapes

| Shape     | Description       | Method               |
| --------- | ----------------- | -------------------- |
| Rectangle | Draws a rectangle | `create_rectangle()` |
| Oval      | Draws an ellipse  | `create_oval()`      |
| Line      | Draws a line      | `create_line()`      |
| Polygon   | Draws a polygon   | `create_polygon()`   |

---

## Exploring Further

- TKinter supports many named colors
- Color charts show all available color names
- Experimenting helps build intuition

---

## Key Takeaways

- Frames create application windows
- Canvases draw graphical objects
- Coordinates control positioning
- Rectangles are the foundation for many graphics

---

# Chapter 7.3 – While Loops

---

## Introduction to While Loops

- A **while loop** runs a block of code repeatedly
- The loop continues **as long as the condition is True**
- The loop stops when the condition becomes False

Example use case:

- A guessing game that runs until the correct answer is guessed

---

## Iterations

- Each execution of a loop is called an **iteration**
- While loops may run:
  - Zero times
  - A fixed number of times
  - An unknown number of times

---

## While Loop Structure

```python
while expression:   # Loop condition
    # Loop body
    # Executes if the expression is True

# Code here runs after the expression becomes False
```

---

## Participation Activity 7.3.1

**Tracing a While Loop**

```python
value = 1

while value < 6:
    print(value)
    value = value * 2

print("Done")
```

---

## Step-by-Step Execution

1. `value` starts at 1
2. Condition `value < 6` is True → loop runs
3. Value is printed and doubled
4. Loop repeats until `value` becomes 8
5. Condition becomes False → loop ends
6. `"Done"` is printed

---

## Key Concepts from the Example

- Initialization happens **before** the loop
- The condition is checked **before each iteration**
- The loop body must update the condition

---

## Participation Activity 7.3.2

**While Loop Questions**

1. What is the output?

```python
total = 5

while total <= 25:
    print(total)
    total = total * 2
```

2. What does indentation indicate in a while loop?
3. How many times will the loop iterate?

```python
score = 0

while score < 20:
    print(score, end=" ")
    score = score + 5
```

---

## Sentinel Values

- A **sentinel value** causes a loop to stop
- The user controls when the loop ends
- Common in input-driven programs

Example sentinel: `"stop"`, `999`, `"quit"`

---

## Sentinel Value Example

```python
password = "star"
user_input = input("Enter the password: ")

while user_input != password:
    print("Wrong password. Try again.")
    user_input = input("Enter the password: ")

print("Access granted.")
```

---

## How the Sentinel Works

- The sentinel value is `"star"`
- Loop continues while input does NOT match the sentinel
- When sentinel is entered, the loop exits

---

## Participation Activity 7.3.4

**Sentinel Values**

1. What is the purpose of the sentinel value?

```python
sentinel = 999
input_value = 0

while input_value != sentinel:
    input_value = int(input("Enter your number or type 999 to stop: "))
```

2. How many times will this loop run if the user types `quit` first?

```python
sentinel = "quit"
command = ""

while command != sentinel:
    command = input("Type quit to exit: ")
```

---

## Infinite Loops

- An **infinite loop** never stops running
- Happens when the condition is always True
- Often caused by incorrect updates to variables

---

## Infinite Loop Example

```python
score = 1

while score > 0:
    score = score * 2
    print(score)
```

---

## Why This Loop Is Infinite

- `score` always increases
- `score` will always be greater than 0
- Condition never becomes False

---

## Infinite Loops: Important Notes

- Infinite loops are usually bugs
- Sometimes intentional (e.g., games, servers)
- Always double-check loop conditions

---

## Participation Activity 7.3.6

**Infinite Loops**

1. How could the infinite loop be stopped?
2. What happens when this code runs?

```python
name = ""
while True:
    name += "a"
    print(name)
```

3. What is the final output?

```python
index = 0

while index > 0:
    print(index, end=" ")
    index = index - 1
print("Bye")
```

---

## Challenge Activity 7.3.1

**While Loop Condition**

Write a while loop condition that continues looping while `in_val` is not equal to `"q"`.

Example:

```python
while __________________:
    in_val = input()
```

---

## Chapter 7.3 Takeaways

- While loops repeat based on conditions
- Sentinel values give users control
- Infinite loops are a common bug
- Correct updates prevent logic errors

---

# Chapter 7.4 – More While Loop Examples

---

## Stepping Through a While Loop

- While loops are often used to process numbers digit by digit
- `% 10` gets the **rightmost digit** of a number
- `// 10` removes the **rightmost digit**

---

## Printing Digits of a Number

```python
# Read num from user ...

while num > 0:
    print(num % 10)
    num = num // 10
```

- Loop continues while `num > 0`
- Each iteration prints one digit
- Digits are printed from **right to left**

---

## Example Walkthrough

User input: `902`

| Iteration | num | Output |
| --------- | --- | ------ |
| 1         | 902 | 2      |
| 2         | 90  | 0      |
| 3         | 9   | 9      |

Loop stops when `num` becomes `0`

---

## Key Takeaways from Digit Example

- `%` is used to extract information
- `//` reduces the number each iteration
- The loop condition eventually becomes False

---

## Participation Activity 7.4.2

**Stepping Through While Loops**

1.

```python
count = 567
while count > 0:
    print(count % 10)
    count //= 10
```

2.

```python
num = -123
while num > 0:
    print(num % 10 * 2)
    num //= 10
```

3.

```python
color = "purple"
n = 1
while n < len(color):
    print(color[n])
    n += 2
```

---

## Greatest Common Divisor (GCD)

- GCD finds the largest number that divides two integers
- Uses **Euclid’s algorithm**
- Repeats until both numbers are equal

---

## GCD Algorithm Logic

- If `num_a > num_b`, subtract `num_b` from `num_a`
- Else subtract `num_a` from `num_b`
- Repeat until `num_a == num_b`

---

## Participation Activity 7.4.3

**GCD Tracing**

Input values:

- `num_a = 15`
- `num_b = 10`

Answer the following by tracing the loop:

1. Value of `num_a` before first iteration
2. Value of `num_a` after first iteration
3. Value of `num_b` after second iteration
4. Total number of loop iterations

---

## Conversation Example

- Program repeatedly responds to user input
- Loop continues until user types `"Goodbye"`
- Uses `random.randint()` to vary responses

---

## Key Conversation Concepts

- Loop condition compares strings
- `randint(a, b)` returns a random integer from `a` to `b`
- `elif` selects which response to print

---

## Participation Activity 7.4.4

**Conversation Program**

1. Which branch executes if the user types `"Goodbye"`?
2. How many times does the loop iterate?
3. Which expression returns a value between 0 and 5?

---

## Input Until a Sentinel

- Loops often process a series of values
- A sentinel ends the loop
- Sentinel is not included in calculations

---

## Sentinel Average Example

- Reads positive integers
- Ends when user enters `0`
- Computes the average of entered values

---

## Participation Activity 7.4.5

**Average with Sentinel**

Input sequence: `10 1 6 3 0`

1. How many non-sentinel values?
2. Final value of `num_values`?
3. What if first input was `0`?
4. What happens with input `10 1 6 3 -1`?

---

## Challenge Activity 7.4.1

**Finding a Maximum Value**

```python
entered_value = int(input())
max_number = entered_value

while entered_value > 0:
    if entered_value > max_number:
        max_number = entered_value
    entered_value = int(input())

print(f"Max value: {max_number}")
```

---

## Challenge Activity 7.4.2

**Bidding Example**

- Continue bidding while input is not `"n"`
- Requires correct loop condition

---

## Challenge Activity 7.4.3

**Insect Growth**

- Loop runs while insects ≤ 100
- Each iteration:
  - Print count
  - Double the value

---

## Challenge Activity 7.4.4

**Advanced While Loop**

- Loop continues until input equals `-4`
- Prints a message each iteration

---

## Chapter 7.4 Takeaways

- While loops are powerful for unknown iteration counts
- `%` and `//` are useful for numeric processing
- Sentinels control loop termination
- Careful tracing prevents logic errors

## 7.6 For Loops

### Introduction to `for` loops

- Used to access **each element in a container**, one at a time
- Common containers: **lists, strings, dictionaries**
- Each iteration assigns the loop variable to the _next element_

```python
for variable in container:
    # loop body

# code after the loop
```

---

### Example: Iterating over a list

```python
for name in ["Kai", "Sam", "Alex"]:
    print(f"Hi {name}!")

print("Done")
```

- Loop variable takes each value in order
- Loop ends after last element

---

### How a `for` loop works (mentally)

1. Take the **next item** from the container
2. Assign it to the loop variable
3. Run the loop body
4. Repeat until no items remain

---

### Participation 7.6.2 — Key answers

- Purpose of a `for` loop: **iterate over items in a container**
- Real‑world analogy: **checking each item in a list one by one**

```python
my_list = [5, 6, 7]
for x in my_list:
    if x == 5:
        print("Found element 5")
```

**Output:**

```
Found element 5
```

---

### For loops with strings

- Strings are sequences of characters

```python
my_str = "Yes"
for char in my_str:
    print(char)
```

**Output:**

```
Y
e
s
```

---

### For loops with dictionaries

- Loop variable receives **keys**
- Values accessed using `dict[key]`

```python
channels = {"MTV": 35, "CNN": 28, "NBC": 4}

for c in channels:
    print(f"{c} is on channel {channels[c]}")
```

---

### Participation 7.6.5 — Answers

1. A dictionary loop iterates over **keys**
2. Output:

```
c
a
t
```

3. Output:

```
ab
```

4. Output:

```
p y t t h o n
```

---

### Creating `for` loops — Solutions

```python
for my_pet in ["Scooter", "Kobe", "Bella"]:
    pass
```

```python
for price in my_prices:
    pass
```

```python
for number in "911":
    pass
```

---

### For loop example: Calculating revenue

```python
total = 0
for day in daily_revenues:
    total += day

average = total / len(daily_revenues)
```

- Accumulators are common with `for` loops

---

### Looping in reverse

```python
for name in reversed(names):
    print(name)
```

- `reversed()` changes iteration order

---

### Participation 7.6.7 — Answers

1.

```python
total += num
```

2.

```python
num_neg += 1
```

3.

```python
for scr in reversed(scores):
```

---

### Key takeaways

- `for` loops are best when **number of items is known**
- `while` loops are better for **condition‑based repetition**
- Loop variable automatically updates — no manual increment

## 7.7 Counting using the `range()` function

### The `range()` function

- While loops are often used for counting a specific number of iterations.
- For loops are commonly used to iterate over all elements of a container.
- The `range()` function allows **counting with a for loop** by generating a sequence of integers.

`range()` generates integers starting from a **start value** (included), stopping before an **end value** (not included), and optionally stepping by a given amount.

---

### Forms of `range()`

#### `range(Y)`

Generates all non-negative integers less than `Y`.

```python
for i in range(3):
    print(i)
```

Output:

```
0
1
2
```

---

#### `range(X, Y)`

Generates integers **greater than or equal to `X` and less than `Y`**.

```python
for i in range(-7, -3):
    print(i)
```

Output:

```
-7
-6
-5
-4
```

---

#### `range(X, Y, Z)` (positive step)

Generates integers starting at `X`, incrementing by `Z`, and stopping before `Y`.

```python
for i in range(0, 50, 10):
    print(i)
```

Output:

```
0
10
20
30
40
```

---

#### `range(X, Y, Z)` (negative step)

Generates integers starting at `X`, decrementing by `Z`, and stopping once the value is no longer greater than `Y`.

```python
for i in range(3, -1, -1):
    print(i)
```

Output:

```
3
2
1
0
```

---

### Key ideas to emphasize

- The **ending value is never included** in the range
- The step value controls how the sequence changes each iteration
- A negative step is required to count downward
- `range()` is commonly used when you **know how many times** a loop should run

---

### Common mistakes

- Forgetting that the end value is excluded
- Using a positive step when counting down
- Creating a range that never runs (start already past end)

```python
# This loop never runs
for i in range(10, 0):
    print(i)
```

---

### When to use `range()`

- Counting iterations
- Repeating an action a fixed number of times
- Index-based access into lists
- Generating numeric sequences

## 7.8 While vs. for loops

### While loop and for loop correspondence

- Both **while loops** and **for loops** can be used to count a specific number of iterations.
- A **for loop combined with `range()`** is generally preferred when counting.
- For loops are **less likely to become infinite loops** because they iterate over a finite sequence.
- With while loops, it is easy to forget to update the loop variable, causing an unintended infinite loop.

---

### Example: While loop vs. for loop

#### While loop version

```python
i = 0
while i < 100:
    # Loop body statements
    i += 1
```

#### Equivalent for loop version

```python
for i in range(100):
    # Loop body statements
```

---

### How the conversion works

```python
# Original while loop
i = 0
while i < 100:
    i += 1
```

Can be rewritten as:

```python
for i in range(0, 100, 1):
    pass
```

And simplified to:

```python
for i in range(100):
    pass
```

---

### General guidelines

Use a **for loop** when:

- The number of iterations is known before the loop starts
- Counting a fixed number of times (e.g., repeat N times)
- Iterating over elements in a container (list, string, dictionary)

Use a **while loop** when:

- The number of iterations is not known in advance
- Looping until a condition becomes true
- Waiting for user input or a sentinel value

These are **guidelines**, not strict rules.

---

### Participation activity: Choosing the correct loop

Decide whether a **while loop** or **for loop** should be used:

1. Iterate as long as the user-entered string `c` is not `"q"`
2. Iterate until the values of `x` and `y` are equal, where both are updated in the loop body
3. Iterate exactly 1500 times

---

### Key takeaway

- Use **for + `range()`** for counting and container traversal
- Use **while loops** for condition-controlled repetition
- Choosing the right loop improves **readability**, **safety**, and **correctness**

---

## 7.9 Nested Loops

### What is a nested loop?

A **nested loop** is a loop that exists inside the body of another loop.

- The **outer loop** controls how many times the inner loop runs.
- The **inner loop** completes _all_ of its iterations for **each** iteration of the outer loop.

> Think of nested loops as a clock:
>
> - Hours = outer loop
> - Minutes = inner loop
>   Every time the hour changes, minutes run from start to finish again.

---

### Why use nested loops?

Nested loops are commonly used to:

- Generate **all combinations** of values
- Work with **rows and columns** (grids, tables, seating charts)
- Create **patterns** (rectangles, triangles, histograms)

---

### Example: Generating combinations

This program prints all two‑letter `.com` domain names using nested `while` loops.

```python
print("Two-letter domain names:")

letter1 = "a"
while letter1 <= "z":          # Outer loop
    letter2 = "a"
    while letter2 <= "z":      # Inner loop
        print(f"{letter1}{letter2}.com")
        letter2 = chr(ord(letter2) + 1)
    letter1 = chr(ord(letter1) + 1)
```

**Key idea:**

- For each value of `letter1`, the inner loop runs **26 times**.
- Total combinations: `26 × 26 = 676` domain names.

---

### Visualizing nested loops

```python
for i in range(2):      # Outer loop
    for j in range(3):  # Inner loop
        print(i, j)
```

Execution order:

```
(0,0) (0,1) (0,2)
(1,0) (1,1) (1,2)
```

The inner loop completes **fully** before the outer loop moves on.

---

### Common beginner mistakes 🚧

- Forgetting to **reset the inner loop variable**
- Expecting inner and outer loops to advance together
- Creating infinite loops by failing to update loop variables

---

### Participation Activity: Nested Loops

**1)** How many times does the inner loop run?

```python
for i in range(2):
    for j in range(3):
        pass
```

**Answer:** 6 times

---

**2)** How many times does `print()` execute?

```python
for i in range(5):
    for j in range(10, 12):
        print(f"{i}{j}")
```

**Answer:** 10 times

---

**3)** What is the output?

```python
c1 = "a"
while c1 < "b":
    c2 = "a"
    while c2 <= "c":
        print(f"{c1}{c2}", end=" ")
        c2 = chr(ord(c2) + 1)
    c1 = chr(ord(c1) + 1)
```

**Answer:**

```
aa ab ac
```

---

**4)** What is the output?

```python
i1 = 1
while i1 < 19:
    i2 = 3
    while i2 <= 9:
        print(f"{i1}{i2}", end=" ")
        i2 = i2 + 3
    i1 = i1 + 10
```

**Answer:**

```
13 16 19 113 116 119
```

---

### Key takeaway 🧠

> **Total executions of the inner loop = outer iterations × inner iterations**

Nested loops are powerful—but should be used thoughtfully as they increase runtime quickly.

---

## 7.10 Developing Programs Incrementally

### What is Incremental Programming?

- Writing a program **step by step**, not all at once
- Start with a **simple, working version**
- Gradually add features and handle more cases
- Test after _every small change_

> Big idea: **Make it work → make it better → make it complete**

---

### Why Incremental Programming Matters

- Large programs often have **many bugs** at first
- Debugging a big, broken program is difficult
- Small changes are easier to test and fix
- This is how **professional developers** work

---

### Example Problem: Phone Number Conversion

Goal:

- Convert phone numbers with letters into **numbers only**
- Example: `1-555-HOLIDAY` → `1-555-4654329`

Based on a standard phone keypad:

- 2 → A B C
- 3 → D E F
- 4 → G H I
- 5 → J K L
- 6 → M N O
- 7 → P Q R S
- 8 → T U V
- 9 → W X Y Z

---

### Version 1: Verify the Loop Works

**Purpose:** Make sure we can loop through the string correctly

```python
user_input = input("Enter phone number: ")

index = 0
for character in user_input:
    print(f"Element {index} is: {character}")
    index += 1
```

✔ Confirms each character is processed correctly

---

### Version 2: Handle Numbers Only

**New goal:** Keep digits, replace everything else with `?`

```python
user_input = input("Enter phone number: ")
phone_number = ""

for character in user_input:
    if "0" <= character <= "9":
        phone_number += character
    else:
        # FIXME: Add elif branches for letters and hyphen
        phone_number += "?"

print(f"Numbers only: {phone_number}")
```

🛠 `FIXME` comments mark **future work**

---

### What Are FIXME Comments?

- Highlight incomplete logic
- Easy to search for later
- Often highlighted by editors
- Common in real-world codebases

Example:

```python
# FIXME: Add remaining letter mappings
```

---

### Version 3: Add Letters A–C and Hyphens

**New goal:** Handle first keypad letters and hyphens

```python
for character in user_input:
    if ("0" <= character <= "9") or (character == "-"):
        phone_number += character
    elif ("a" <= character <= "c") or ("A" <= character <= "C"):
        phone_number += "2"
    # FIXME: Add remaining elif branches
    else:
        phone_number += "?"
```

✔ Program still works
✔ Behavior improves

---

### Version 4: Complete the Program

**Final behavior:**

Input:

```
1-555-HOLIDAY
```

Output:

```
1-555-4654329
```

Also works with:

- Lowercase letters
- Numbers only
- Unexpected characters (replaced with `?`)

---

### Key Takeaways

- Do **not** write the entire program at once
- Test after every small change
- Use `FIXME` to track unfinished work
- Incremental programming reduces bugs and stress

---

### Participation Activity: Incremental Programming

**True or False**

1. Incremental programming may help reduce the number of errors in a program.
2. FIXME comments provide a way for a programmer to remember what needs to be added.
3. Once a program is complete, a programmer can expect to see several FIXME comments.

---

### Answers

1. ✅ True
2. ✅ True
3. ❌ False — FIXME comments should be removed when the program is complete

---

## 7.11 Break and Continue

### Break statements

- `break` immediately exits the **nearest enclosing loop**
- Often used when a desired condition has been met
- Can make loops easier to understand by **ending early** instead of adding complex conditions
- Especially useful in **search problems**

---

### Example: Using `break` to stop searching

```python
empanada_cost = 3
taco_cost = 4

user_money = int(input("Enter money for meal: "))

max_empanadas = user_money // empanada_cost
max_tacos = user_money // taco_cost

meal_cost = 0
for num_tacos in range(max_tacos + 1):
    for num_empanadas in range(max_empanadas + 1):
        meal_cost = (num_empanadas * empanada_cost) + (num_tacos * taco_cost)

        if meal_cost == user_money:
            break

    if meal_cost == user_money:
        break
```

---

### Why `break` helps here

Without `break`:

- Loop conditions become more complex
- Additional flags or variables are needed
- Code becomes harder to read and debug

With `break`:

- Logic matches human reasoning: _“stop once found”_
- Less nesting and fewer condition checks

---

### Participation: Break statements

```python
mult = 0
while a < 10:
    mult = b * a
    if mult > c:
        break
    a = a + 1
z = a
```

- Trace the loop step by step
- Identify **when the break triggers**
- Final value of `a` becomes `z`

---

## Continue statements

- `continue` immediately jumps to the **next loop iteration**
- Skips the remaining code in the loop body
- Useful for **filtering out unwanted cases early**

---

### Example: Using `continue` to skip invalid cases

```python
if (num_tacos + num_empanadas) % num_diners != 0:
    continue
```

- Invalid combinations are skipped
- Remaining logic stays clean and readable
- Avoids deep nesting like:

```python
if valid:
    if cost_matches:
        ...
```

---

### Full example: `continue` in nested loops

```python
for num_tacos in range(max_tacos + 1):
    for num_empanadas in range(max_empanadas + 1):

        if (num_tacos + num_empanadas) % num_diners != 0:
            continue

        meal_cost = (num_empanadas * empanada_cost) + (num_tacos * taco_cost)

        if meal_cost == user_money:
            print(f"${meal_cost} buys {num_empanadas} empanadas and {num_tacos} tacos")
```

---

### Break vs Continue

| Statement  | Effect                     |
| ---------- | -------------------------- |
| `break`    | Exit the loop entirely     |
| `continue` | Skip to the next iteration |

---

### When to use them (carefully)

Use `break` when:

- Searching for a value
- Only the **first match** matters

Use `continue` when:

- Filtering input
- Ignoring invalid or unwanted cases

⚠️ Overuse can reduce readability — use only when intent is clear

---

### Common pitfalls

- Forgetting a `break` in nested loops (only exits **one** loop)
- Skipping important updates after `continue`
- Making control flow harder to follow for new readers

---

### Participation: Continue statements

```python
for i in range(5):
    if i < 10:
        continue
    print(i)
```

- Loop still iterates 5 times
- `print(i)` never runs
- Output: _(nothing)_

---

### Key takeaways

- `break` stops a loop early
- `continue` skips the rest of the current iteration
- Both can simplify logic **when used intentionally**
- Always prioritize readability for future readers (including yourself)
