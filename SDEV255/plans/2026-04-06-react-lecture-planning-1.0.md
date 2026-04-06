# React Lecture Planning for SDEV255

## Context Summary

**Course Structure Analysis:**
- Students have completed: JavaScript fundamentals, OOP patterns, DOM manipulation, Fetch/async, Node/Express basics
- Learning Objective 4-1: "Create a client-side application using frameworks and APIs"
- Final Project requires: "Front-end UI system (framework/library)"
- Next week: Fullstack React (connecting React frontend to Express backend)

**Time Allocation:**
- Two 3-hour lectures = 6 hours total
- Live coding style requires: concept intro → live demo → student practice cycle
- Standard pacing: ~15-20 min concept, ~25-35 min live build, ~10-15 min practice/check

**Current Student Skill Level:**
- Comfortable with: JavaScript (variables, functions, arrays, objects, classes), DOM events, Fetch API, async/await
- Familiar with: OOP patterns, JSON serialization, form validation
- Gap: No prior React/component framework experience

---

## Recommended React Coverage (Two Lectures)

### Lecture 1: React Foundations (3 hours)

**Core Topics (Must Cover - ~2.5 hours):**

1. **What React Is and Why It Exists** (15 min)
   - Declarative vs imperative UI
   - Component-based architecture
   - Virtual DOM concept (brief)
   - How it fits with what they know (JavaScript, DOM, events)

2. **JSX and Component Basics** (45 min live build)
   - JSX syntax rules
   - Functional components
   - Rendering to DOM with `createRoot`
   - Component composition (parent/child)
   - Live build: Simple static component tree

3. **Props: Passing Data Down** (40 min live build)
   - Props as function arguments
   - Prop types and default values
   - Passing functions as props (event handlers)
   - Live build: Parent passing data to child components

4. **State with useState Hook** (50 min live build)
   - What state is vs props
   - `useState` syntax and array destructuring
   - State updates trigger re-renders
   - Immutable state updates
   - Live build: Interactive component with state changes

**Buffer Time:** 20 minutes for questions, setup, transitions

---

### Lecture 2: React Patterns and API Integration (3 hours)

**Core Topics (Must Cover - ~2.5 hours):**

1. **Conditional Rendering & Lists** (35 min live build)
   - Ternary operators in JSX
   - `&&` short-circuit rendering
   - Rendering lists with `.map()`
   - Key prop importance
   - Live build: List component with conditional items

2. **Forms and Controlled Components** (40 min live build)
   - Controlled inputs (state as single source of truth)
   - Form submission handling
   - Multiple inputs pattern
   - Basic validation in React
   - Live build: Form with validation feedback

3. **Fetching Data in React** (45 min live build)
   - Where to fetch: `useEffect` hook
   - Loading and error states
   - Displaying fetched data
   - Dependency array basics
   - Live build: Component that fetches from an API

4. **Component Composition Patterns** (30 min live build)
   - Children prop
   - Lifting state up
   - Simple prop drilling (and why it becomes a problem)
   - Live build: Shared state between sibling components

**Buffer Time:** 30 minutes for questions, practice, wrap-up

---

## Additional Content Options (If Time Permits)

Given 6 hours with buffer, you have approximately **30-60 minutes of flexibility**. Recommended additions:

### Priority 1: Essential for Next Week's Fullstack (Add if possible)
- **Custom Hooks Introduction** (20 min)
  - Extracting fetch logic into `useFetch` hook
  - Why custom hooks matter for code reuse
  - Sets up cleaner API integration patterns for fullstack week

### Priority 2: Improves React Fluency
- **Event Handling Deep Dive** (15 min)
  - Synthetic events
  - Passing arguments to handlers
  - Preventing default behavior in React forms

### Priority 3: Quality of Life / Best Practices
- **Component Organization** (10 min)
  - File structure patterns
  - One component per file
  - Import/export patterns

### Priority 4: If Students Are Moving Quickly
- **useEffect Cleanup** (15 min)
  - Why cleanup matters (subscriptions, intervals)
  - Return function pattern
  - Preventing memory leaks

---

## What NOT to Cover (Save for Fullstack Week or Later)

These topics should be deferred to avoid overwhelming students:

- **useReducer / useContext** - State management can wait
- **React Router** - Navigation fits better with fullstack routing
- **Server-side rendering (Next.js)** - Advanced, not needed yet
- **Performance optimization (memo, useMemo, useCallback)** - Premature optimization
- **Testing React components** - Separate topic, not essential for this week
- **TypeScript with React** - Would require TypeScript prerequisite
- **Class components** - Functional components with hooks are the modern standard
- **Redux / state management libraries** - Overkill for this scope

---

## Live Coding Session Plans

### Lecture 1 Live Build Sequence

**Build 1: Hello React** (15 min)
```
- Create React app or use CDN/simple setup
- Single component returning JSX
- Render to DOM
- Modify JSX, see update
```

**Build 2: Component Tree** (30 min)
```
- Header component
- Main content component
- Footer component
- App component composing all three
- Pass simple props (title, year)
```

**Build 3: Interactive State** (45 min)
```
- Counter component with useState
- Button increments/decrements
- Display current count
- Add reset button
- Discuss: why not modify state directly
```

---

### Lecture 2 Live Build Sequence

**Build 1: Task List** (35 min)
```
- Array of task objects
- Map over array to render TaskItem components
- Add key prop
- Conditional: show "no tasks" message when empty
- Add checkbox to toggle completion (ternary styling)
```

**Build 2: Task Form** (40 min)
```
- Input field with controlled state
- Add button creates new task
- Form validation (non-empty required)
- Clear input after submit
```

**Build 3: API Fetch** (45 min)
```
- Fetch tasks from JSON placeholder or your Express server
- Show loading state
- Handle errors
- Display fetched data
- Add refresh button
```

**Build 4: Lift State** (30 min)
```
- TaskList and TaskStats as siblings
- Both need access to tasks array
- Move state to parent App component
- Pass down tasks and handlers as props
```

---

## Verification Criteria

After Lecture 1, students should be able to:
- [ ] Explain what React is and why components matter
- [ ] Write valid JSX with proper syntax
- [ ] Create functional components
- [ ] Pass and use props in child components
- [ ] Use useState to manage component state
- [ ] Update state correctly (immutably)

After Lecture 2, students should be able to:
- [ ] Render lists using .map() with keys
- [ ] Conditionally render UI elements
- [ ] Build controlled form inputs
- [ ] Fetch data using useEffect
- [ ] Handle loading and error states
- [ ] Lift state up to share between components

---

## Risk Assessment

### Risk 1: Students Struggle with JSX Syntax
**Likelihood:** Medium
**Impact:** Delays all subsequent topics
**Mitigation:** 
- Start with very simple JSX examples
- Show direct comparison to document.createElement
- Emphasize "it's just JavaScript" with expressions in braces

### Risk 2: useState Confusion (especially async updates)
**Likelihood:** High
**Impact:** Students write buggy state logic
**Mitigation:**
- Demonstrate the bug: show state not updating when they mutate directly
- Live code the "stale closure" problem with counter example
- Provide clear mental model: "state is immutable, always use setter"

### Risk 3: useEffect Dependencies Misunderstanding
**Likelihood:** High
**Impact:** Infinite loops or stale data
**Mitigation:**
- Start with empty dependency array (mount only)
- Show what happens with missing dependencies
- Keep examples simple; avoid complex dependency scenarios

### Risk 4: Running Out of Time
**Likelihood:** Medium
**Impact:** Core topics not fully covered
**Mitigation:**
- Priority order: JSX → Props → State → Lists → Forms → Fetch
- Skip composition patterns if needed (can reference next week)
- Have a "minimum viable demo" ready for each section

### Risk 5: Students Want to Compare to jQuery/vanilla JS
**Likelihood:** Medium
**Impact:** Can be educational or distracting
**Mitigation:**
- Acknowledge the comparison briefly
- Show one side-by-side example (imperative vs declarative)
- Move on: "React is a different mental model, embrace it"

---

## Alternative Approaches

### Alternative 1: Use create-react-app vs Vite vs CDN
**Trade-offs:**
- **create-react-app:** Familiar, but deprecated and slow
- **Vite:** Modern, fast, but another tool to explain
- **CDN/simple HTML:** Fastest to start, but not production-realistic

**Recommendation:** Vite for live coding (speed matters in demos), but explain that students can use any setup for labs.

### Alternative 2: Build One App Across Both Lectures
**Trade-offs:**
- **Single progressive app:** Better continuity, realistic project feel
- **Separate mini-examples:** Easier to reset if something breaks, clearer isolation of concepts

**Recommendation:** Hybrid approach - use a Task App as the main thread, but have isolated backup examples ready for each concept.

### Alternative 3: TypeScript Integration
**Trade-offs:**
- **Add TypeScript:** Industry-relevant, catches errors early
- **Skip TypeScript:** Reduces cognitive load, focuses on React concepts

**Recommendation:** Skip for this week. If the course uses TypeScript later, do a "TypeScript + React" session after students are comfortable with React basics.

---

## Connection to Next Week (Fullstack React)

Topics from this week that directly enable next week:

| This Week | Next Week (Fullstack) |
|-----------|----------------------|
| Fetching data with useEffect | Fetching from your own Express API |
| Loading/error states | Fullstack error handling |
| Form handling | Submitting data to backend |
| Lifting state up | Shared state across client/server boundary |
| Component composition | Page-level components with routing |

**Bridge statement for end of Lecture 2:**
> "This week we built React apps that fetch from external APIs. Next week, you'll build the Express backend that serves those APIs, and connect your React frontend to your own server."

---

## Final Recommendation

**Coverage Assessment:** The core React topics (JSX, props, state, lists, forms, fetch) fit well within 6 hours with live coding. There is **30-60 minutes of buffer** available.

**Recommended Use of Extra Time:**
1. **Custom Hooks (20 min)** - Highest value for fullstack preparation
2. **Additional practice time** - Let students code alongside you
3. **Early release** - If students are comfortable, letting them go early is better than rushing into advanced topics

**Do NOT add:** Context, Router, Redux, testing, performance optimization, class components

**Success Metric:** Students should leave able to build a simple React app that fetches and displays data, with forms that update state. This is the exact foundation needed for fullstack React next week.
