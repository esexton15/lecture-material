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

# SDEV140 Lecture 7

#### Chapter 8 — Conditionals (if / elif / else)

**Focus:** decision-making in code, ranges, logical operators, common comparison/indentation errors

<!-- ---

## This week’s objectives (mapped)

**2 / 2.01–2.03 (Control structures + debugging)**

- Execute and debug a program using control structures
- Use variables/constants with correct types
- Avoid common strings vs integers mistakes (`input()`)

**Next lecture (this week): Objective 3 (Functions + modularization)**

- Abstraction and modularization with `def`, parameters, and return values
- Breaking problems into smaller pieces

--- -->
<!--
## 2‑hour flow (suggested)

- **0:00–0:10** Warm-up: “What is a branch?”
- **0:10–0:45** Core patterns: `if`, `if/else`, `if/elif/else`
- **0:45–1:15** Ranges: relational operators, chaining, and logical ops
- **1:15–1:45** Common errors: types, indentation, precedence
- **1:45–2:00** Practice + exit ticket -->

---

# Part 1 — Branching concept

---

## Branching (real-world analogy)

Think like a restaurant host:

- If party is **1** → seat at the **counter**
- Else if party is **2** → seat at a **small table**
- Else (party ≥ 3) → seat at a **large table**

Key idea: **only one path runs** (if/elif/else).

---

## Restaurant seating (Python sketch)

```python
party = int(input("Party size? "))

if party == 1:
	print("Counter")
elif party == 2:
	print("Small table")
else:
	print("Large table")
```

---

# Part 2 — if branches (single decision)

---

## What is an `if` branch?

- A **branch** is code that runs **only when a condition is True**
- Condition is a **Boolean expression** (evaluates to `True` or `False`)

Pattern:

```python
if condition:
	# runs only if condition is True
```

---

## Example: Senior hotel discount (`if`)

```python
hotel_rate = 155
user_age = int(input("Age? "))

if user_age > 65:
	hotel_rate = hotel_rate - 20

print("Your rate:", hotel_rate)
```

---

## Practice: trace the hotel rate

1. If `user_age` is 20: does the `if` run? What prints?
2. If `user_age` is 70: what prints?
3. Do the output lines run for all ages?

<!-- 1) no, 155  2) 135  3) yes -->

---

## Strings vs integers

`input()` returns a **string**.

Bug:

```python
age = input("Age? ")
if age > 65:
	print("Discount")
```

What could we do to fix this code?

---

## Strings vs integers The Fix

Fix:

1. Convert input to `int`:
2. Handle non-numeric input (optional but recommended)

```python
user_input = input("Age? ")
if not user_input.isnumeric(): # handle non-numeric input
	print("Invalid age")
	exit()

age = int(user_input) # convert string to int
if age > 65:
	print("Discount")
```

---

# Part 2.5 — Equality & inequality (Chapter 8.2)

---

## `=` vs `==` (assignment vs comparison)

- `=` **assigns** a value to a variable
- `==` **compares** two values (results in `True` or `False`)

Example:

```python
x = 5      # assignment
print(x == 5)  # comparison -> True
```

---

## Equality operators (Boolean results)

- `a == b` is `True` if equal
- `a != b` is `True` if different

```python
x = 3
print(x == 3)  # True
print(x != 3)  # False
print(x != 4)  # True
```

---

# Examples

<!--
## Example: 50th anniversary hotel discount

```python
hotel_rate = 150
num_years = int(input("Enter years married: "))

if num_years == 50:
	print("Congratulations on 50 years of marriage!")
	hotel_rate = hotel_rate / 2

print(f"Your hotel rate: ${hotel_rate:.2f}")
```

---

## Example: even vs odd (`if/else` + `%`)

```python
user_num = int(input("Enter a number: "))
div_remainder = user_num % 2

if div_remainder == 0:
	print(f"{user_num} is even.")
else:
	print(f"{user_num} is odd.")
``` -->

---

## Quick practice: True or False?

Assume `x = 5` and `y = 7`.

1. `x == 5` → **\_\_**
2. `x == y` → **\_\_**
3. `y != 99` → **\_\_**

<!-- True, False, True -->

---

# Part 3 — if/else branches (two paths)

---

## `if/else`: exactly one runs

Pattern:

```python
if condition:
	# true branch
else:
	# false branch
```

Useful when you need a value set either way.

---

## Example: insurance price (`if/else`)

```python
user_age = int(input("Age? "))

if user_age < 25:
	insure_price = 4800
else:
	insure_price = 2200

print("Annual price: $", insure_price)
```

1. `user_age = 18` → price = **\_\_**
2. `user_age = 30` → price = **\_\_**
3. `user_age = 25` → price = **\_\_**

<!-- ---

## Example: max of two values

```python
x = int(input("x? "))
y = int(input("y? "))

if x > y:
	max_val = x
else:
	max_val = y

print(max_val)
``` -->

---

# Part 4 — if/elif/else

---

## `if/elif/else` rules

- Conditions are checked **top to bottom**
- The **first True** condition wins
- `else` runs only if **none** were True
- `else` is optional

---

## Example: anniversaries (`if/elif/else`)

```python
years = int(input("Years married? "))

if years == 1:
	print("Newlyweds")
elif years == 25:
	print("Silver")
elif years == 50:
	print("Golden")
else:
	print("Congrats")
```

---

## Practice: what prints?

Using the anniversaries example:

1. years = 1 → **\_\_**
2. years = 50 → **\_\_**
3. years = 2 → **\_\_**

<!-- Newlyweds, Golden, Congrats -->

---

## Ordering matters

If you write:

```python
if years >= 1:
	print("Congrats")
elif years == 1:
	print("Newlyweds")
```

The `elif` never runs.

---

# Part 4.5 — Detecting ranges

---

## Detecting ranges with `if/elif/else`

A common task: do different actions depending on what _range_ a number falls into.

Key idea:

- If the code reaches an `elif`, you already know all earlier conditions were **False**
- That gives you an **implicit lower bound**

---

## Example: soccer teams by age

```python
age = int(input("Age? "))

if age < 6:
	print("No teams")
elif age < 8:
	print("U8 team")
elif age < 10:
	print("U10 team")
elif age < 12:
	print("U12 team")
else:
	print("No teams")
```

Read it as increasing “cutoffs”.

---

## Practice: what ages map to each branch?

Using the soccer example:

- `elif age < 8` covers ages **\_\_**
- `elif age < 10` covers ages **\_\_**
- `elif age < 12` covers ages **\_\_**

<!-- 6-7, 8-9, 10-11 -->

---

## Applied example: insurance price (ranges)

```python
user_age = int(input("Age? "))

if user_age < 16:
	insurance_price = 0
	print("Too young.")
elif user_age < 25:
	insurance_price = 4800
elif user_age < 40:
	insurance_price = 2350
else:
	insurance_price = 2100

print("Annual price: $", insurance_price)
```

---

## Range logic pitfall: out-of-order tests

This is **not** reasonable:

```python
if x < 100:
	...
elif x < 200:
	...
elif x < 150:
	...
else:
	...
```

Why?

---

## Range logic pitfall: out-of-order tests

This is **not** reasonable:

```python
if x < 100:
	...
elif x < 200:
	...
elif x < 150:
	...
else:
	...
```

Why? The `x < 150` branch can never happen (anything <150 already matched earlier).

---

# Part 4.6 — Relational operators + chaining (Chapter 8.4)

---

## Relational operators (comparisons)

These compare two values and evaluate to `True` or `False`.

| Operator | Meaning               | Example (`x = 3`) |
| -------- | --------------------- | ----------------- |
| `<`      | less than             | `x < 4` → True    |
| `>`      | greater than          | `x > 3` → False   |
| `<=`     | less than or equal    | `x <= 3` → True   |
| `>=`     | greater than or equal | `x >= 4` → False  |

Only these two-character operators are valid: `<=` and `>=`.

---

## Quick check: True/False + valid syntax

Assume `x = 5` and `y = 7`.

1. `x <= 7` → **\_\_**
2. `y >= 7` → **\_\_**
3. Is `x <> y` valid Python? **\_\_**
4. Is `x =< y` valid Python? **\_\_**

<!-- True, True, No, No -->

---

## Operator chaining (Python feature)

Python supports chained comparisons:

```python
# x is less than y but greater than z
if z < x < y:
	print("in between")
```

Common pattern:

```python
if 0 <= x < 100:
	print("x is 0..99")
```

---

## Example: grade range with chaining

```python
grade = int(input("Grade level (0-12)? "))

if 9 <= grade <= 12:
	print("in high school")
else:
	print("not in high school")
```

---

# Part 4.7 — Logical operators (Chapter 8.5)

---

## Logical operators: `and`, `or`, `not`

Logical operators combine or flip Boolean expressions.

- `a and b` → True only if **both** are True
- `a or b` → True if **either** is True (or both)
- `not a` → flips True/False

Python uses **lowercase** keywords: `and`, `or`, `not`.

---

## Quick evaluation (x = 7, y = 9)

```python
x = 7
y = 9

print((x > 5) and (y < 20))   # ?
print((x > 10) or (y < 20))  # ?
print(not (x > 10))          # ?
```

<!-- True, True, True -->

---

## Detecting “inside a range” with `and`

Example: “x is between 10 and 15 (exclusive)”

```python
if (x > 10) and (x < 15):
	print("11–14")
```

Even better in Python (chaining from 8.4):

```python
if 10 < x < 15:
	print("11–14")
```

---

## Detecting “outside a range” with `or`

Example: “x is less than -5 **or** greater than 10”

```python
if (x < -5) or (x > 10):
	print("out of bounds")
```

---

## Example: TV channel type (explicit ranges)

Standard channels: 2–499

HD channels: 1002–1499

```python
user_channel = int(input("Channel? "))

if (user_channel >= 2) and (user_channel <= 499):
	channel_type = "s"
elif (user_channel >= 1002) and (user_channel <= 1499):
	channel_type = "h"
else:
	channel_type = "e"

print(channel_type)
```

---

## Implicit vs explicit ranges (when to use which)

If ranges are **continuous with no gaps**, you can often use implicit cutoffs:

```python
if x < 0:
	...
elif x <= 10:
	...
elif x <= 20:
	...
else:
	...
```

<!-- If ranges have **gaps** or separate blocks, use explicit `and` ranges. -->

---

# Part 4.8 — Detecting ranges with gaps (Chapter 8.6)

---

## Ranges with gaps (the “discount groups” pattern)

Example: movie ticket discounts for:

- Children: age **≤ 12**
- Seniors: age **≥ 65**

Gap: ages **13–64** (regular price)

---

## Example: movie ticket pricing (gap in the middle)

```python
age = int(input("Age? "))

if (age <= 12) or (age >= 65):
	price = 8
else:
	price = 12

print("Ticket price: $", price)
```

_Practice: For movie tickets above, which ages get the discount? **\_\_**_

<!-- ages 0-12 and 65+ -->

---

## Multiple valid ranges (two separate blocks)

Example: valid office numbers are 100–150 **or** 200–250.

```python
office = int(input("Office number? "))

valid = (100 <= office <= 150) or (200 <= office <= 250)

if valid:
	print("Valid office")
else:
	print("Invalid office")
```

1. For office numbers above, is 175 valid? **\_\_**
2. For office numbers above, is 225 valid? **\_\_**
<!-- No, Yes -->

---

# Part 4.9 — Multiple features with branches (Chapter 8.7)

---

## Multi-branch vs multiple `if` statements

These can look similar but mean different things:

- `if / elif / else`: **at most one** branch runs
- multiple separate `if`s: **more than one** branch can run

---

## Example: multiple independent `if` statements

Goal: print every “feature” that applies.

```python
temp = int(input("Temp? "))

if temp <= 32:
	print("freezing")

if temp >= 90:
	print("hot")

if temp % 2 == 0:
	print("even number")
```

If `temp = 92`, the output includes **hot** and **even number**.

---

## Same idea, but with `if/elif/else` (only one)

```python
temp = int(input("Temp? "))

if temp <= 32:
	print("freezing")
elif temp >= 90:
	print("hot")
else:
	print("normal")
```

This is for **choosing one category**, not listing multiple features.

---

## Nested `if` statements (nested branches)

Branches can contain other branches.

Example: validate age, then choose price.

```python
age = int(input("Age? "))

if age < 0:
	print("Invalid age")
else:
	if age <= 12:
		print("Child price")
	elif age >= 65:
		print("Senior price")
	else:
		print("Regular price")
```

---

# Part 5 — Debugging conditionals (2.01–2.03)

---

## Code blocks & indentation (Chapter 8.11)

- A **code block** is a grouped set of statements
- In Python, blocks are defined by **indentation level**
- A new block usually starts after a line ending with `:` (like `if`, `elif`, `else`, `for`, `while`, `def`)

Best practice: **4 spaces per indent level**.

---

## Example: where blocks begin

```python
age = int(input("Age? "))

if age < 0:                 # block starts
	print("Invalid")
else:                       # new block starts
	if age <= 12:           # nested block starts
		print("Child")
	else:
		print("Not a child")

print("Done")               # back to outermost level
```

---

## Common indentation errors

Typical messages:

- `IndentationError: unexpected indent`
- `IndentationError: unindent does not match any outer indentation level`
- `IndentationError: expected an indented block`

Most common cause: **mixing tabs and spaces**.

---

## Tabs vs spaces (rule)

- Never mix tabs and spaces in the same program
- Configure editors to insert **spaces** when you press Tab
- Keep indentation consistent inside each block

---

## Special case: long lines wrapping

Wrapping a long statement does **not** create a new block.

Common approach: wrap inside parentheses:

```python
if (
	(age >= 0)
	and (age <= 12)
	and (member_status == "active")
):
	print("Child member")
```

---

## Common mistakes to watch for

- Using `=` instead of `==` (Python will error)
- Missing `:` after `if`/`elif`/`else`
- Indentation problems (code ends up in the wrong branch)
- Wrong type from `input()` (string vs int)
- Off-by-one boundaries (`<` vs `<=`)

---

## Comparing data types (Chapter 8.8)

- If both values are **numbers**, comparisons are arithmetic (`5 < 2` is False)
- If both values are **strings**, comparisons are lexicographic (character-by-character)
- Comparing different types like `1 < "abc"` raises `TypeError`

---

## Strings: equality is case-sensitive

```python
day = "Tuesday"
print(day == "Tuesday")  # True
print(day == "tuesday")  # False
```

Common pattern for case-insensitive checks:

```python
cmd = input("Command? ").strip().lower()
if cmd == "quit":
	print("bye")
```

---

## Don’t compare floats with `==`

Floating-point numbers are approximations.

```python
print(0.1 + 0.2 == 0.3)  # often False
```

Better:

```python
import math
print(math.isclose(0.1 + 0.2, 0.3))
```

---

## Common operator errors (fast fixes)

- Use `==` for equality, not `=`
- Valid: `<=` and `>=` (exactly these)
- Invalid in Python: `<>`, `=<`, `=>`, `!<`

---

## Membership operators: `in` / `not in` (Chapter 8.9)

Use membership operators to ask: “Is this value in that container?”

They evaluate to `True` or `False`.

---

## `in` with lists and strings

List membership:

```python
colors = ["red", "green", "blue"]
print("green" in colors)      # True
print("purple" not in colors) # True
```

String membership (substring):

```python
print("abc" in "123abcd")  # True
```

---

## `in` with dictionaries checks KEYS

```python
channels = {"CNN": 28, "NBC": 4}

print("CNN" in channels)   # True (key exists)
print(28 in channels)      # False (NOT checking values)
print(28 in channels.values())  # True
```

---

## Identity operators: `is` / `is not`

`==` compares values. `is` compares whether two names refer to the **same object**.

Good use (common in Python):

```python
result = None
if result is None:
	print("no result yet")
```

Avoid using `is` to compare numbers/strings (can behave inconsistently).

---

## Order of evaluation (precedence) — Chapter 8.10

When an expression has multiple operators, Python follows precedence rules.

High-level order (most common for this chapter):

1. Parentheses `( )`
2. Arithmetic `* / %` then `+ -`
3. Comparisons: `< <= > >= == != in not in`
4. `not`
5. `and`
6. `or`

Rule of thumb: **when in doubt, add parentheses**.

---

## Precedence example

```python
# and binds tighter than or
if x == 5 or y == 10 and z != 10:
	...
```

This means:

```python
if (x == 5) or ((y == 10) and (z != 10)):
	...
```

---

## Common error: missing parentheses

These often don’t mean what beginners expect:

```python
not a == b
```

Interpreted as:

```python
not (a == b)
```

If you mean “not equal”, prefer:

```python
a != b
```

---

## Another common error

```python
w and x == y and z
```

Interpreted like:

```python
(w and (x == y)) and z
```

If you want a specific grouping, write it with parentheses.

---

## Conditional expressions (ternary) — Chapter 8.12

Form:

```python
expr_when_true if condition else expr_when_false
```

The `condition` is evaluated first.

Example:

```python
x = 2
value = 5 if x == 2 else 9 * x
print(value)
```

---

## When to use conditional expressions

Good practice: keep them **simple** and typically in **assignments**.

Readable example:

```python
status = "adult" if age >= 18 else "minor"
```

If it’s getting long/complex, prefer a normal `if/else` block for clarity.

---

## Debugging habit: test the boundaries

For `if age < 25` test:

- 24 (true branch)
- 25 (false branch)
- 26 (false branch)

If your results surprise you, your condition is probably wrong.

---

# Wrap-up

---

## What you should be able to do (today)

- Write `if`, `if/else`, and `if/elif/else`
- Detect ranges with increasing cutoffs
- Use `and` / `or` / `not` (and chaining like `0 <= x < 100`)
- Avoid common bugs: type mismatches, indentation mistakes, precedence surprises

---

## Next lecture (this week)

- Turn repeated decision logic into **functions**
- Introduce **modules**: importing and organizing code across files
