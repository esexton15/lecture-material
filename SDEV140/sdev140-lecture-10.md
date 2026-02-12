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

# SDEV140 Lecture 10

#### Modules + Exceptions

**Focus:** reuse code with modules, handle errors with exceptions

---

## Today’s outcomes

By the end of class you can:

- Explain what a module is and why it helps
- Import modules and use their definitions safely
- Describe how the import process works at a high level
- Use exceptions to handle errors (coming next)

---

# Part 1 — Modules

---

## Module basics

- A **script** is a Python file you run.
- A **module** is a Python file you import and reuse.

Modules help you:

- avoid repeating the same functions
- keep scripts shorter and easier to maintain

---

## Module file naming

- Module files must end in `.py`
- The module name matches the filename **without** `.py`

Example:

- filename: `HTTPServer.py`
- import: `import HTTPServer`

Imports are **case-sensitive**.

---

## Where Python looks for modules

Simplest rule: keep the module in the **same folder** as the script.

Python can also search other locations (covered later).

---

## Import statements: placement

Good practice: put imports **at the top** of the file.

Benefits:

- readers can see dependencies quickly
- easier to troubleshoot missing modules

---

## What happens during import

When you run `import module_name`:

1. Python checks if the module is already loaded
2. If not, a **module object** is created and added to `sys.modules`
3. The module code executes in its own namespace
4. The module is made available to the importer

---

## `sys.modules` (import cache)

- `sys.modules` is a dictionary of loaded modules
- If a module is already there, Python reuses it

This avoids re-running the same module code multiple times.

---

## Using an imported module

Use **attribute access** to reach definitions:

```python
import HTTPServer

my_ip = HTTPServer.address
```

You can also overwrite values locally:

```python
HTTPServer.address = "www.yahoo.com"
```

This change is only for the current Python run.

---

## Example module: `my_funcs.py`

```python
def factorial(num):
	"""Calculates and returns the factorial (num!)"""
	x = 1
	for i in range(1, num + 1):
		x *= i

	return x
```

---

## Using `my_funcs.factorial`

```python
import my_funcs

n = int(input("Enter number: "))
fact = my_funcs.factorial(n)

for i in range(1, n + 1):
	print(i, end=" ")
	if i != n:
		print("*", end=" ")

print(f"= {fact}")
```

---

# Part 1b - Finding modules

---

## How Python finds modules

When you run `import name`, Python searches in this order:

1. **Built-in modules** (pre-installed)
2. Directories in `sys.path`

Built-in examples: `sys`, `time`, `math`.

---

## Built-in name conflicts

If you name your file `math.py`, Python will load the **built-in** `math` first.

Avoid naming your modules after standard libraries.

---

## `sys.path` (module search path)

`sys.path` is a list of directories Python searches for modules.

It starts with:

- the script's directory
- directories in the `PYTHONPATH` environment variable
- the Python install directory

---

## `PYTHONPATH` (for bigger projects)

`PYTHONPATH` is an operating system environment variable.

It lets you add extra directories so Python can find modules.

Use it for larger projects with many folders or shared modules.

---

# Part 1c - Importing specific names

---

## Import specific names

You can import only what you need:

```python
from module_name import name1, name2
```

This copies **only those names** into your namespace.

---

## `import` vs. `from ... import`

**Import entire module:**

```python
import HTTPServer
print(HTTPServer.address)
```

**Import a specific name:**

```python
from HTTPServer import address
print(address)
```

---

## Example: importing specific names

```python
from math import sqrt, pi

radius = 5
area = pi * radius * radius
print(sqrt(area))
```

---

## `import *` (use with caution)

```python
from HTTPServer import *
```

Why avoid it in scripts/modules:

- hides where names come from
- makes dependencies unclear
- easier to create name conflicts

OK for interactive use, not for programs.

---

# Part 1d - Executing modules as scripts

---

## Import side effects

`import` **executes** the module code.

If a module has top-level `print()` or `input()`, those run on import.

That can cause **unintended behavior**.

---

## The problem (example)

If `WebSearch.py` runs a prompt at top level, then:

- running `WebSearch.py` works
- importing it from another script triggers a prompt too

We want a file to work as **both**:

- a script (when executed)
- a module (when imported)

---

## The `__name__` guard

Every module gets a `__name__` value.

- imported module: `__name__ == "WebSearch"`
- executing script: `__name__ == "__main__"`

Use this pattern:

```python
if __name__ == "__main__":
    # run the script UI
```

---

# Part 1e - Reloading modules

---

## Why reload a module?

Modules execute **once** when imported.

If you change the module source while a long program is running,
those changes won’t show up unless you reload.

Use case: long-running scripts or servers.

---

## `importlib.reload()`

`reload()` re-executes the module code **in place**.

```python
from importlib import reload
import my_module

reload(my_module)
```

The module object stays the same, but its definitions update.

---

## Example: reload on file change (concept)

```python
import os
from importlib import reload
import send_gmail

mod_time = os.path.getmtime(send_gmail.__file__)

# ... work loop ...
last_mod = os.path.getmtime(send_gmail.__file__)
if last_mod > mod_time:
	mod_time = last_mod
	reload(send_gmail)
```

---

## What changes after reload

If `send_gmail.py` changes `header`, then:

- `send_gmail.header` updates after reload
- calls like `send_gmail.send(...)` use the new definition

This lets you change behavior **without restarting** the program.

---

## Important caveat: `from ... import`

If you import a name directly:

```python
from send_gmail import header
```

That **name does not update** after `reload(send_gmail)`.

Use `import module` when you plan to reload.

---

# Part 1f - Packages

---

## What is a package?

A **package** is a directory of modules you can import.

Use packages to:

- group related modules
- organize large projects
- avoid name collisions

---

## `__init__.py`

A directory is a package if it contains `__init__.py`.

That file can be empty or import submodules.

Python searches for packages in `sys.path`.

---

## Example structure (ASCIIArt)

```
draw_scene.py
ASCIIArt/
	__init__.py
	canvas.py
	figures/
		__init__.py
		man.py
		cow.py
	buildings/
		__init__.py
		barn.py
		house.py
```

---

## Import the package

```python
import ASCIIArt
```

This loads the package so you can reach submodules.

---

## Import a module inside a package

```python
import ASCIIArt.canvas

ASCIIArt.canvas.draw_canvas()
```

Use the full path to access names.

---

## `from` with packages

```python
from ASCIIArt.figures import cow

cow.draw()
```

This lets you omit the full package path.

---

## Import a specific name

```python
from ASCIIArt.figures.cow import draw

draw()
```

With `from x.y import z`, `z` can be a module **or** a name.

---

## Avoid name collisions

Packages prevent conflicts:

- `ASCIIArt.canvas` vs. `3DGraphics.canvas`

Be careful with `from` imports if two modules share names.

---

# Part 1g - Standard library

---

## Python standard library

Python ships with built-in modules for common tasks.

Before writing new code, check if the standard library already helps.

---

## Common standard library modules

- `datetime` (dates/times)
- `random` (random values)
- `math` (math functions)
- `time` (sleep, time values)
- `os` (files and OS info)
- `sys` (system config)
- `sqlite3` (databases)
- `urllib` (URLs/web)
- `pdb` (debugger)

---

## Example: `datetime`

```python
import datetime

today = datetime.date.today()
days_from_now = int(input("Enter number of days from now: "))
day_difference = datetime.timedelta(days=days_from_now)
future_date = today + day_difference

print(f"{days_from_now} days from now is {future_date}")
```

---

## Example: `random`

```python
import random

deck = [2, 3, 4, 5, 6, 7, 8, 9, 10, "J", "Q", "K", "A"] * 4
random.shuffle(deck)

card = random.choice(deck)
print("Card drawn:", card)
```

---

# Part 2 — Exceptions

---

## Why exceptions exist

Some errors happen **at runtime** (bad input, missing files, etc.).

Without handling, the program stops and prints a traceback.

Goal: handle errors **gracefully** and keep running.

---

## Example: BMI without handling (crashes)

```python
weight = int(input("Enter weight (in pounds): "))
height = int(input("Enter height (in inches): "))

bmi = (float(weight) / float(height * height)) * 703
print(f"BMI: {bmi}")
```

Bad input like "One-hundred fifty" raises `ValueError`.

---

## try/except (basic idea)

```python
try:
	# code that might fail
except:
	# run if any error occurs
```

`try` runs the normal code; `except` handles the error.

---

## try/except control flow

- Python executes the `try` block first.
- If **no exception** occurs, `except` is skipped.
- If an **exception** occurs, `except` runs.
- Any remaining statements in the `try` block are skipped.

Execution continues **after** the `except` block.

---

## BMI with try/except

```python
try:
	weight = int(input("Enter weight (in pounds): "))
	height = int(input("Enter height (in inches): "))

	bmi = (float(weight) / float(height * height)) * 703
	print(f"BMI: {bmi}")
	print("(CDC: 18.6-24.9 normal)\n")
except:
	print("Could not calculate health info.\n")
```

Now the program keeps running after bad input.

---

## When to use try/except

- user input that might be invalid
- file/network operations that might fail
- conversions (`int()`, `float()`) that can throw errors

Keep the `try` block small and focused.

---

## Multiple exception handlers

One `try` block can have **multiple** `except` blocks.

Use specific exception types so each error can be handled differently.

---

## Multiple `except` blocks (pattern)

```python
try:
	# normal code
except ExceptionType1:
	# handle one type
except ExceptionType2:
	# handle another type
```

Avoid a catchall `except:` unless you truly need it.

---

## BMI with two handlers

```python
try:
	weight = int(input("Enter weight (in pounds): "))
	height = int(input("Enter height (in inches): "))

	bmi = (float(weight) / float(height * height)) * 703
	print(f"BMI: {bmi}")
	print("(CDC: 18.6-24.9 normal)\n")
except ValueError:
	print("Could not calculate health info.\n")
except ZeroDivisionError:
	print("Invalid height entered. Must be > 0.")
```

---

## Grouping exception types

Use a tuple when multiple types share one handler:

```python
try:
	# ...
except (ValueError, TypeError):
	# handle either ValueError or TypeError
except (NameError, AttributeError):
	# handle either NameError or AttributeError
```

If no handler matches, the exception is unhandled and the program stops.

---

## Raising exceptions

Sometimes you detect a problem yourself.

Use `raise` to stop normal flow and jump to `except`.

This keeps the main logic clean and readable.

---

## Why `raise` helps

Without exceptions, you may add many `if/else` checks that:

- clutter the main logic
- repeat conditions in multiple places
- make bugs more likely

With `raise`, the flow stays clear.

---

## BMI with `raise` + `except as`

```python
try:
	weight = int(input("Enter weight (in pounds): "))
	if weight < 0:
		raise ValueError("Invalid weight.")

	height = int(input("Enter height (in inches): "))
	if height <= 0:
		raise ValueError("Invalid height.")

	bmi = (float(weight) * 703) / (float(height * height))
	print(f"BMI: {bmi}")
	print("(CDC: 18.6-24.9 normal)\n")
except ValueError as excpt:
	print(excpt)
	print("Could not calculate health info.\n")
```

---

## `except ... as` (details)

`as` binds the exception object to a variable:

```python
except ValueError as excpt:
	print(excpt)
```

`excpt` contains the message passed to `raise`.

---

## Exceptions with functions

If a function raises an exception and doesn’t handle it:

- the function exits immediately
- Python looks for a handler in the **calling code**
- it keeps moving up the call stack until one is found

---

## Why this is useful

Functions can stay clean and focused.

They don’t need special error return values like `-1`.

The caller decides how to handle failures.

---

## BMI with helper functions

```python
def get_weight():
	weight = int(input("Enter weight (in pounds): "))
	if weight < 0:
		raise ValueError("Invalid weight.")
	return weight

def get_height():
	height = int(input("Enter height (in inches): "))
	if height <= 0:
		raise ValueError("Invalid height.")
	return height

user_input = ""
while user_input != "q":
	try:
		weight = get_weight()
		height = get_height()

		bmi = (float(weight) / float(height * height)) * 703
		print(f"BMI: {bmi}")
		print("(CDC: 18.6-24.9 normal)\n")
	except ValueError as excpt:
		print(excpt)
		print("Could not calculate health info.\n")

	user_input = input('Enter any key ("q" to quit): ')
```

---

## Using `finally` for cleanup

Sometimes you need code to run **no matter what**.

Use `finally` for cleanup actions like closing files.

---

## `finally` behavior (summary)

`finally` runs:

- if no exception occurs
- after a handled exception
- even after an unhandled exception (then it re-raises)
- even if `break`, `continue`, or `return` exits the try block

`finally` always runs last.

---

## Example: file read with cleanup

```python
nums = []
rd_nums = -1
my_file = input("Enter file name: ")

try:
	print("Opening", my_file)
	rd_nums = open(my_file, "r")  # Might cause IOError

	for line in rd_nums:
		nums.append(int(line))  # Might cause ValueError
except IOError:
	print(f"Could not find {my_file}")
except ValueError:
	print(f"Could not read number from {my_file}")
finally:
	print(f"Closing {my_file}")
	if rd_nums != -1:
		rd_nums.close()
	print(f"Numbers found: {' '.join([str(n) for n in nums])}")
```

---

## Custom exception types

You can define your own exception classes when built-ins are not specific enough.

Custom exceptions help you **signal and handle** unique errors.

---

## Define and raise a custom exception

```python
class LessThanZeroError(Exception):
	def __init__(self, value):
		self.value = value

my_num = int(input("Enter number: "))

if my_num < 0:
	raise LessThanZeroError("my_num must be greater than 0")
else:
	print(f"my_num: {my_num}")
```

---

## Custom exception tips

- Inherit from `Exception`.
- Keep the class minimal.
- End the name with `Error` (convention).

Custom exception types are common in large projects and libraries.
