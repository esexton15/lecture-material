# Module 5 Lecture Content Plan — Solving Difficult Structuring Problems

## Objective

Create two ~3-hour Marp slide decks (Day 9 and Day 10) for Module 5 of SDEV 120, covering: solving difficult structuring problems (Appendix B spaghetti method), priming input, UML Use Case Diagrams, secure programming, and IT ethics. The slides must follow the existing Marp format established in `1.md` and `6.md`.

---

## Context and Scope

### Course Trajectory
| Module | Topic |
|--------|-------|
| 1 | Programming Logic & Design |
| 2 | Elements of High-Quality Programs |
| 3 | Understanding Numbering Systems and Computer Codes |
| 4 | Understanding Structure |
| **5** | **Solving Difficult Structuring Problems** |
| 6 | (TBD) |
| 7 | (TBD) |
| 8 | (TBD) |

### Module 5 Assignments (students must complete)
- Discussion: Ethical Obligations for IT Professionals
- Assignment: Applying Principles of Structured Programming (2 steps)
- Assignment: UML — Use Case Diagrams
- Assignment: Applying Basic Formulas
- Knowledge Check
- Group Project check-in

### Module 5 Learning Objectives (subset of course-level objectives active this week)
1. Use flowcharts, pseudocode, and UML to visualize/express algorithms and document system design
2. Use control structures (sequence, selection, repetition) and modularity to design algorithms
3. Present priming input to a structured program
4. Differentiate between integer and floating-point values; present basic control structures
5. Compute arithmetic operations
6. Describe security practices in programming; define reason for a code of ethics
7. Summarize security testing for loopholes and weaknesses; describe goals of security testing
8. Investigate secure design patterns; explain building security into the SDLC

---

## Slide Deck Format Specification

Both decks use the identical Marp YAML front-matter and CSS from `1.md:1-40`:
- `marp: true`, `theme: gaia`, `class: invert`, `paginate: true`
- Font sizes: section `1.85rem`, h1 `3.3rem`, h2 `2.2rem`
- Scoped centering style for title slides
- Horizontal rule `---` between every slide

---

## Lecture 1 (Day 9): Structured Programming Deep Dive — ~3 hours

### Part 1: Welcome and Agenda (~10 min)
- [ ] Slide: Title — "SDEV 120 Day 9 — Solving Difficult Structuring Problems"
- [ ] Slide: Today We Will Cover — numbered agenda (4 parts)
- [ ] Slide: Part 1 divider — "Review — The Three Structures"

### Part 2: Review — The Three Structures (~30 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: Recap — The Three Fundamental Structures (sequence, selection, loop)
- [ ] Slide: Sequence Structure — definition + simple flowchart/pseudocode example
- [ ] Slide: Selection Structure (IF-THEN-ELSE) — definition + example
- [ ] Slide: Repetition Structure (WHILE/DO-WHILE) — definition + example
- [ ] Slide: Why Structure Matters — readability, maintainability, testability, debugging
- [ ] Slide: Quick Check — identify which structure is shown in 2-3 small examples
- [ ] Slide: Part 2 divider — "Structured vs. Unstructured Flowcharts"

### Part 3: Structured vs. Unstructured Flowcharts (~50 min)
- [ ] Slide: What Makes a Flowchart Structured? — rules (single entry, single exit per structure; no crossed lines; nesting allowed)
- [ ] Slide: Visual — a structured flowchart segment (clean, nested boxes)
- [ ] Slide: Visual — an unstructured flowchart segment (crossed lines, multiple exits)
- [ ] Slide: The Problem with Spaghetti Code — hard to read, hard to debug, hard to maintain
- [ ] Slide: Can Every Problem Be Solved Structured? — yes, theorem (Bohm-Jacopini)
- [ ] Slide: The "Spaghetti Method" — introduction to the technique from Appendix B
- [ ] Slide: Spaghetti Method Step 1 — Start at the first decision, pull one branch
- [ ] Slide: Spaghetti Method Step 2 — Follow the No/left branch, document the path
- [ ] Slide: Spaghetti Method Step 3 — Follow the Yes/right branch, document the path
- [ ] Slide: Spaghetti Method Step 4 — Handle repeated steps (copy processes as needed)
- [ ] Slide: Spaghetti Method Step 5 — Identify loops and ensure they return directly to their own question
- [ ] Slide: Spaghetti Method Step 6 — Repeat the decision question when a loop would skip back past another decision
- [ ] Slide: Key Insight — you may need to DUPLICATE steps to eliminate crossed lines
- [ ] Slide: Worked Example — Walk through the full Figure B-1 to B-7 restructuring from Appendix B (3-4 slides showing each step with descriptions)
- [ ] Slide: Before vs. After — side-by-side comparison of unstructured and structured versions
- [ ] Slide: Practice Exercise 1 — Given an unstructured flowchart, students identify the problems
- [ ] Slide: Practice Exercise 2 — Students attempt to restructure it (individual or pair work)
- [ ] Slide: Part 3 divider — "Priming Input"

### Part 4: Priming Input (~40 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: The Priming Read Problem — why do we need input before a loop starts?
- [ ] Slide: Example Without Priming — flowchart/pseudocode showing a loop that checks a condition before any input is read (logic error)
- [ ] Slide: Example With Priming — flowchart/pseudocode showing the priming read before the loop, then reading again inside the loop
- [ ] Slide: Priming Input Pattern — generalized pattern: read first value → while condition → process → read next value
- [ ] Slide: Sentinel Values and Priming — how priming works with sentinel-controlled loops
- [ ] Slide: Common Mistakes — forgetting the priming read, reading twice, off-by-one errors
- [ ] Slide: Practice — write pseudocode for a program that reads scores until -1 is entered, using priming input
- [ ] Slide: Part 4 divider — "Applying Basic Formulas"

### Part 5: Applying Basic Formulas (~30 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: Integer vs. Floating-Point Values — definition, when to use each, precision differences
- [ ] Slide: Integer Division and Remainder — how computers handle integer division vs. floating-point division
- [ ] Slide: Arithmetic Operators — +, -, *, /, % (modulus) with examples
- [ ] Slide: Order of Operations — PEMDAS in programming, parentheses for clarity
- [ ] Slide: Type Coercion and Promotion — what happens when you mix integer and float
- [ ] Slide: Practical Example — calculate area of a circle (π × r²), payroll calculation, temperature conversion
- [ ] Slide: Practice — write expressions for: (a) total with tax, (b) average of three numbers, (c) remainder when dividing
- [ ] Slide: Part 5 divider — "Summary"

### Part 6: Summary and Wrap-Up (~20 min)
- [ ] Slide: Day 9 Takeaways — bullet list of key concepts
- [ ] Slide: Looking Ahead — what's coming in Day 10 (UML, security, ethics)
- [ ] Slide: Reminders — assignments due this week (Discussion, Structured Programming assignment, Applying Basic Formulas, Knowledge Check)
- [ ] Slide: Questions

**Estimated slide count: ~45 slides**

---

## Lecture 2 (Day 10): UML, Security, and Ethics — ~3 hours

### Part 1: Welcome and Agenda (~10 min)
- [ ] Slide: Title — "SDEV 120 Day 10 — UML, Security, and Ethics in Programming"
- [ ] Slide: Today We Will Cover — numbered agenda (4 parts)
- [ ] Slide: Part 1 divider — "Introduction to UML"

### Part 2: Introduction to UML (~40 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: What Is UML? — Unified Modeling Language, purpose, history (brief)
- [ ] Slide: Why Use UML? — standard notation, visual communication, design before coding, documentation
- [ ] Slide: Types of UML Diagrams — categorized into Structural and Behavioral
- [ ] Slide: Structural Diagrams — Class, Composite Structure, Object, Component, Deployment, Package (brief description of each)
- [ ] Slide: Behavioral Diagrams — Use Case, Sequence, Activity, State Machine, Communication, Timing, Interaction Overview (brief description of each)
- [ ] Slide: Which Diagrams Matter Most for This Course? — highlight Use Case (assignment focus), Class, Activity, Sequence
- [ ] Slide: Tools for Creating UML — Draw.io (primary tool for this course), brief mention of alternatives
- [ ] Slide: Part 2 divider — "Use Case Diagrams"

### Part 3: Use Case Diagrams Deep Dive (~60 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: What Is a Use Case Diagram? — definition, purpose, shows system functionality from user perspective
- [ ] Slide: Key Elements — System boundary, Actors, Use cases, Relationships (include, extend, generalization)
- [ ] Slide: Actors — who/what interacts with the system (stick figures, external systems)
- [ ] Slide: Use Cases — oval shapes representing functions/scenarios the system performs
- [ ] Slide: System Boundary — rectangle enclosing all use cases, defines scope
- [ ] Slide: Relationships — «include» (mandatory sub-flow), «extend» (optional/conditional sub-flow), generalization (inheritance)
- [ ] Slide: Step-by-Step Example 1 — Online Shopping System (identify actors: Customer, Admin, Payment System; identify use cases: Browse Products, Add to Cart, Checkout, etc.)
- [ ] Slide: Step-by-Step Example 1 (continued) — draw the diagram elements and relationships
- [ ] Slide: Step-by-Step Example 2 — Library Management System (actors: Patron, Librarian; use cases: Search Catalog, Check Out Book, Pay Fine, etc.)
- [ ] Slide: Step-by-Step Example 2 (continued) — diagram elements and relationships
- [ ] Slide: Draw.io Walkthrough — step-by-step instructions: open Draw.io, find UML shapes in left menu, place system boundary, add actors, add use cases, connect with lines, label relationships
- [ ] Slide: Common Mistakes in Use Case Diagrams — too much detail inside use cases, confusing actors with use cases, missing system boundary
- [ ] Slide: Practice Exercise — Create a use case diagram for an ATM system (actors: Customer, Bank; use cases: Withdraw, Deposit, Check Balance, Transfer)
- [ ] Slide: Practice Exercise (continued) — time for students to work, then review
- [ ] Slide: Part 3 divider — "Secure Programming"

### Part 4: Secure Programming and Ethics (~50 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: Why Security Matters in Programming — real-world consequences of insecure code (data breaches, financial loss, safety risks)
- [ ] Slide: The Threat Landscape — common vulnerabilities: injection, buffer overflow, weak authentication, insecure data storage
- [ ] Slide: Secure Programming Practices — input validation, least privilege, defense in depth, secure defaults, fail securely
- [ ] Slide: Input Validation — the most critical practice; never trust user input; examples of validation (range checks, type checks, length checks)
- [ ] Slide: Defense in Depth — multiple layers of security; no single point of failure
- [ ] Slide: Principle of Least Privilege — give code only the access it needs
- [ ] Slide: Secure Design Patterns — brief overview: fail-safe defaults, complete mediation, open design, separation of privilege
- [ ] Slide: Building Security into the SDLC — shift-left: requirements → design → implementation → testing → deployment → maintenance; security at every phase
- [ ] Slide: Security Testing — what it is, why it's different from functional testing
- [ ] Slide: Goals of Security Testing — identify vulnerabilities, verify security controls, ensure compliance, assess risk
- [ ] Slide: Types of Security Testing — vulnerability scanning, penetration testing, code review, fuzz testing
- [ ] Slide: Security Testing for Loopholes and Weaknesses — how to think like an attacker; common weaknesses (OWASP Top 10 at a high level)
- [ ] Slide: Part 4 divider — "Ethics in IT"

### Part 5: Ethics in IT (~20 min)
- [ ] Slide: Learning Objectives for this section
- [ ] Slide: Why Do Programmers Need a Code of Ethics? — power and responsibility of software; real-world impact on people
- [ ] Slide: Key Ethical Principles — ACM/IEEE Code of Ethics highlights: public safety, professional competence, confidentiality, integrity
- [ ] Slide: Ethical Dilemmas in Programming — examples: data privacy vs. convenience, security vs. usability, AI bias, surveillance
- [ ] Slide: Your Ethical Obligations as an IT Professional — discussion prompt linking to the week's discussion assignment
- [ ] Slide: Part 5 divider — "Summary"

### Part 6: Summary and Wrap-Up (~10 min)
- [ ] Slide: Day 10 Takeaways — bullet list of key concepts
- [ ] Slide: Module 5 Assignment Recap — all assignments listed with brief descriptions
- [ ] Slide: Group Project Reminder — next check-in milestone
- [ ] Slide: Questions

**Estimated slide count: ~50 slides**

---

## Verification Criteria

- Each slide deck follows the exact Marp YAML front-matter and CSS from `1.md:1-40`
- Every slide is separated by `---`
- Title slides use the scoped centering style
- Content slides use the base style (left-aligned, standard section)
- All Module 5 learning objectives are addressed across the two decks
- All Module 5 assignments are mentioned/reminded at appropriate points
- Appendix B content (spaghetti method) is covered with worked examples in Day 9
- UML Use Case Diagrams are covered with hands-on Draw.io guidance in Day 10
- Security and ethics topics prepare students for the discussion assignment
- Pacing allows for ~3 hours per deck including breaks and student practice

## Potential Risks and Mitigations

1. **Too much content for the time allotted**
   Mitigation: The practice exercises can be shortened or made homework if time runs short. The UML diagram types overview (Day 10, Part 2) can be compressed to a single slide with a reference handout.

2. **Appendix B restructuring is highly visual and hard to convey in slides**
   Mitigation: Use clear text-based descriptions of each step. Consider using Draw.io or ASCII art representations of the flowcharts within slides. The instructor should draw live if possible.

3. **Security/ethics topics are broad and could consume too much time**
   Mitigation: Keep each concept to one slide with a brief definition. Deeper exploration happens in the discussion assignment. Focus on definitions and "why it matters" rather than deep technical detail.

4. **Students may not have Draw.io experience**
   Mitigation: Include a step-by-step walkthrough slide. Consider a live demo during class. The practice exercise gives hands-on experience.

## Alternative Approaches

1. **Combine priming input into the structuring section**: Instead of a separate Part 4 on Day 9, weave priming input into the restructuring examples (show how priming reads naturally emerge from structured loops). This saves ~15 min but may reduce clarity.

2. **Flip the lecture order**: Cover UML and security on Day 9, and structuring problems on Day 10. This front-loads the more "new" material (UML is entirely new; structuring builds on Module 4). Trade-off: students get more time to practice restructuring before the assignment is due.

3. **Create a separate hands-on lab session**: Dedicate the last hour of Day 10 entirely to Draw.io practice and UML creation rather than covering security/ethics in lecture. Move security/ethics to a reading/video assignment. Trade-off: less lecture coverage but more practical skill development.
