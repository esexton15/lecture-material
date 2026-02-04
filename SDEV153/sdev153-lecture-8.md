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

# SDEV153 Lecture 8

#### JavaScript Fundamentals (Part 2)

**Focus:** loops, functions, arrays/objects, DOM basics, debugging, exceptions

---

By the end of class you can:

- Write `for` and `while` loops safely
- Write functions (including arrow functions) and understand basic scope
- Use arrays and objects to store real-world data
- Read/change a page with basic DOM selection
- Use `try/catch` to prevent crashes from runtime errors

---

## 2-hour flow (suggested)

- **0:00–0:10** Warm-up: loop + function quick demo
- **0:10–0:35** Loops (for/while) + common bugs
- **0:35–0:55** Functions (parameters, return, scope)
- **0:55–1:30** Arrays + objects (everyday data structures)
- **1:30–1:40** DOM starter + debugging habits
- **1:40–1:55** Exception handling (try/catch/finally)
- **1:55–2:00** Exit ticket

---

# Part 3 — Loops

---

## `for` loop (counting)

```js
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

---

## `while` loop (condition-driven)

```js
let n = 1;
while (n < 10) {
  n = n * 2;
}
console.log(n);
```

---

## Loop safety checklist

- Does the loop variable change?
- Will the condition eventually become false?
- Are you accidentally creating an off-by-one?

---

# Part 4 — Functions

---

## Function basics

```js
function add(a, b) {
  return a + b;
}

console.log(add(2, 3));
```

---

## Arrow functions (common in web apps)

```js
const add = (a, b) => a + b;
```

If the body is more than one expression, use braces and `return`.

---

## Scope (very short version)

- `let` / `const` are **block-scoped**
- Variables declared inside `{}` don’t exist outside
- `var` is **function-scoped** (older behavior)

---

# Part 5 — Arrays + objects

---

## Arrays

An array is an **ordered list** of values.

- Each value is an **element**
- Each element is stored at an **index** (0, 1, 2, ...)

```js
const groceries = ["bread", "milk", "peanut butter"];
console.log(groceries[0]); // "bread"
console.log(groceries.length); // 3
```

Arrays can hold mixed types, but you usually keep them consistent.

---

## Adding/removing elements (6.8)

Common methods:

- `push(value)` / `pop()` (end)
- `unshift(value)` / `shift()` (front)

```js
let nums = [2, 4, 6];
nums.push(8); // [2, 4, 6, 8]

const last = nums.pop(); // last = 8, nums = [2, 4, 6]

nums.unshift(0); // [0, 2, 4, 6]
const first = nums.shift(); // first = 0, nums = [2, 4, 6]
```

---

## `splice()` (6.8)

`splice(startIndex, deleteCount, ...itemsToAdd)` changes the array.

```js
let nums = [2, 4, 6, 8, 10];

nums.splice(3); // delete from index 3 to end -> [2, 4, 6]
nums.splice(0, 2); // delete 2 from index 0 -> [6]
nums.splice(0, 0, 3, 5); // add 3,5 at index 0 -> [3, 5, 6]
nums.splice(2, 0, 7, 9, 11); // add at index 2 -> [3, 5, 7, 9, 11, 6]
```

---

## Looping with `length` (6.8)

Use `length` when you need the index.

```js
const groceries = ["bread", "milk", "peanut butter"];

for (let i = 0; i < groceries.length; i++) {
  console.log(i + " - " + groceries[i]);
}
```

---

## Looping with `for...of` (6.8)

Simpler when you just need each item:

```js
const groceries = ["bread", "milk", "peanut butter"];

for (const item of groceries) {
  console.log(item);
}
```

---

## Looping with `forEach()` (6.8)

`forEach()` takes a function and runs it once per element.

```js
const groceries = ["bread", "milk", "peanut butter"];

groceries.forEach(function (item, index) {
  console.log(index + " - " + item);
});
```

---

## Passing arrays to functions (6.8)

Arrays can be modified inside functions.

```js
function addBonus(scores) {
  for (let i = 0; i < scores.length; i++) {
    scores[i] = scores[i] + 5;
  }
}

const scores = [80, 92, 75];
addBonus(scores);
console.log(scores); // [85, 97, 80]
```

---

## Searching: `indexOf()` / `lastIndexOf()` (6.8)

Returns the index of the match, or `-1` if not found.

```js
const scores = [80, 92, 75, 64, 88, 92];

console.log(scores.indexOf(92)); // 1
console.log(scores.indexOf(92, 2)); // 5
console.log(scores.indexOf(100)); // -1

console.log(scores.lastIndexOf(92)); // 5
console.log(scores.lastIndexOf(92, 4)); // 1
```

---

## Sorting: strings vs numbers (6.8)

Default `sort()` compares **as strings** (Unicode order):

```js
const nums = [10, 2, 5];
nums.sort();
console.log(nums); // [10, 2, 5]  (surprising!)
```

For numeric sort, pass a compare function:

```js
nums.sort((a, b) => a - b);
console.log(nums); // [2, 5, 10]
```

---

## Objects and properties (6.9)

An object is an **unordered** collection of **properties**.

- A property is a **name/value** pair
- Commonly created with an **object literal** `{ ... }`

```js
const user = {
  name: "Kai",
  age: 19,
};

console.log(user.name);
console.log(user["age"]);
```

---

## Methods + `this` (6.9)

If a property’s value is a function, it’s a **method**.

Use `this` to access the object’s own properties.

```js
const account = {
  balance: 10,
  deposit: function (amount) {
    this.balance = this.balance + amount;
  },
};

account.deposit(5);
console.log(account.balance); // 15
```

---

## Accessor properties: getters/setters (6.9)

Use getters/setters when reading needs computation or setting needs validation.

```js
const person = {
  first: "Kai",
  last: "Ng",
  _age: 19,

  get fullName() {
    return this.first + " " + this.last;
  },

  set age(value) {
    if (value >= 0) this._age = value;
  },
};

console.log(person.fullName);
person.age = 20;
```

---

## Primitives vs references (6.9)

- **Primitives** copy the value (number, string, boolean, `null`, `undefined`)
- **Objects** copy a reference (two variables can point to the same object)

```js
let a = 2;
let b = a;
b = 3;
console.log(a); // 2

const u1 = { name: "Kai" };
const u2 = u1;
u2.name = "Sam";
console.log(u1.name); // "Sam"
```

---

## Passing objects to functions (6.9)

Mutating properties affects the original object; reassigning the parameter does not.

```js
function rename(user) {
  user.name = "Riley"; // changes original object
}

function reset(user) {
  user = { name: "New" }; // does NOT change the original reference
}

const user = { name: "Kai" };
rename(user);
reset(user);
console.log(user.name); // "Riley"
```

---

## Primitive wrappers (6.9)

Most primitives (except `null` / `undefined`) have methods via temporary “wrapper” objects.

```js
console.log("abc".toUpperCase()); // "ABC"
```

---

## Maps (key/value) with objects (6.10)

A **map** (associative array) stores key/value pairs.

JavaScript objects can act like maps (keys are property names):

```js
const counts = {};
counts["apples"] = 3;
counts["bananas"] = 1;

console.log(counts["apples"]); // 3
```

Bracket access is typical when treating an object as a map.

---

## `for...in` loop (object maps) (6.10)

`for...in` iterates over an object’s property names (order can be arbitrary).

```js
const counts = { apples: 3, bananas: 1 };

for (const key in counts) {
  console.log(key, counts[key]);
}
```

---

## Common map operations (6.10)

```js
const counts = { apples: 3, bananas: 1 };

// number of elements
console.log(Object.keys(counts).length);

// check for a key
console.log("apples" in counts); // true

// remove an element
delete counts.bananas;
```

---

## `Map` object (6.10)

`Map` is a newer key/value collection with explicit methods and `size`.

```js
const m = new Map();
m.set("apples", 3);
m.set("bananas", 1);

console.log(m.get("apples")); // 3
console.log(m.has("bananas")); // true
console.log(m.size); // 2

m.delete("bananas");
```

Looping through a `Map`:

```js
for (const [key, value] of m) {
  console.log(key, value);
}
```

---

## Arrays of objects (most real web data)

```js
const todos = [
  { text: "read", done: false },
  { text: "code", done: true },
];

const doneCount = todos.filter((t) => t.done).length;
console.log(doneCount);
```

---

# Part 6 — DOM (1 slide starter)

---

## DOM: read + change the page

```js
const title = document.querySelector("h1");
title.textContent = "Updated from JS";
```

We’ll go deeper when we start building pages.

---

## Debugging basics

- `console.log()` is fine for quick checks
- Use DevTools **Sources** to set breakpoints
- When confused: log the value _and_ `typeof value`

---

# Part 7 — Exception handling (6.14)

---

## Exception handling: what/why (6.14)

An **exception** is an error that disrupts the normal flow of program execution.

When an exception occurs, a program may need to execute code to handle the error:

- Display an error message
- Call a function (cleanup/retry)
- Shut down / stop the current operation

**Exception handling** is the process of catching and responding to an exception.

---

## `try` / `catch` / `finally` (6.14)

Pattern:

```js
try {
  // code that might throw
} catch (err) {
  // runs if an exception happens above
  console.error(err.name + ": " + err.message);
} finally {
  // runs whether it worked or failed (optional)
}
```

Notes:

- `catch` receives whatever was thrown (often an `Error`, but it can be a string, number, etc.)
- `finally` is great for cleanup (closing files, resetting UI state, etc.)

---

## Figure 6.14.1 — calling a non-existing method

JavaScript is **case-sensitive**.

```js
// Oops! Should be console.log()
console.Log("Will this work?");
```

Typical result:

```txt
Uncaught TypeError: console.Log is not a function
```

Feedback:

- This is a **runtime** error (program started running, then failed)
- Fix the spelling/casing (`log`, not `Log`)
- You can catch it, but it’s better to prevent it by calling the right method

---

## The `throw` statement (6.14)

The `throw` statement throws a user-defined exception.

Syntax:

```js
throw expression;
```

Example (throwing a string):

```js
throw "number is negative";
```

Feedback:

- Throwing strings works, but prefer `throw new Error("...")` for richer info (`name`, `message`, stack)

---

## Construct 6.14.1 — `try/catch`

```js
try {
  // Statements that might throw an exception
} catch (exception) {
  // Handle the exception
}
```

Key rule: a program halts when an exception is thrown **unless** it’s caught by a `try/catch`.

---

## Figure 6.14.2 — `finally` without a `catch`

`finally` executes whether an exception was thrown or not.

```js
function test() {
  try {
    console.log("try");
    throw "crash!!!";

    // Skips because an exception was thrown
    console.log("after throw");
  } finally {
    console.log("finally");
  }

  // Skips because an exception was thrown
  console.log("after");
}

// Exception is not caught, so program halts!
test();
console.log("done");
```

Expected output:

```txt
try
finally
Uncaught crash!!!
```

Feedback:

- `finally` is perfect for cleanup that **must** run
- If you want the program to continue, add a surrounding `try/catch` where you call `test()`

---

## Figure 6.14.3 — `finally` runs even if `catch` throws

```js
function test() {
  try {
    console.log("try");
    throw "crash!!!";

    // Skips because exception is thrown
    console.log("after throw");
  } catch (exception) {
    console.log("catch");
    throw "oops!!!";
  } finally {
    console.log("finally");
  }

  // Doesn't execute because exception thrown in catch block
  console.log("after");
}

test();
console.log("done");
```

Expected output:

```txt
try
catch
finally
Uncaught oops!!!
```

Feedback:

- `finally` is especially useful when your `catch` code might also fail

---

## Error objects (6.14)

Developers commonly throw an `Error` object.

An `Error` object represents a runtime error and includes:

- `name` — the error’s name
- `message` — the error’s message

```js
const err = new Error("My error message.");
console.log(err.name); // "Error"
console.log(err.message); // "My error message."
```

Other common error types:

- `TypeError` — wrong type
- `RangeError` — value outside valid range

---

## Figure 6.14.4 — throwing `Error`, `TypeError`, `RangeError`

```js
// Returns the average of the scores array
function findAverage(scores) {
  if (!Array.isArray(scores)) {
    throw new TypeError("Must supply an array.");
  }

  if (scores.length === 0) {
    throw new Error("Must supply at least one score.");
  }

  let sum = 0;
  scores.forEach(function (score) {
    if (!Number.isInteger(score)) {
      throw new TypeError("Score '" + score + "' is not an integer.");
    }
    if (score < 0) {
      throw new RangeError("Negative score encountered.");
    }
    sum += score;
  });
  return sum / scores.length;
}

try {
  const ave = findAverage([50, "cow"]);
  console.log("Average:", ave);
} catch (ex) {
  console.log(ex.name + ": " + ex.message);
}
```

Typical output:

```txt
TypeError: Score 'cow' is not an integer.
```

Feedback:

- Throw **specific** error types when you can (helps debugging)
- Keep the `try` block tight so you know what line likely failed

---

## Example: handling bad JSON input

`JSON.parse()` throws if the text is not valid JSON.

```js
const text = prompt('Paste JSON like {"x": 1}:');

try {
  const obj = JSON.parse(text);
  console.log("x is", obj.x);
} catch (err) {
  console.log("That was not valid JSON.");
  console.log(err.message);
}
```

---

## Example: numbers (validate vs exceptions)

Not every “bad value” throws an exception.

```js
const raw = prompt("Enter an integer:");
const n = Number(raw);

if (!Number.isInteger(n)) {
  console.log("Invalid integer");
} else {
  console.log("n + 1 =", n + 1);
}
```

Rule of thumb:

- Use **validation** for expected input problems
- Use `try/catch` for operations that actually _throw_

---

## Throwing your own exception (6.14)

You can create an error when something must not happen:

```js
function requireNonEmpty(s) {
  if (typeof s !== "string" || s.trim() === "") {
    throw new Error("Expected a non-empty string");
  }
  return s.trim();
}

try {
  const name = requireNonEmpty(prompt("Name?"));
  console.log("Hello", name);
} catch (err) {
  console.log("Please enter a name.");
}
```

---

## What `try/catch` does NOT do

- It can’t “fix” a **syntax error** (code that won’t even run)
- It won’t catch errors in other async callbacks unless the `try` wraps _that_ execution

For this course right now:

- Focus on catching **runtime errors** in the same block of code
- Keep `try` blocks small so you know what failed

---

## Exit ticket (5 minutes)

Write code that:

1. Stores an array of numbers
2. Computes the sum
3. Prints `"even"` or `"odd"` for each number

---

<!-- BOOK CONTENT INSERTS (send excerpts anytime) -->
<!-- - Add slides for: variables & constants terminology -->
<!-- - Add slides for: common JS errors from the book -->
<!-- - Add guided practice problems from the book -->
