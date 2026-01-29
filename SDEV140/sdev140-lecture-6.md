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

# SDEV140 Lecture 6

#### Control Structures + Debugging Mindset

**Focus:** while loops, for loops, range, loop safety, incremental development

---

<!--
## Today’s learning targets (mapped)

**2 / 2.01–2.03 (Control structures + debugging)**

- Choose and implement `while` vs `for`
- Trace loops and debug common mistakes
- Work safely with strings vs integers (especially `input()`)

**8 / 8.01–8.03 (Defensive + secure programming)**

- Use practices that prevent mistakes from becoming failures

**7 / 7.01–7.03 (Professional responsibility)**

- Understand that correctness, privacy, and honesty matter

---

## 2‑hour flow (suggested)

- **0:00–0:10** Warm-up + loop mental model
- **0:10–0:55** `while` loops (sentinel + avoiding infinite loops)
- **0:55–1:30** `for` loops + `range()` + “while vs for” decisions
- **1:30–1:50** Nested loops + `break`/`continue`
- **1:50–2:00** Debugging + defensive/ethical wrap-up

---
-->

# Part 1 — While Loops

---

## `while` loop: the idea

- Repeats **while a condition is True**
- Best when you **don’t know** how many iterations you’ll need

Pattern:

```python
while condition:
    # work
    # update something so condition can change
```

---

## `while` loop checklist (debugging)

Before you run:

- **Initialization:** starting values set?
- **Condition:** will it eventually become False?
- **Update:** does the loop body change the right variable?

If any are missing → high chance of an infinite loop.

---

## Trace this loop (class activity)

```python
value = 1
while value < 6:
    print(value)
    value = value * 2
print("Done")
```

- What prints?
- How many iterations?

<!-- Answer: 1,2,4 then Done; 3 iterations -->

---

## Sentinel loops (input-controlled)

A **sentinel value** is a special value that means “stop”.

Example:

```python
password = "star"
user_input = input("Enter the password: ")

while user_input != password:
    print("Wrong password. Try again.")
    user_input = input("Enter the password: ")

print("Access granted.")
```

---

## Defensive sentinel loop pattern

Two common safety upgrades:

- Normalize input (`strip()`, maybe case handling)
- Avoid crashing on bad input

Example:

```python
sentinel = "q"
cmd = ""
while cmd != sentinel:
    cmd = input("Enter command (q to quit): ").strip()
```

---

## Infinite loops (common bug)

Infinite loops happen when:

- Condition is always True, or
- Update never changes the condition

Example bug:

```python
score = 1
while score > 0:
    score = score * 2
```

Fix idea: change the condition or update so it can end.

---

## Quick practice

1. Write a loop condition that continues while `in_val` is not `"q"`.

```python
in_val = ""
while __________________:
    in_val = input()
```

<!-- Answer: while in_val != "q": -->

---

# Part 2 — For Loops + range()

---

## `for` loop: the idea

- Iterates through a **container** (list/string/dict)
- Best when the number of items is **known** (or comes from the container)

```python
for item in container:
    # work
```

---

## `for` loop examples

```python
# list (elements)
for name in ["Kai", "Sam", "Alex"]:
    print(name)

# strings (characters)
for ch in "Yes":
    print(ch)

# dictionaries (keys)
channels = {"MTV": 35, "CNN": 28}
for c in channels:
    print(c, channels[c])
```

---

## Accumulator pattern (super common)

```python
total = 0
for day in daily_revenues:
    total += day
average = total / len(daily_revenues)
```

Key idea: initialize accumulator **before** the loop.

---

## `range()` essentials

`range(end)` generates 0…end-1

```python
for i in range(3):
    print(i)
# 0 1 2
```

`range(start, end, step)`

```python
for i in range(10, 0, -2):
    print(i)
# 10 8 6 4 2
```

---

## `range()` mistakes to watch for

- End value is **excluded**
- Step sign must match direction
- This never runs:

```python
for i in range(10, 0):
    print(i)
```

---

## While vs For (decision rule)

Use `for` when:

- Counting a fixed number of times
- Traversing a container

Use `while` when:

- Stopping on a condition / sentinel
- You don’t know the iteration count ahead of time

---

## Quick practice (choose the loop)

1. Keep asking until user types `q`
2. Repeat exactly 1500 times
3. Keep updating `x` and `y` until they’re equal

<!-- Suggested: while, for, while -->

---

# Part 3 — Nested Loops + break/continue

---

## Nested loops (what to know)

- Inner loop runs **fully** for each outer loop iteration
- Total inner executions = outer × inner

```python
for i in range(2):
    for j in range(3):
        print(i, j)
```

---

## `break` vs `continue`

- `break`: exit the **nearest** loop early
- `continue`: skip to the **next iteration**

Use them only when they make intent clearer.

---

## `break` example (search)

```python
nums = [5, 9, 2, 9]
found = False

for n in nums:
    if n == 2:
        found = True
        break

print(found)
```

---

## `continue` example (filter)

```python
for n in [3, -1, 7, 0, 4]:
    if n <= 0:
        continue
    print(n)
```

---

# Part 4 — Incremental Development + Professional/Defensive Practices

---

## Develop programs incrementally (debug faster)

Workflow:

1. Make a tiny version that works
2. Add one feature
3. Test
4. Repeat

Rule: don’t add 5 changes before testing once.

---

## Debugging habits (what “good” looks like)

- Reproduce the bug reliably
- Reduce to a small test case
- Print/log variables at key points
- Check types (`type(x)`) when things look weird
- Verify edge cases (empty input, 0, negatives)

---

## Defensive programming (Objective 8)

High-value habits that prevent failures:

- Validate input (type, range, empty strings)
- Handle “nothing entered” / `0 items` cases
- Avoid assumptions (“user always types an int”)
- Prefer clear conditions that obviously terminate

---

## Professional responsibility (Objective 7)

As an IT professional, your code choices affect people:

- Be honest about what your program does/doesn’t do
- Don’t misuse or expose private data
- Follow rules and policies (school, workplace, laws)

(Short reminder today: writing “safe” loops and validating input is part of professionalism.)

---

## Secure mindset: SSDLC (Objective 8.03)

Even small programs benefit from a mini secure lifecycle:

- **Plan:** what inputs exist, what could go wrong?
- **Build:** validate inputs, handle errors
- **Test:** include edge cases and “bad” input
- **Review:** can someone crash it or trick it?

---

## Wrap-up (what you should be able to do)

- Write and trace `while` loops (including sentinel loops)
- Explain and avoid infinite loops
- Use `for` loops to traverse containers
- Use `range()` correctly (end exclusive)
- Use `break`/`continue` intentionally
- Debug with small steps and good test cases

---

## Module 3: Lecture Activity (5 minutes)

Write a program that:

- Reads integers until the user enters `0`
- Prints the count of numbers entered
- Prints the maximum number entered

(What happens if the first input is `0`?)

---

# TKinter (Graphic User Interfaces)

---

## TKinter: one mental model

- `Tk()` creates the window
- A `Canvas` draws shapes
- Coordinates start at **(0,0)** top-left

---

## Minimal rectangle demo

```python
import tkinter as tk

root = tk.Tk()
root.geometry("400x250")
root.title("Canvas Demo")

canvas = tk.Canvas(root)
canvas.pack(fill="both", expand=True)

canvas.create_rectangle(10, 10, 160, 60, outline="blue", fill="pink")

root.mainloop()
```
