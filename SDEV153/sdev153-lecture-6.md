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

# SDEV153 Lecture 6

#### CSS Layout: Page Structure + Flexbox

**Focus:** layout mental models, Flexbox essentials, common patterns, responsive habits, debugging

**Goal today:** build a reliable mental model.

---

<!--
## Today’s learning targets (optional)

- Explain how “normal flow” places elements and why layout breaks happen
- Use Flexbox to build common UI patterns (nav bars, cards, two-column layouts)
- Predict sizing behavior: content size vs container size
- Debug layout using the browser devtools
-->

## The layout mental model (high-level)

Three big layers:

1. **Normal flow** (default document layout)
2. **Layout modes** (`block`, `inline`, `flex`)
3. **Positioning** (`relative`, `absolute`, `fixed`, `sticky`)

---

## Normal flow

- **Block elements** stack top-to-bottom
- **Inline elements** flow left-to-right and wrap
- Parent height normally depends on its children (unless children are positioned)

---

# Part 1 — Flexbox fundamentals

---

## Flexbox: what it is

Flexbox is for **one-dimensional layout**:

- lay items out in a row OR a column
- distribute extra space
- align items on cross-axis

Think: “a smarter row/column system.”

---

## Mental model: Flexbox is “Auto Layout”

If you’ve used an auto layout tool (Figma Auto Layout, Stack/Row components, UI builders):

- You pick a **direction** (row/column)
- You choose **spacing** between items
- You choose **alignment** (start/center/end/stretch)
- Items can **grow** to fill space or **stay fixed**

Flexbox is the web version of that.

---

## Auto Layout mapping (sticky cheat sheet)

Container (the “frame”):

- Direction → `flex-direction`
- Spacing → `gap`
- Main-axis alignment → `justify-content`
- Cross-axis alignment → `align-items`
- Wrap to next line → `flex-wrap`

Items (the “children”):

- Fill remaining space → `flex-grow`
- Allow shrinking → `flex-shrink`
- Starting size → `flex-basis`

---

## The two roles: container vs items

- Parent becomes the **flex container**: `display: flex;`
- Direct children become **flex items**

If you put flex rules on grandchildren, nothing happens.

---

## Axes: the #1 flexbox concept

- `flex-direction` chooses the **main axis**
- Alignment changes meaning depending on axis

Quick mapping:

- Main axis alignment → `justify-content`
- Cross axis alignment → `align-items`

---

## Flexbox defaults (surprising at first)

Defaults:

- `flex-direction: row`
- `justify-content: flex-start`
- `align-items: stretch`
- items do **not** wrap (`flex-wrap: nowrap`)

Those defaults explain a lot of “why does it look like that?”

---

## Flexbox starter pattern (minimal)

Use this pattern constantly:

```css
.row {
  display: flex;
  gap: 1rem;
  align-items: center;
}
```

Then you choose whether you want wrapping, spacing, and sizing.

---

## Common confusion: `justify-content` “does nothing”

Most common causes:

- You’re not on a flex container
- Container has no extra space
- You meant cross-axis alignment (use `align-items`)

Debug tip: inspect the element and confirm it says “flex” in devtools.

---

## `gap` is your friend

- Use `gap` for spacing **between items**
- Avoid giving every child a `margin-right`

Better:

- consistent spacing
- no “last item has extra margin” hacks

---

## Wrapping rows

When you want cards that wrap:

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
```

Live demo idea: resize window and watch wrap happen.

---

## Centering (the reliable way)

Two different “centers”:

- center items within a row/column
- center a whole container on the page

Flex centering (items):

```css
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

## Flex sizing: `flex` shorthand

On a flex item:

- `flex-grow`: can it take extra space?
- `flex-shrink`: can it shrink when needed?
- `flex-basis`: starting size

Common patterns:

- `flex: 1` → “share space evenly”
- `flex: 0 0 200px` → “fixed basis, don’t grow/shrink”

---

## Two-column layout (classic)

Goal: main content + sidebar.

Conceptual setup:

- container is flex row
- main grows
- sidebar has a basis

Live demo: show what happens when the screen gets narrow.

---

## The min-width gotcha (real-world)

Sometimes text causes overflow even when flex should shrink.

Fix concept:

- allow the flex item to shrink by setting `min-width: 0` on the item that should be allowed to shrink

This is a common “why won’t it wrap?” issue in flex layouts.

---

# Part 2 — Page layout patterns

---

## Pattern: header / main / footer

Common page skeleton:

- header at top
- main grows
- footer at bottom

Flex column layout can do this cleanly.

Live demo: “sticky footer” without `position: fixed`.

---

## Pattern: nav bar

Typical needs:

- logo left
- links right
- consistent vertical alignment
- wrap or collapse later (responsive)

Flex makes this a one-container problem.

---

## Pattern: wrapping cards (Flexbox)

Flex-wrap works, but it’s “row-based”.

Use it when:

- you’re okay with uneven columns
- you want simple wrapping

---

## Pattern: media object

Example: avatar + text.

Layout goals:

- image fixed size
- text takes remaining space
- vertical alignment controlled

Flex with a gap solves it.

---

## Pattern: forms

Common issues:

- labels don’t line up
- inputs stretch weirdly
- spacing inconsistent

Suggestion:

- use a column flex container for vertical rhythm
- for label/input pairs, use flex row

---

# Part 3 — Responsive layout tips

---

## Tip #1: let things be fluid

Prefer:

- `%`, `fr`, `auto`
- `max-width`
- flexible containers

Avoid:

- fixed pixel widths everywhere
- fixed heights on text blocks

---

## Tip #2: Responsive images

Must-have concept:

- constrain images so they don’t overflow their container

Live demo suggestion: show an oversized image, then fix with `max-width: 100%`.

---

# Part 4 — Debugging layout (what pros actually do)

---

## Debug checklist

1. Inspect element → confirm layout mode (block/flex)
2. Turn on devtools overlays (flex)
3. Check container size vs item size
4. Temporarily add outlines to see boxes
5. Remove rules until it works, then re-add

---

## Quick “why is this broken?” questions

- Am I styling the right element?
- Is the parent constrained (`max-width`) or full width?
- Is the spacing coming from `margin` or `gap`?
- Did I accidentally set a fixed height/width?
- Are there default margins (like on `body`, `h1`, `ul`)?

---

## Common defaults to reset (carefully)

- `body` default margin
- headings default margin
- lists default padding

Live demo: minimal “reset” (not a giant framework).

---

## Wrap-up (what you should be able to do)

- Pick the right layout mode (flow vs flex)
- Use flex axes correctly (`justify-content` vs `align-items`)
- Build common page patterns with flex containers
- Debug layout with devtools instead of guessing

---

## 10-minute practice prompts

1. Build a nav: logo left, links right, centered vertically
2. Build a card row that wraps with consistent gaps
3. Make a simple page: header + main + footer (footer stays at bottom)
