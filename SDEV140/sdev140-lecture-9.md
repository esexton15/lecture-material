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

section {
	font-size: 1.95rem;
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

# SDEV140 Lecture 9

#### Troubleshooting & Debugging Process

**Focus:** a repeatable process for finding + fixing bugs

---

## Today’s outcomes

By the end of class you can:

- Describe a step-by-step troubleshooting process
- Reproduce a bug and capture good evidence (inputs, outputs, environment)
- Use traceback messages to locate the _first useful_ error line
- Form a hypothesis, run a test, and repeat systematically
- Use knowledge to create multiple hypotheses and prioritize what to test first
- Prevent regressions with a small set of re-tests

---

<!-- ## 2‑hour flow (suggested)

- **0:00–0:10** Warm‑up: “What’s the bug?” mini scenarios
- **0:10–0:30** Troubleshooting basics: hypotheses + tests
- **0:30–0:55** Reading tracebacks + common error categories
- **0:55–1:25** Debugging tools: print checks + isolating with minimal examples
- **1:25–1:55** Guided practice: fix 3 bugs (increasing difficulty)
- **1:55–2:00** Wrap‑up: habits checklist

--- -->

<!--
# Warm‑up

---

## Warm‑up: “Is this a bug report?”

Which is more helpful?

1) “My code doesn’t work.”

2) “When I enter `-5` for age, the program crashes with `ValueError` on the `int(input(...))` line.”

Goal: learn to produce **actionable** bug reports.

---

## What to capture (every time)

- Exact input(s)
- What you expected
- What actually happened
- Full error message / traceback (copy/paste)
- What you changed right before it broke

---

-->

# Part 1 — The troubleshooting loop

---

## Introduction to troubleshooting

Everyday systems have problems:

- a lamp suddenly turns off
- a smartphone won’t charge
- a car won’t start

When a problem happens, many people try random actions.

Troubleshooting replaces randomness with a **systematic process**.

---

## Troubleshooting process: hypothesis → test

**Troubleshooting** is a systematic process for finding and fixing a problem’s cause.

Loop:

1. Create a **hypothesis** (a possible cause)
2. Run a **test** (a procedure that validates/invalidates the hypothesis)

Repeat until a test validates a hypothesis.

---

## Important assumptions (for learning)

To keep things simple, we usually assume:

- **One cause:** the problem has a single underlying cause
- **Certain tests:** a test result validates/invalidates with 100% certainty

Real life has uncertainty (you might not look carefully enough), so sometimes you must revisit a hypothesis.

---

## Troubleshooting and programming

In programming, troubleshooting is called **debugging**.

- problems are caused by **bugs**
- programs are large: one tiny mistake can break everything

Common beginner habits that don’t work well:

- making random changes
- asking for help before forming hypotheses
- not knowing how to design tests

Following a systematic process reduces frustration.

---

## Debugging mindset

Debugging isn’t a nuisance — it’s part of the job.

Analogy: a doctor doesn’t think diagnosis is “annoying” — it’s a core skill.

Takeaway: every time you debug systematically, you become a better programmer.

---

## Applying the loop to code (quick map)

- **Hypothesis:** what _could_ cause the wrong output/crash?
- **Test:** a small run that proves/disproves the hypothesis

In code, good tests often look like:

- reproduce with exact input
- reduce to a tiny case
- print values/types at a checkpoint
- re-run after the fix (plus a few edge cases)

---

## Logic of troubleshooting: hypotheses

A **hypothesis** is a statement of a _possible cause_.

Good hypotheses are:

- written so they can be **true or false**
- about a **cause**, not a solution

Example (lamp doesn’t light):

- ✅ “The bulb is broken.” (cause)
- ❌ “The bulb should be replaced.” (solution)

---

## Participation: forming hypotheses

For each statement: is it a **hypothesis of a cause** (Y) or **not** (N)?

1. Car won’t start → “The battery is dead.”
2. Car won’t start → “The user should wait and try again.”
3. Car won’t start → “Make sure the car has fuel.”
4. Smartphone has no signal → “The phone should be restarted.”
5. Phone doesn’t ring → “The phone is on silent.”
6. Music is very quiet → “Visually inspect the speaker for lint.”
7. Touchscreen misses presses → “The phone was dropped.”
8. Display is purple not white → “How firmly connected is the display cable?”
9. Lamp doesn’t light → “The bulb is working.”

---

## Debrief (quick)

Hypothesis (cause, true/false): 1, 5, 7, 9

Not a hypothesis (solution/test/question): 2, 3, 4, 6, 8

Takeaway: troubleshooting separates **cause** from **actions** (tests/solutions).

---

## Testing a hypothesis

A **test** is a procedure (often with two outcomes) that:

- **validates** a hypothesis, or
- **invalidates** a hypothesis

Example: Hypothesis “Bulb is broken”

- Test: try the bulb in a known-working lamp
- Result:
  - doesn’t light → validates
  - lights → invalidates

---

## Asymmetric tests

Some tests are **symmetric**:

- Yes validates / No invalidates (or vice versa)

Other tests are **asymmetric**:

- Yes validates, but No does **not** invalidate (or vice versa)

Example: “Bulb is broken”

- shake bulb, hear rattling → validates (filament broken)
- no rattling → does _not_ invalidate (bulb could be broken another way)

Use asymmetric tests as quick checks, but don’t over-trust a “No”.

---

## Tests, solutions, and overlap

Once a cause is found, you try a **solution**.

Sometimes:

- a test makes the solution obvious (wire is unplugged → plug it in)
- the test **solves** the problem (insert a new bulb)
- you can’t test directly, so you try a solution and see if it works (indirect validation)

---

## One test can cover multiple hypotheses

A single test may validate/invalidates multiple hypotheses.

Example: “Grass turned brown” hypotheses:

- water is off
- sprinkler system is off
- sprinkler system has a big underground leak

Test: “Check if the grass is wet.”

If wet (and it hasn’t rained), that can invalidate several hypotheses at once.

---

## Creating hypotheses

When faced with a problem, you usually create **multiple hypotheses** (possible causes).

Common pattern:

- start with just a few
- pick the **most likely** causes
- prefer causes that are **easy to test** first

---

## Ordering hypotheses (what to test first)

Given a list of hypotheses, order them based on:

- **likelihood** (how probable is this cause?)
- **ease of testing** (how fast/cheap/safe is the test?)

There are no strict rules — good ordering is partly an art.

---

## Knowledge yields hypotheses and tests

Every hypothesis and test comes from **knowledge of how the system works**.

Example (lamp doesn’t light):

- Hypothesis: “Not plugged in”
- Test: “Check if the wire is firmly plugged into the outlet”

That comes from knowing the lamp needs electricity through a plugged-in wire.

---

## Getting more knowledge (when you’re stuck)

Sometimes you run out of hypotheses.

To continue troubleshooting, you need new knowledge. Common ways:

- search the web
- ask another person (friend/colleague/support)

Then you can generate new hypotheses and new tests.

---

## Example: “Why won’t my lamp turn on?”

A web search might surface common causes/tests like:

- switch is off / not plugged in
- circuit breaker tripped
- light bulb not working (jiggle → try a new bulb)
- socket tab flattened (unplug first; carefully bend tab up)

New info (like “socket tab”) can create a new hypothesis + test.

---

## Example: portable speaker won’t turn on

You test your only hypothesis (“battery isn’t charged”) and it’s invalid.

You search and find a troubleshooting page that lists common hypotheses.

That new knowledge can lead to:

- Hypothesis: “I’m not holding the power button long enough”
- Test: “Hold power for 4 seconds. Turns on?”

Sometimes the test validates the hypothesis **and** solves the problem.

---

## Hierarchical hypotheses

**Hierarchy** means an object can be decomposed into sub-objects.

Example:

- U.S.A. → states → counties → cities

In troubleshooting, a broad hypothesis can be decomposed into more precise **sub-hypotheses**.

---

## Hierarchical hypotheses form a tree

You can think of hypotheses like a **tree**:

- start with a top-level hypothesis (high-level cause)
- decompose into child hypotheses (more specific causes)
- keep going top-down until you have a hypothesis that’s detailed enough to point to the cause

---

## Binary search (divide-and-test)

Often you’re trying to find _where_ in a large system the cause lives.

**Binary search** approach:

1. divide the system into two halves
2. run a test to decide which half contains the cause
3. repeat on that half

Example:

- Hypothesis: “File has a bad character”
- Sub-hypotheses: “Bad character is in first half” vs “Bad character is in second half”

---

## Why halving works

Halving shrinks the search space quickly.

Example: file with 200 lines

200 → 100 → 50 → 25 → 13 → 7 → 4 → 2 → 1

So only **8** halvings can narrow the cause to a single line (rounding up).

---

# Part 2 — Reading errors and tracebacks

---

## Traceback: how to read it

Start at the bottom:

- the last line is the error type + message
- the most useful line is often the **first line in your file** (not inside Python internals)

---

## Common error categories (Python)

- `SyntaxError`: Python can’t parse the code
- `NameError`: using a name that isn’t defined
- `TypeError`: using the wrong type for an operation
- `ValueError`: right type, wrong value (often input conversion)
- `IndexError` / `KeyError`: invalid index/key

---

## Example: `NameError`

```python
def total_cost(price, tax_rate):
	return price + (price * tax)

print(total_cost(10, 0.07))
```

Debug questions:

- What name is missing?
- Where was it supposed to come from?

---

## Example: `TypeError`

```python
age = input("Enter age: ")
print(age + 1)
```

Fix idea: convert types deliberately.

---

# Part 3 — Tools: isolating and checking assumptions

---

## Tool 1: Print debugging (the right way)

Use prints to check assumptions:

- print values _and_ types
- label output clearly
- remove the prints after the fix

```python
print("DEBUG price=", price, "type=", type(price))
```

---

## Tool 2: Checkpoint prints

Place prints at key milestones:

- before/after a loop
- before/after a function call
- before returning

Goal: find **the first wrong value**.

---

## Tool 3: Trace a tiny input by hand

Pick the smallest input that still fails.

Example:

- if the bug happens with 1,000 items, try 3
- if the bug happens at 50, try 49, 50, 51

---

# Part 4 — Guided practice

---

## Practice 1

You’re debugging a pay calculator. A coworker says:

- “Sometimes my pay comes out wrong, but it doesn’t crash.”

Tasks:

- Write 2–3 hypotheses for the wrong output
- Pick one test that quickly narrows the cause
- Fix + verify with the two provided cases (and one of your own)

---

## Practice 1 — Code

```python
def weekly_pay(hours, rate):
	# Overtime should be 1.5x for any hours over 40
	if hours > 40:
		overtime_hours = hours - 40
		return (hours * rate) + (overtime_hours * rate * 1.5)
	return hours * rate

print(weekly_pay(40, 10))  # expected 400
print(weekly_pay(45, 10))  # expected 475
```

---

## Practice 2

This program _sometimes_ crashes depending on what the user types.

Tasks:

- Create a minimal input that reproduces the crash
- Use the traceback to find the _first useful_ line
- Fix so extra spaces and accidental blanks don’t break it

---

## Practice 2 — Code

```python
def average_score(scores):
	total = 0
	for s in scores:
		total += int(s)
	return total / len(scores)

raw = input("Enter scores separated by spaces: ")
parts = raw.split(" ")
print("Average:", average_score(parts))
```

---

## Practice 3

You’re told: “This function works the first time, then gets weird.”

Tasks:

- Describe the symptom
- Make a hypothesis about what is being reused
- Fix so each call starts with a fresh empty cart (unless one is provided)

---

## Practice 3 — Code

```python
def add_item(item, cart=[]):
	cart.append(item)
	return cart

print(add_item("apple"))
print(add_item("banana"))
```

---

## Debugging habits checklist

- Reproduce first
- Change one thing at a time
- Keep a “known good” version
- Use small test inputs
- Verify with the original failing case
