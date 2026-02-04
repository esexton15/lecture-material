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

# SDEV153 Lecture 7

#### JavaScript Fundamentals (Part 1)

**Focus:** variables, types, operators, conditionals/loops, functions, arrays/objects, debugging

---

By the end of class you can:

- Explain what JavaScript runs on browser
- Use `let` / `const` correctly
- Predict type coercion pitfalls and avoid them
- Write `if/else`, loops, and simple functions
- Use arrays/objects and basic DOM interaction

---

<!--
## 2‑hour flow (suggested)

- **0:00–0:10** Warm‑up: JS in the browser console
- **0:10–0:35** Variables + types + coercion
- **0:35–0:55** Operators + comparisons + conditionals
- **0:55–1:15** Loops + common loop bugs
- **1:15–1:35** Functions (parameters, return, scope)
- **1:35–1:55** Arrays + objects (the everyday data structures)
- **1:55–2:00** Exit ticket

--- -->

# Part 0 — Where JavaScript runs

---

## JavaScript execution environments

- **Browser**: runs in tabs (Chrome/Edge/Firefox)
- **Node.js**: runs on your computer/server

For this course: we care about **browser JS + the DOM**.

---

## Background (6.1)

- 1995: Brendan Eich created JavaScript for Netscape Navigator
- Goal: respond to user events (click/hover) and update the page
- 1997: standardized as **ECMAScript** (by Ecma International)
- Today: runs in every major browser + on servers via **Node.js**

---

## Interpreter + JIT (6.1)

- JavaScript is executed by an **interpreter** (runs code without a separate compile step)
- Modern engines use **JIT compilation** to speed execution

Practical takeaway: you’ll mostly “run it and see,” then debug in DevTools.

---

## Warm‑up (2 minutes)

Open DevTools → Console and run:

```js
console.log("Hello, JS");
console.log(2 + 3);
```

---

## Input & output (browser) (6.1)

- `prompt()` gets **one line of text** from the user
  - returns a `string`, or `null` if they cancel
- `console.log()` prints to the browser console

```js
const name = prompt("What is your name?");
console.log("Name:", name);
```

If you need a number:

```js
const age = Number(prompt("Age?"));
console.log(age + 1);
```

---

# Part 1 — Variables + types

---

## `let` vs `const`

- `const`: default choice (can’t reassign)
- `let`: use when the value must change

```js
const course = "SDEV153";
let counter = 0;
counter = counter + 1;
```

---

## `var` vs `let`

`var` is the older way to declare variables (pre‑2015).

Key difference: **scope** (where a variable is accessible).

- `var` → **function-scoped**
- `let` / `const` → **block-scoped** (inside `{}` only)

Rule for this course: default to `const`, then `let`.

---

## Block scope vs function scope

```js
function demo() {
  if (true) {
    var a = 1;
    let b = 2;
  }

  console.log(a); // 1 (var is function-scoped)
  // console.log(b) // ReferenceError (let is block-scoped)
}
```

---

## Global variables + the global object)

Before your code runs, JavaScript creates the **global object**.

In a browser, the global object is usually `window`.

So a global variable called `test` may be accessible as `window.test`.

---

## Why globals are risky

Globals can collide with existing `window` properties.

Example: `window.location` is the current page URL.

If you do this:

```js
location = "Texas"; // BAD
```

the browser may try to navigate to a page named “Texas”.

---

## 3 ways “global X” can happen

In browser scripts (not modules):

1. `var X = 1` → adds `window.X`
2. `let X = 1` → global name `X`, but **not** `window.X`
3. `X = 1` (no `let/const/var`) → creates `window.X` (even inside a function)

Best practice: always declare with `const`/`let`.

---

## Variables: declare, assign, initialize

- **Declaration:** create a variable name
- **Assignment:** give it a value
- **Initialization:** declare + assign in one line

```js
let score; // declaration
score = 2; // assignment

let maxValue = 5; // initialization
const slicesPerPizza = 8;
```

---

## Identifier rules + naming (6.1)

Identifiers can contain:

- letters, digits, `_`, or `$`
- cannot start with a digit
- cannot be reserved words like `let`, `function`, `while`

Convention: **camelCase**

```js
let lastPrice = 10;
// prefer lastPrice over LastPrice or last_price
```

---

## Primitive types you’ll see constantly

- `string` → `"hi"`
- `number` → `42`, `3.14`
- `boolean` → `true` / `false`
- `null` → intentional “no value”
- `undefined` → missing/unset

```js
console.log(typeof "hi");
console.log(typeof true);
```

---

## Dynamic typing (6.1)

JavaScript determines types **at runtime**.

```js
let x = 5;
x = "test";
console.log(typeof x); // "string"
```

This is powerful, but it’s also why type coercion bugs happen.

---

## Comments + semicolons

Comments:

```js
// single-line comment
/* multi-line
	comment */
```

Semicolons are optional in many places, but be consistent.

---

## Strings: template literals

Use backticks for readable string building:

```js
const name = "Kai";
const score = 18;
console.log(`${name} scored ${score}`);
```

---

## String object

String literals are automatically treated like `String` objects when you call methods.

```js
const s = "test";
console.log(s.length); // 4
console.log(s.charAt(1)); // "e"
console.log(s.charAt(99)); // "" (empty string)
```

---

## Searching + replacing

```js
let s = "Seek and you will find.";

console.log(s.indexOf("and")); // 5
console.log(s.indexOf("e")); // 1
console.log(s.lastIndexOf("e")); // 2
console.log(s.indexOf("SEEK")); // -1 (case-sensitive)

s = s.replace("find", "discover");
console.log(s); // "Seek and you will discover."
```

---

## Common String methods

```js
let s = "As you wish.";

console.log(s.substr(3, 3)); // "you" (legacy)
console.log(s.substring(3, 6)); // "you"
console.log(s.split(" ")); // ["As", "you", "wish."]

console.log("What?".toLowerCase());
console.log("What?".toUpperCase());
console.log("   test  ".trim()); // "test"
```

---

## Type coercion

```js
console.log("2" + 2); // "22"
console.log("2" * 2); // 4
```

Rule of thumb:

- `+` can mean **string concatenation**
- prefer explicit conversion

```js
Number("2"); // 2
String(2); // "2"
```

---

## Quick practice

Predict the output:

1. `"5" + 1`
2. `"5" - 1`
3. `Number("5") + 1`

<!-- Answers: "51", 4, 6 -->

---

# Part 2 — Operators, comparisons, and conditionals

---

## Comparisons: prefer `===` and `!==`

- `===` checks value **and** type
- `==` allows coercion (surprising)

```js
console.log(0 == "0"); // true (coercion)
console.log(0 === "0"); // false
```

---

## `==` vs `===`

- `==` / `!=` may **coerce types** (ex: string → number)
- `===` / `!==` are **strict** (type + value must match)

```js
console.log(3 == "3"); // true
console.log(3 === "3"); // false
console.log("3" !== 3); // true
```

Rule for this course: prefer `===` and `!==`.

---

## Common bug: using `=` in a condition

This assigns instead of compares:

```js
// WRONG (syntax error in JS):
if (name = "Sue") {
	...
}
```

Use `===`:

```js
if (name === "Sue") {
	...
}
```

---

## Conditionals (pattern)

```js
const temp = 12;

if (temp < 8) {
  console.log("Too cold");
} else if (temp <= 26) {
  console.log("Satisfactory");
} else {
  console.log("Too hot");
}
```

Braces `{}` create a block.

---

## Always use braces (even for one line) (6.3)

JavaScript allows omitting braces for single statements, but it’s risky.

Avoid:

```js
if (vote === "M") memberCount++;
else nonMemberCount++;
```

Prefer:

```js
if (vote === "M") {
  memberCount++;
} else {
  nonMemberCount++;
}
```

---

## Comparing numbers vs strings (6.3)

- Number vs number: numeric comparison
- Number vs string: JS often converts the string to a number (`2 < "12"` is true)
- String vs string: compares by **Unicode** values (character-by-character)

```js
console.log("cat" <= "dog"); // true ("c" comes before "d")
```

---

## Nested `if` vs `else if`

Nested is valid but can get hard to read:

```js
if (score >= 90) {
  grade = "A";
} else {
  if (score >= 80) {
    grade = "B";
  } else {
    grade = "C";
  }
}
```

---

## Nested `if` vs `else if`

`else if` is usually clearer:

```js
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else {
  grade = "C";
}
```

---

## Logical operators

- `&&` (and)
- `||` (or)
- `!` (not)

```js
const age = 19;
console.log(age >= 16 && age < 25);
```

---

## `&&` / `||` precedence + parentheses (6.3)

`&&` is evaluated before `||`.

Good practice: use parentheses to show intent.

```js
// clearer:
if (a < 0 || (a > 1 && b > 2)) {
	...
}
```

---

## Avoid `!` when a simpler comparison exists

Harder to read:

```js
if (!(score > 10)) {
	...
}
```

Clearer:

```js
if (score <= 10) {
	...
}
```

---

## Truthy / falsy

A **truthy** value is a non-Boolean that acts like `true` in an `if`.

A **falsy** value is a non-Boolean that acts like `false` in an `if`.

---

## Common Truthy / falsy Values

Common falsy values:

- `false`, `0`, `""`, `NaN`, `undefined`, `null`

Common truthy examples:

- non-zero numbers (ex: `32`)
- non-empty strings (ex: `"cat"`)
- objects/arrays (ex: `{}` and `[]`)

---

## Quick truthy/falsy practice

Will each `if` run?

```js
if (0) console.log("A");
if (" ") console.log("B");
if ([]) console.log("C");
if (null) console.log("D");
```

<!-- A no, B yes, C yes, D no -->

---

## Conditional (ternary) operator (6.4)

Concise if/else expression:

```js
const label = age >= 18 ? "adult" : "minor";
```

Guideline: use ternary for simple assignments; use `if/else` when logic gets long.

---

## `switch` statement (6.4)

Use `switch` as an alternative to a long `else if` chain.

- `switch` uses **strict equality** (`===`) for matching
- `break` prevents “fall-through” into the next case

```js
switch (status) {
  case "open":
    console.log("open");
    break;
  case "closed":
    console.log("closed");
    break;
  default:
    console.log("unknown");
}
```

If you forget `break`, the next case runs too.

---

## Wrap-up

- Prefer `===` / `!==` for comparisons
- Know what’s **truthy/falsy** to avoid surprises
- Use parentheses with `&&` / `||` when in doubt
- Use `switch` when you have many exact string matches

---

## Code Activity (5 minutes)

Write code that prompts for a temperature and prints:

- `Too cold` if `temp < 8`
- `Satisfactory` if `8 <= temp <= 26`
- `Too hot` if `temp > 26`

Requirements:

- Use `Number(prompt(...))`
- Use `if / else if / else`

---

## Next class

- Loops, functions, arrays/objects, DOM starter
- Exception handling (`try/catch/finally`) as a debugging tool
