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

<style scoped>
	h1 {
		height: unset;
		display: block;
	}

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
	}
</style>

# SDEV140 Lecture 8

#### Functions

**Focus:** writing reusable functions and tracing program flow

---

## Today’s outcomes

By the end of class you can:

- Define and call functions with parameters
- Use `return` correctly (and understand `None`)
- Trace program flow across function calls
- Understand local vs global scope (and why globals are risky)
- Explain pass-by-assignment and when mutability creates side effects
- Use keyword arguments, default parameter values, arbitrary argument lists (`*args`, `**kwargs`), and tuple returns (unpacking)

---

# Warm‑up — Why functions?

---

## The problem: repeated code

If you copy/paste logic (like validation or pricing rules), bugs multiply.

Functions let you:

- name a chunk of behavior
- reuse it
- test/debug it in isolation

---

# Functions

---

## Function basics + naming

A function is a **named series of statements**.

- **Definition**: name + indented block (created with `def`)
- **Call**: uses the name to run the block

Good practice: `snake_case` names like `get_name`, `calc_area`, `safe_int`.

---

## `return` statements

A function may return **one** value.

```python
def compute_square(x):
	return x * x
```

Notes:

- `return` can appear anywhere (not only at the end)
- a function can have multiple `return` statements (different paths)

---

## `None` (no return value) + void functions

If a function has no `return` (or `return` with no expression), it returns `None`.

That’s common for **print functions** (sometimes called _void functions_): they do output, not computation.

```python
def greet(name):
	print("Hello", name)

result = greet("Kai")
print(result)  # None
```

---

# Function Type Examples

---

## Writing mathematical functions

A “math function” is just a calculation that:

- takes numeric parameters
- returns a numeric result

Example: convert height (feet + inches) to centimeters.

```python
def height_to_cm(feet, inches):
	total_inches = feet * 12 + inches
	return total_inches * 2.54

print(height_to_cm(5, 10))
```

---

## Function calls inside expressions

A function call evaluates to its **returned value**.

```python
def compute_square(x):
	return x * x

print(5 + compute_square(4))  # 21
```

If a function returns `None` (like a print/void function), you can’t use it in a math expression.

---

## Modular math helpers

Build complex formulas from smaller functions.

```python
import math

def circle_area(r):
	return math.pi * r * r

def cylinder_volume(r, h):
	return circle_area(r) * h

def cylinder_surface_area(r, h):
	return 2 * circle_area(r) + 2 * math.pi * r * h
```

---

## Print functions: why they’re useful

Benefits:

- large outputs don’t clutter the main loop
- write formatting once, call it anywhere
- updating output is less error-prone

---

## Example: menu system

```python
def print_menu():
	print("Today's Menu:")
	print("   1) Gumbo")
	print("   2) Jambalaya")
	print("   3) Quit\n")

quit_program = False

while not quit_program:
	print_menu()
	choice = int(input("Enter choice: "))
	if choice == 3:
		print("Goodbye")
		quit_program = True
	else:
		print("Order:", end=" ")
		if choice == 1:
			print("Gumbo")
		elif choice == 2:
			print("Jambalaya")
		print()
```

---

## Parameters vs arguments

- **Parameter**: input name in the function definition
- **Argument**: value/expression passed in the call

```python
def calc_pizza_area(diameter):
	radius = diameter / 2
	return 3.14159 * radius * radius

print(calc_pizza_area(12.0))
print(calc_pizza_area(16.0))
```

Entering the function binds the parameter name to the argument’s value.

---

## Multiple (or no) parameters

- multiple parameters: separated by commas
- no-parameter functions: still need empty parentheses

```python
def add(a, b):
	return a + b

def show_banner():
	print("Welcome!")

print(add(2, 3))
show_banner()
```

---

## Hierarchical (nested) function calls

A function call can be used as an argument to another call.

```python
user_input = int(input("Enter a number: "))
```

Execution idea:

1. call `input()` → returns a string
2. call `int(...)` with that result → returns an int

---

## Functions with branches/loops

A function body can include:

- `if/elif/else`
- loops (`while` / `for`)
- calls to other functions

This is how you package real “business rules” into a reusable unit.

---

## Example: auction website fee calculator

<!-- Return the fee charged given an item selling price.
$0.50 to list +
- 13% of first $50
- 5% of the amount from $50.01 to $1000
- 2% of the amount above $1000 -->

```python
def calc_ebay_fee(sell_price):
	p50 = 0.13
	p50_to_1000 = 0.05
	p1000 = 0.02
	fee = 0.50

	if sell_price <= 50:
		fee = fee + (sell_price * p50)
	elif sell_price <= 1000:
		fee = fee + (50 * p50) + ((sell_price - 50) * p50_to_1000)
	else:
		fee = (
			fee
			+ (50 * p50)
			+ ((1000 - 50) * p50_to_1000)
			+ ((sell_price - 1000) * p1000)
		)

	return fee

selling_price = float(input("Enter item selling price (ex: 65.00): "))
print(f"eBay fee: ${calc_ebay_fee(selling_price):.2f}")
```

---

## Using a branchy function (tips)

- Test boundary values: 50, 50.01, 1000, 1000.01
- You can call it in a loop to process many prices
- Keep the rules inside the function so the “main story” stays readable

---

## Bigger programs: multiple functions

As programs grow, you’ll use several functions together.

Goal:

- each function does one recognizable job
- the main program reads like a sequence of function calls

---

## Functions are objects (Python)

In Python, a function is an **object**.

That means it has:

- a type (`function`)
- an identity (it’s a real object in memory)
- a value (the compiled code it runs)

When you write a definition like `def print_face():`, Python creates a new function object and binds the name to it.

---

## Multiple names can refer to one function

Because functions are objects, assignment works normally:

```python
def print_face():
	print(":)")

func = print_face  # NOTE: no parentheses

print_face()
func()
```

Both calls run the same function object.

---

## Passing functions as arguments

You can pass a function into another function ("first-class" functions).

```python
def print_human_head():
	print("o   o")
	print("  >  ")

def print_monkey_head():
	print("( o o )")
	print("  \"  ")

def print_figure(face):
	face()
	print("  |")
	print("--|--")

choice = int(input('Enter 1=monkey, 2=human: '))
if choice == 1:
	print_figure(print_monkey_head)
elif choice == 2:
	print_figure(print_human_head)
```

Functions mainly support the **call** operation: `face()`.

---

## Dynamic typing (Python)

In Python, function parameters don’t have declared types.

That means you can pass different kinds of objects to the same function.

---

## Dynamic typing: polymorphism + runtime errors

```python
def add(x, y):
	return x + y

print(add(5, 7))
print(add("Tora", "Bora"))
print("x" * 5)

# print(add(5, "100"))  # runtime TypeError
```

Python is flexible (polymorphism), but invalid operations fail at runtime.

---

## Duck typing + static typing (super short)

- **Duck typing:** if it supports the operations you need, use it
- **Static typing (C/C++/Java):** more type checks happen before running

Takeaway: write small functions and test them with a few inputs.

---

## Reasons for defining functions (fast)

- **Readability:** main program reads like a story
- **Modular development:** build/test pieces separately
- **Avoid redundancy:** define once, call many

Beginner guideline: keep most functions under ~30 lines.

---

## Function stubs (incremental development)

We build programs **incrementally**:

- write a small amount
- test it
- add a small amount more

Function stubs help you sketch the “route” before filling in details.

```python
def steps_to_calories(num_steps):
	pass  # TODO: implement later
```

---

## Stub options

Choose how unfinished code behaves:

- do nothing (early sketch): `pass`
- warn + return a sentinel value:

```python
def steps_to_calories(steps):
	print("FIXME: finish steps_to_calories")
	return -1
```

- stop the program if it must not run yet:

```python
def get_points(num_points):
	raise NotImplementedError
```

---

## Quick practice (5 minutes)

1. Trace this call:

```python
def f(x):
	return x + 1

def g(x):
	return f(x) * 2

print(g(3))
```

2. Write `is_even(n)` and use it in a loop.

---

## Scope of variables and functions

**Scope** = where a name (variable/function) is visible and usable.

- **Local variables:** created inside a function, only usable inside that function
- **Global variables:** created outside functions, usable from that point to end of file

Key idea: a variable’s scope starts **after its first assignment**.

---

## Local variables

`total_inches` and `centimeters` exist **only inside** the function:

```python
centimeters_per_inch = 2.54
inches_per_foot = 12

def height_US_to_centimeters(feet, inches):
	"""Converts a height in feet/inches to centimeters."""
	total_inches = (feet * inches_per_foot) + inches
	centimeters = total_inches * centimeters_per_inch
	return centimeters
```

Outside the function, you can call the function, but you cannot use `total_inches`.

---

## Global variables + the `global` statement

Assigning a name inside a function creates a **local** variable by default:

```python
employee_name = "N/A"

def get_name():
	name = input("Enter employee name: ")
	employee_name = name  # local variable, does NOT change the global
```

To **rebind** (change) a global variable inside a function:

```python
employee_name = "N/A"

def get_name():
	global employee_name
	employee_name = input("Enter employee name: ")
```

Guideline: avoid globals (except constants). Globals can cause confusing side effects.

Note: `global` is required when you **assign** to a global name. Mutating a global list/dict (e.g., `my_list.append(...)`) doesn’t require `global`.

---

## Function scope + order matters

A function name exists only **after** Python evaluates the `def` statement.

```python
employee_name = "N/A"

get_name()  # NameError: get_name is not defined yet

def get_name():
	global employee_name
	employee_name = input("Enter employee name: ")
```

Common pattern: define functions first, then run your “main” code at the bottom.

---

## Namespaces

A **namespace** maps names → objects (think: a dictionary).

When Python runs `z = x + y`, it looks up `x` and `y` in a namespace, evaluates the expression, and then binds `z`.

You can inspect namespaces with:

- `globals()` (global namespace)
- `locals()` (current local namespace)

---

## Scope resolution

When Python sees a name, it searches scopes in order:

- **Local** (current function)
- **Enclosing** (outer function, if nested)
- **Global** (module/file)
- **Built-in** (`int`, `str`, `range`, ...)

If the name isn’t found: `NameError`.

---

## Same name, different namespaces

Different scopes can use the same name without conflict:

```python
tmp = 0  # global

def avg(a, b):
	tmp = a + b  # local (does NOT change the global)
	return tmp / 2

print(avg(10, 14))
print(tmp)  # still 0
```

Rule of thumb: assignment inside a function creates/modifies a **local** name unless you use `global tmp`.

---

## Function arguments (pass-by-assignment) + mutability

Python passes arguments by **object reference** (often called _pass-by-assignment_).

- Parameters become new **local names** bound to the passed objects
- If the object is **immutable** (like `int`, `str`): “modifying” usually creates a new object (no outside change)
- If the object is **mutable** (like `list`, `dict`): in-place changes are visible outside the function

Example (list mutation persists):

```python
def add_bonus(scores):
	for i in range(len(scores)):
		scores[i] += 5

nums = [80, 90]
add_bonus(nums)
print(nums)  # [85, 95]
```

Avoid side effects by passing a copy (example): `add_bonus(nums[:])`.

---

## Keyword arguments (readability)

Keyword arguments map arguments to parameters **by name**, not just position.

Helpful when a function has lots of parameters (easy to mix up):

```python
def print_book_description(title, author, publisher, year, version, num_chapters, num_pages):
	...

print_book_description(
	title="The Lord of the Rings",
	author="J. R. R. Tolkien",
	publisher="George Allen & Unwin",
	year=1954,
	version=1.0,
	num_chapters=22,
	num_pages=456,
)
```

Rule: you can mix positional + keyword arguments, but **keyword arguments must come last**.

---

## Default parameter values (+ the mutable default pitfall)

Defaults make some parameters optional:

```python
def print_date(day, month, year, style=0):
	...

print_date(30, 7, 2012)  # style defaults to 0
```

Avoid mutable defaults (they persist across calls). Use `None`:

```python
def append_to_list(value, my_list=None):
	if my_list is None:
		my_list = []
	my_list.append(value)
	return my_list
```

Keyword args + defaults let you omit _any_ defaulted parameter: `print_date(day=30, year=2012)`.

---

## Arbitrary positional arguments: `*args`

Use `*args` when you don’t know how many extra positional arguments you’ll get.

`args` becomes a **tuple** of the “extras”:

```python
def print_sandwich(bread, meat, *args):
	print(f"{meat} on {bread}", end=" ")
	if len(args) > 0:
		print("with", end=" ")
	for extra in args:
		print(extra, end=" ")
	print()

print_sandwich("sourdough", "turkey", "mayo")
print_sandwich("wheat", "ham", "mustard", "tomato", "lettuce")
```

Note: the `*` is what matters. `args` is just a common name.

---

## Arbitrary keyword arguments: `**kwargs`

Use `**kwargs` to collect extra keyword arguments into a **dict**.

```python
def print_sandwich(meat, bread, **kwargs):
	print(f"{meat} on {bread}")
	for category, extra in kwargs.items():
		print(f"\t{category}: {extra}")
	print()

print_sandwich("turkey", "sourdough", sauce="mayo")
print_sandwich("ham", "wheat", sauce1="mustard", veggie1="tomato", veggie2="lettuce")
```

Rule: `*args` / `**kwargs` must come **last** (and in that order if both are used).

---

## Multiple function outputs (tuples + unpacking)

A function can only `return` **one object**.

To return multiple values, package them into a container (commonly a **tuple**):

```python
student_scores = [75, 84, 66, 99, 51, 65]

def get_grade_stats(scores):
	mean = sum(scores) / len(scores)
	# standard deviation (population)
	tmp = 0
	for score in scores:
		tmp += (score - mean) ** 2
	std_dev = (tmp / len(scores)) ** 0.5
	return mean, std_dev  # tuple

average, standard_deviation = get_grade_stats(student_scores)  # unpacking
print(average)
print(standard_deviation)
```

Note: `return mean, std_dev` is the same as `return (mean, std_dev)`.

<!-- BOOK CONTENT INSERTS (paste excerpts any time) -->
<!--
Functions chapter:
- terminology (parameter/argument)
- local vs global variables
- default arguments (if covered)
- input validation patterns

Modules chapter:
- import mechanics
- module search path (if covered)
- packages (if covered)
-->
