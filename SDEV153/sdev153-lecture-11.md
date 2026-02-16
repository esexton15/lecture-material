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

# SDEV153 Lecture 11

#### DOM + Form Validation + Secure Coding

**Focus:** DOM updates, validation, and secure programming basics

---

## Today’s outcomes

By the end of class you can:

- Select and modify DOM elements
- Create, add, and remove DOM elements
- Validate forms with HTML5 and JavaScript
- Identify risks and strategies for secure coding

---

# Part 1 — Form validation

---

## Why validate in the browser

Data validation checks input for correctness.

Servers **must** validate, but browser validation improves UX:

- immediate feedback
- fewer round trips
- clearer error messages

---

## When to validate

Two common options:

1. **As the user types** (input/change handlers)
2. **On submit** (submit handler)

Both can be used together.

---

## JavaScript validation basics

Most inputs use the `value` property:

- length checks
- equality checks (`===`)
- substring checks (`indexOf()`)
- numeric checks (`isNaN()`)
- pattern checks (regex + `match()`)

Checkbox/radio use `checked`.

---

## Validate on submit (checkbox example)

```html
<form id="tosForm">
  <label for="tos">I agree:</label>
  <input type="checkbox" id="tos" />
  <input type="submit" />
</form>
```

```js
function checkForm(event) {
  let tosWidget = document.querySelector("#tos");
  if (!tosWidget.checked) {
    event.preventDefault();
  }
}

let tosForm = document.querySelector("#tosForm");
tosForm.addEventListener("submit", checkForm);
```

---

## Validate as the user types (ZIP)

```html
<form id="tosForm">
  <label for="zip">ZIP:</label>
  <input type="text" id="zip" />
  <input type="submit" />
</form>
```

```js
let zipCodeValid = false;
let zipCodeWidget = document.querySelector("#zip");
zipCodeWidget.addEventListener("input", checkZipCode);

function checkZipCode() {
  let regex = /^\d\d\d\d\d$/;
  let zip = zipCodeWidget.value.trim();
  zipCodeValid = zip.match(regex);
}

let tosForm = document.querySelector("#tosForm");
tosForm.addEventListener("submit", checkForm);

function checkForm(event) {
  if (!zipCodeValid) {
    event.preventDefault();
  }
}
```

---

## HTML5 validation (built-in)

Browser validation can reduce JS needs:

- `required`
- `min` / `max`
- `minlength` / `maxlength`
- `pattern` + `title`

Note: unsupported inputs fall back to text.

---

## HTML5 validation example

```html
<form>
  <input type="range" name="age" min="5" max="120" />
  <input type="checkbox" name="agree" required />
  <input type="password" name="password" minlength="10" maxlength="16" />
  <input
    type="text"
    name="credit"
    pattern="^\d{16}$"
    title="exactly 16 digits"
  />
  <input type="submit" />
</form>
```

---

## Styling validation states

CSS pseudo-classes:

- `:valid`
- `:invalid`
- `:required`
- `:optional`

Use these to highlight fields as users edit.

---

# Part 2 — DOM updates

---

## JavaScript + the DOM

JavaScript runs in the browser and can change the page in response to events.

The **DOM** is the data structure for the HTML document.

`document` represents the page; changes to it update the view.

---

## The `window` object

Each browser tab has a `window` object.

Useful properties:

- `window.location` (URL info)
- `window.navigator` (browser info)
- `window.innerWidth/innerHeight` (viewport size)

Useful methods:

- `alert()`, `confirm()`, `open()`

---

## Use the console

Keep the dev console open while coding.

Common console API methods:

- `console.log()`
- `console.warn()`
- `console.error()`
- `console.dir()`

Errors often show up **only** in the console.

---

## Load JS from external files

Use external scripts for maintainability:

```html
<script src="app.js"></script>
```

Always include a **closing** `</script>` tag.

---

## `async` vs `defer`

```html
<script src="app.js" async></script>
<script src="app.js" defer></script>
```

- `async`: downloads + executes as soon as possible
- `defer`: downloads now, executes after HTML is parsed

---

## DOM structure

The DOM is a **tree** of nodes built from the HTML.

- root node at the top
- parents, children, siblings
- nodes for elements, text, and attributes

---

## Inspecting the DOM

Use DevTools Elements panel to view the live DOM.

In Chrome: `Ctrl+Shift+C` (Win/Linux) or `Cmd+Option+C` (Mac).

The DOM can differ from the raw HTML (browser may add nodes).

---

## DOM search methods

Single element:

- `getElementById("id")`
- `querySelector("css")`

Multiple elements:

- `getElementsByTagName("tag")`
- `getElementsByClassName("class")`
- `querySelectorAll("css")`

---

## NodeList vs HTMLCollection

Both look like arrays:

- have `length`
- use `[0]` indexing

Treat them as collections, not true arrays.

---

## More DOM modification

Once you can **find elements**, you can also:

- navigate the DOM tree (parents/children/siblings)
- move existing nodes
- insert/remove nodes
- create or clone nodes

---

## Accessing nodes

The root of the DOM tree is:

```js
let html = document.documentElement;
```

That gives you the `<html>` element node.

---

## Node relationships (common properties)

- `parentNode`: the node’s parent
- `childNodes`: _all_ children (includes whitespace text nodes)
- `children`: element children only (no text nodes)
- `nextElementSibling`: next element with same parent
- `previousElementSibling`: previous element with same parent

---

## Common mistake: `childNodes` vs `children`

When iterating list items, prefer `children`:

- `ol.children` contains only `<li>` nodes
- `ol.childNodes` also includes whitespace text nodes between `<li>` nodes

---

## Example HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Geologic eons of earth</title>
  </head>
  <body>
    <p>The four geologic eons on earth:</p>
    <ol>
      <li><a href="https://en.wikipedia.org/wiki/Hadean">Hadean</a></li>
      <li><a href="https://en.wikipedia.org/wiki/Archean">Archean</a></li>
      <li>
        <a href="https://en.wikipedia.org/wiki/Proterozoic">Proterozoic</a>
      </li>
      <li>
        <a href="https://en.wikipedia.org/wiki/Phanerozoic">Phanerozoic</a>
      </li>
    </ol>
  </body>
</html>
```

---

## Modifying the DOM structure

Move or remove existing nodes:

- `appendChild(node)`
- `insertBefore(node, existingChild)`
- `removeChild(node)`

---

## Move a node with `appendChild()`

Append moves a node if it already exists in the DOM:

```js
const ol = document.getElementsByTagName("ol")[0];
const li = ol.getElementsByTagName("li")[0];
ol.appendChild(li);
```

This moves the first `<li>` to the end.

---

## Move a node with `insertBefore()`

```js
const ol = document.getElementsByTagName("ol")[0];
const items = ol.getElementsByTagName("li");
ol.insertBefore(items[0], items[3]);
```

This moves the first `<li>` before the 4th.

---

## Remove a node with `removeChild()`

Common pattern:

```js
// n is the node you want to remove
n.parentNode.removeChild(n);
```

(`remove()` is also available on modern elements.)

---

## Create new nodes

Create element + text nodes:

```js
const p = document.createElement("p");
const text = document.createTextNode("Hello there!");
p.appendChild(text);
```

The new nodes don’t appear until attached to the DOM.

---

## Clone nodes with `cloneNode()`

```js
const copyShallow = x.cloneNode(false);
const copyDeep = x.cloneNode(true);
```

- `false`: clone only the node
- `true`: clone the node and all children

Watch out for duplicated `id` attributes after cloning.

---

## Modify attributes

Every attribute is a property:

```js
const link = document.getElementById("nasa_link");
link.href = "https://www.spacex.com/";
```

Remove an attribute:

```js
link.removeAttribute("href");
```

---

## Modify content

```js
document.querySelector("p").textContent = "$25.99";
document.querySelector("p").innerHTML = "<strong>$25.99</strong>";
```

- `textContent` is faster (no HTML parsing)
- `innerHTML` parses HTML

---

## Mini exercise (Pluto)

Goal on button click:

- show hidden paragraph `#p2`
- change `#lastPlanet` to "Neptune"
- set `#p4` to a source link

Hint: use `getElementById()`, `removeAttribute()`, `textContent`, `innerHTML`.

---

## Why async requests matter

Traditional page loads block the UI and refresh the whole page.

Modern apps use **async requests** so the page stays responsive.

Today: use `fetch()` instead of legacy `XMLHttpRequest`.

---

## Fetch basics (GET)

```js
fetch("/api/products")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  });
```

`fetch()` returns a **Promise**. Use `.then()` or `async/await`.

---

## Fetch with async/await

```js
async function loadProducts() {
  const response = await fetch("/api/products");
  const data = await response.json();
  console.log(data);
}
```

Use `await` to read the response without blocking the UI.

---

## Check status codes

Fetch only rejects on **network** errors.

Always check status:

```js
if (!response.ok) {
  throw new Error(`HTTP ${response.status}`);
}
```

Common codes: 200, 301, 400, 401, 403, 404, 500, 503.

---

## Response types

Choose the right parser:

- `response.json()` for JSON
- `response.text()` for plain text / HTML
- `response.blob()` for files

```js
const html = await response.text();
```

---

## Update the DOM after fetch

```js
const list = document.querySelector("#results");
list.innerHTML = "";

data.forEach((item) => {
  const li = document.createElement("li");
  li.textContent = item.name;
  list.appendChild(li);
});
```

This covers **create + add** elements.

---

## Remove elements safely

```js
const item = document.querySelector(".result");
if (item) item.remove();
```

Use `remove()` or `parent.removeChild(node)`.

---

## Handle errors

```js
try {
  const response = await fetch("/api/products");
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  const data = await response.json();
} catch (err) {
  console.error(err);
}
```

---

## Cancel or timeout a request

```js
const controller = new AbortController();

const timeout = setTimeout(() => controller.abort(), 5000);
const response = await fetch("/api/products", {
  signal: controller.signal,
});
clearTimeout(timeout);
```

Use `AbortController` to cancel slow requests.
