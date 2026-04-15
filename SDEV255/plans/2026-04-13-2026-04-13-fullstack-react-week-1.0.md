# Fullstack React Week: REST + React vs Next.js

## Objective

Cover fullstack development with React across two ~3-hour lectures. Lecture 1 builds a traditional MERN-style app (React frontend + Express REST API backend, without MongoDB since databases haven't been covered yet). Lecture 2 rebuilds the same app using Next.js as an alternative fullstack framework. The same application built two ways creates a direct comparison that reinforces concepts and exposes students to industry-relevant tooling.

## Context Summary

**Course progression so far:**
- Lectures 1-3: JavaScript fundamentals, OOP, DOM, JSON, form validation
- Lecture 5: Client-side APIs, async/await, Fetch, Promises, WebSockets
- Lecture 6: Node.js, Express, MVC architecture, fullstack integration, Final Project launch
- Lectures 7-8: React foundations (JSX, components, props, useState) and React patterns (lists, forms, useEffect, composition)

**What students can already do:**
- Build Express routes that return JSON
- Build React components with state, props, forms, and fetch
- Use async/await and handle loading/error states
- Organize code with MVC separation

**What this week adds:**
- Connecting a React frontend to an Express backend end-to-end
- CORS, proxying, and environment configuration
- RESTful API design patterns
- Next.js as an alternative fullstack framework
- Understanding when and why to choose one approach over the other

**Key constraint:** Databases have NOT been covered yet. All data will be in-memory on the server side. This keeps the focus on architecture and patterns rather than persistence.

---

## Lecture 1: REST + React (Traditional MERN-Style)

**Duration:** ~3 hours
**App:** Task Manager (CRUD for tasks - consistent with course-long task theme)

### Part 1: Fullstack Architecture Review (15 min)

- [ ] **Review the fullstack request lifecycle** from Lecture 6, now framed for React specifically: React component triggers fetch -> Express route -> controller -> model (in-memory) -> JSON response -> React updates state. This bridges Lectures 6, 7, 8, and today. Reference `6.md:505-515` for the end-to-end flow diagram.
- [ ] **Introduce the "ME" stack concept** (without MongoDB): Explain that MERN = MongoDB + Express + React + Node, but we are doing "ERN" today with in-memory data. Frame this as: same architecture, same patterns, just swapping the data layer later when databases are covered.
- [ ] **Show the project structure** students will build: two separate directories (`task-api/` for Express backend, `task-client/` for React frontend), two dev servers, two `package.json` files. This is the traditional decoupled fullstack architecture.

### Part 2: Building the Express REST API (60 min)

- [ ] **Set up the Express project** (`task-api/`): `npm init`, install express and cors, create `server.js` with basic server setup. Reference `6.md:198-215` for the Node project setup pattern students have seen before.
- [ ] **Design RESTful endpoints** for the Task CRUD app: GET /api/tasks (list all), GET /api/tasks/:id (get one), POST /api/tasks (create), PUT /api/tasks/:id (update), DELETE /api/tasks/:id (delete). Explain REST conventions: nouns for resources, HTTP methods for actions, JSON for request/response bodies.
- [ ] **Create in-memory data store**: A simple array of task objects with `id`, `title`, `completed`, `priority`. Include a helper to generate IDs (e.g., `Date.now()` or a counter). Explain this is a stand-in for a database.
- [ ] **Implement GET routes** (list all, get one): Wire up controller functions that read from the in-memory array. Return 404 when a task is not found. Show the responses in browser/Postman.
- [ ] **Implement POST route** (create): Use `express.json()` middleware, validate required fields (`title`), return 201 with the created task (including the server-generated id). Reference `6.md:297-310` for req/res object patterns.
- [ ] **Implement PUT and DELETE routes** (update, delete): Update fields on existing task, remove task from array. Return appropriate status codes (200 for update, 204 or 200 for delete, 404 for not found).
- [ ] **Add CORS middleware**: Explain why browsers block cross-origin requests, install and configure the `cors` package. This is a critical fullstack concept that only matters when frontend and backend are on different ports.

### Part 3: Building the React Frontend (70 min)

- [ ] **Set up the React project** (`task-client/`): Use Vite to scaffold a React app. Reference `7.md:427-432` for the Vite setup pattern from React week.
- [ ] **Create the component structure**: `App` (top-level state holder), `TaskList` (renders all tasks), `TaskItem` (single task with toggle/delete), `TaskForm` (add new task), `TaskStats` (count summary). This reuses the composition patterns from `8.md:738-760` (lifting state up).
- [ ] **Create an API service layer**: A separate file (e.g., `api/tasks.js`) with functions like `getAllTasks()`, `createTask(data)`, `updateTask(id, data)`, `deleteTask(id)`. Each function uses `fetch()` with the full `http://localhost:3001/api/tasks` URL. This reinforces the service layer pattern from `5.md:176-183`.
- [ ] **Build TaskList with useEffect fetch**: On mount, call `getAllTasks()` from the API service. Display loading state, error state, and the task list. Reference `8.md:537-560` for the useEffect fetch pattern.
- [ ] **Build TaskForm with POST**: Controlled form that calls `createTask()` on submit. On success, re-fetch the task list (or optimistically update state). Reference `8.md:336-358` for controlled form patterns.
- [ ] **Build TaskItem with toggle and delete**: Toggle completion calls `updateTask(id, { completed: !task.completed })`. Delete button calls `deleteTask(id)`. Both re-fetch or update local state after success.
- [ ] **Wire everything together in App**: Lifted state pattern where App holds `tasks` and passes down to children. Reference `8.md:746-760` for the lifting state up pattern.

### Part 4: Full Integration and Debugging (20 min)

- [ ] **Run both servers simultaneously**: Terminal tab 1 for Express (port 3001), Terminal tab 2 for Vite dev server (port 5173). Demonstrate the full round trip: add a task in React, see it stored in the Express server's memory, refresh to confirm persistence within the server session.
- [ ] **Demonstrate error scenarios**: Stop the Express server and show the React error handling in action. Try submitting an empty title and show validation. Try deleting a non-existent task.
- [ ] **Review the architecture**: Draw the separation on screen - React handles UI/state/routing, Express handles API/business logic/data. Two codebases, two servers, one application.

### Lecture 1 Wrap-Up (15 min)

- [ ] **Objective check**: Students should be able to trace a full CRUD operation from React component through fetch to Express route and back.
- [ ] **Preview Lecture 2**: "Same app, different framework. Next.js combines what we just built into a single project."

---

## Lecture 2: Next.js (Alternative Fullstack Framework)

**Duration:** ~3 hours
**App:** Same Task Manager (CRUD for tasks)

### Part 1: Why Next.js and What It Changes (20 min)

- [ ] **Recap Lecture 1 architecture**: Two projects, two servers, CORS configuration, manual API service layer, separate deployments. This worked, but it introduced friction (CORS, two package.json files, two build processes, proxy configuration).
- [ ] **Introduce Next.js as a fullstack React framework**: Explain that Next.js lets you write React components AND server-side API routes in the same project. One codebase, one dev server, no CORS issues.
- [ ] **Key Next.js concepts to cover**: App Router (modern approach), file-system routing (folders = routes), Server Components vs Client Components, API Routes (Route Handlers), shared types/data between client and server.
- [ ] **Show the project structure comparison**: Side-by-side view of Lecture 1's two-project structure vs Next.js's single-project structure. Emphasize: same concepts (REST endpoints, React components, fetch), just organized differently.
- [ ] **Discuss the tradeoffs honestly**: Next.js advantages (simpler deployment, no CORS, shared types, SSR capability, built-in optimization). Next.js costs (more magic/abstraction, learning curve, framework lock-in, opinionated structure). Reference the course's MVC discussion from `6.md:374-383` as the conceptual foundation.

### Part 2: Setting Up Next.js and API Routes (45 min)

- [ ] **Create the Next.js project**: Use `npx create-next-app` with App Router. Walk through the generated structure: `app/` directory, `layout.js`, `page.js`, `api/` folder.
- [ ] **Explain Server vs Client Components**: By default, components in Next.js App Router are Server Components (run on the server, no useState/useEffect). Mark components that need interactivity with `"use client"`. This is the biggest mental shift from Lecture 1.
- [ ] **Build API routes (Route Handlers)**: Create `app/api/tasks/route.js` for GET (list all) and POST (create). Create `app/api/tasks/[id]/route.js` for GET (one), PUT (update), DELETE (delete). These use the same Express-like patterns (request, response, JSON) but use Next.js's `NextResponse` and `NextRequest` objects. Reuse the same in-memory data store pattern from Lecture 1.
- [ ] **Test API routes**: Use the browser or curl to verify each endpoint works. Point out: no CORS needed because the API and frontend share the same origin.

### Part 3: Building the React UI in Next.js (70 min)

- [ ] **Create the main page component** (`app/page.js`): This will be a Server Component that fetches tasks directly (no useEffect needed for the initial load). Show how `fetch()` works on the server in Next.js.
- [ ] **Create Client Components for interactivity**: `TaskForm` (needs useState for form state, marked `"use client"`), `TaskItem` (needs onClick handlers for toggle/delete, marked `"use client"`). Import these into the server page.
- [ ] **Implement the TaskForm with server action or fetch POST**: Create a new task by fetching `/api/tasks` from the client component. On success, use `router.refresh()` (Next.js built-in) to re-fetch server data, or manage local state.
- [ ] **Implement toggle and delete**: Client-side fetch calls to PUT and DELETE endpoints. After success, refresh the page data.
- [ ] **Add loading UI**: Next.js provides `loading.js` files for automatic loading states. Show how this replaces the manual `useState(true)` loading pattern from Lecture 1.
- [ ] **Compare to Lecture 1's React code**: Show that the component logic is nearly identical. The difference is in how data flows (server components fetch directly vs client components use useEffect) and project organization (single project vs two projects).

### Part 4: Comparison and Industry Context (30 min)

- [ ] **Side-by-side architecture comparison**: Draw both architectures on screen. Traditional MERN: separate client + server, REST API, CORS, two deployments. Next.js: unified project, API routes, same origin, one deployment.
- [ ] **When to use each approach**:
  - Traditional MERN/REST: When you want maximum flexibility, separate teams for frontend/backend, microservices architecture, or when the frontend framework might change.
  - Next.js: When you want developer productivity, simpler deployment, SEO/SSR needs, or when your team is all-React.
  - Other alternatives worth mentioning briefly: Remix (similar to Next.js), SvelteKit (if they encounter Svelte later), Nuxt (Vue equivalent).
- [ ] **Connect back to the course and final project**: Students' final project (course registration app) can use either approach. The patterns are the same: REST endpoints, React components, fetch, state management. The framework choice is an implementation detail.
- [ ] **Discuss what happens when databases are added**: Both approaches connect to MongoDB/PostgreSQL the same way on the server side. The in-memory store from this week gets replaced with database calls. The frontend code doesn't change.

### Lecture 2 Wrap-Up (15 min)

- [ ] **Objective check**: Students should be able to explain the architectural difference between traditional MERN and Next.js, and understand when each is appropriate.
- [ ] **Final takeaway**: The concepts (REST, components, state, fetch) matter more than the framework. Learn the patterns, and you can work in any fullstack stack.

---

## The Shared App: Task Manager

Both lectures build the same app to enable direct comparison.

**Features (identical in both versions):**
- View all tasks (title, completed status, priority)
- Add a new task (title required, priority optional)
- Toggle task completion
- Delete a task
- See task count summary

**Data model (in-memory):**
- `id` (auto-generated)
- `title` (string, required)
- `completed` (boolean, default false)
- `priority` ("low" | "normal" | "high", default "normal")
- `createdAt` (timestamp)

**Why this app works:**
- Consistent with the task theme used throughout the course (Lectures 3, 7, 8)
- Simple enough to complete in ~3 hours per lecture
- Rich enough to demonstrate all CRUD operations
- Maps directly to the final project's course management CRUD

---

## Verification Criteria

### Lecture 1 (REST + React)
- Students can explain why CORS is needed and how to configure it
- Students can design RESTful endpoints for a CRUD resource
- Students can build an Express API that handles all four CRUD operations
- Students can connect a React frontend to a separate Express backend
- Students can trace a request from React fetch through Express route to response

### Lecture 2 (Next.js)
- Students can explain the difference between Server Components and Client Components
- Students can create API routes in a Next.js App Router project
- Students can build a fullstack CRUD app in a single Next.js project
- Students can articulate at least 3 tradeoffs between traditional MERN and Next.js
- Students understand when each approach is appropriate

### Overall Week
- Students can build the same application using two different fullstack architectures
- Students recognize that the underlying patterns (REST, components, state, fetch) are framework-agnostic
- Students are prepared to make an informed architecture choice for their final project

---

## Potential Risks and Mitigations

### Risk 1: Students struggle with running two dev servers simultaneously
**Likelihood:** Medium
**Impact:** High - blocks all of Lecture 1's integration work
**Mitigation:** Provide a clear terminal setup guide at the start. Consider using a single terminal with concurrent commands (`npm-run-all` or separate VS Code terminal tabs). Have a screenshot/diagram of what "both servers running" looks like.

### Risk 2: CORS issues consume too much time
**Likelihood:** High
**Impact:** Medium - frustrating but fixable
**Mitigation:** Install and configure CORS early in the Express setup. Have the exact configuration ready to paste if live coding goes wrong. Frame CORS as a learning moment, not a roadblock.

### Risk 3: Next.js Server vs Client Component confusion
**Likelihood:** High
**Impact:** High - fundamental misunderstanding of the framework
**Mitigation:** Introduce the concept early with clear rules of thumb: "If it has useState, useEffect, or event handlers, it needs 'use client'." Start with mostly client components to match their existing React knowledge, then show server component benefits.

### Risk 4: Lecture 2 feels repetitive if Lecture 1 went well
**Likelihood:** Medium
**Impact:** Low - some repetition is intentional for comparison
**Mitigation:** Lean into the comparison angle. Make it explicit: "Notice this is the same fetch call, same state update, same JSX - just organized differently." Use speed for the rebuild parts and slow down for the genuinely new Next.js concepts (Server Components, API routes, file-system routing).

### Risk 5: Running out of time in either lecture
**Likelihood:** Medium
**Impact:** Medium - core concepts may be rushed
**Mitigation:** Priority order for Lecture 1: Express API (GET + POST) > React frontend (fetch + display) > PUT/DELETE > full integration. Priority order for Lecture 2: API routes > Client Components > Server Components > comparison. Have a "minimum viable demo" for each lecture that covers at least GET + POST end-to-end.

### Risk 6: Students confuse Next.js API routes with Express routes
**Likelihood:** Low-Medium
**Impact:** Low - concepts transfer well
**Mitigation:** Explicitly map Next.js Route Handler concepts to Express equivalents. Show the same POST handler written both ways. Emphasize: "Same REST pattern, different syntax."

---

## Alternative Approaches

### Alternative 1: Use a different app instead of Task Manager
A Notes app, Contact List, or Book Tracker would all work equally well. The Task Manager is recommended because it maintains continuity with the task theme from Lectures 3, 7, and 8. If students are fatigued by tasks, a simple Course Catalog mini-app (connecting to the final project theme) would also work.

### Alternative 2: Use JSON Server instead of building Express API from scratch
**Trade-offs:** JSON Server gives you a full REST API in seconds with zero code. This saves ~30 minutes in Lecture 1 but loses the teaching value of students seeing how REST endpoints are actually implemented. **Recommendation:** Build the Express API from scratch. Students need to understand what's behind the API, not just consume one.

### Alternative 3: Skip Next.js and go deeper into MERN patterns
**Trade-offs:** More time for React+Express mastery, but students miss exposure to the most popular React fullstack framework in industry. Next.js is increasingly the default for new React projects. **Recommendation:** Keep Next.js. The comparison is pedagogically valuable and industry-relevant.

### Alternative 4: Use Pages Router instead of App Router in Next.js
**Trade-offs:** Pages Router is simpler and has more tutorials/resources. App Router is the current default and what students will encounter in new projects. **Recommendation:** Use App Router since it's the modern standard, but acknowledge Pages Router exists.

### Alternative 5: Add a brief database layer (e.g., lowdb or better-sqlite3)
**Trade-offs:** Makes the app feel more "real" but adds complexity and time. Databases are a separate module. **Recommendation:** Keep in-memory storage. Mention explicitly: "When we cover databases, you'll replace this array with database calls and nothing else changes."
