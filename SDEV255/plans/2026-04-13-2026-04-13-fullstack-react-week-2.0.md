# Fullstack React Week: REST + React vs Next.js

## Objective

Cover fullstack development with React across two ~3-hour lectures. Lecture 1 builds a traditional MERN-style Bulletin Board System (React frontend + Express REST API backend, without MongoDB since databases haven't been covered yet). Lecture 2 rebuilds the same BBS using Next.js as an alternative fullstack framework. The same application built two ways creates a direct comparison that reinforces concepts and exposes students to industry-relevant tooling.

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
- RESTful API design with nested resources (posts and replies)
- Client-side navigation between list and detail views
- Next.js as an alternative fullstack framework
- Understanding when and why to choose one approach over the other

**Key constraint:** Databases have NOT been covered yet. All data will be in-memory on the server side. This keeps the focus on architecture and patterns rather than persistence.

---

## The Shared App: Bulletin Board System (BBS)

Both lectures build the same BBS to enable direct comparison.

**Why a BBS:**
- Fresh domain — breaks away from the task theme that ran through Lectures 3, 7, and 8
- Classic web application that students immediately understand (everyone has used a forum or message board)
- Introduces **nested resources** (posts contain replies) — teaches sub-resource REST patterns
- Requires **multiple views** (post list vs post detail) — teaches client-side navigation/routing
- Richer data model than simple CRUD — author, body content, timestamps, reply counts
- Maps well to the final project (course catalog with course details and enrolled students)

**Features (identical in both versions):**
- View all posts in a list (title, author, date, reply count)
- View a single post with all its replies
- Create a new post (title + body + author name)
- Reply to an existing post (body + author name)
- Delete a post (and its replies)

**Data model (in-memory):**

Post:
- `id` (auto-generated)
- `title` (string, required)
- `body` (string, required)
- `author` (string, required)
- `createdAt` (timestamp)
- `replies` (array of Reply objects)

Reply:
- `id` (auto-generated)
- `body` (string, required)
- `author` (string, required)
- `createdAt` (timestamp)

**REST endpoints:**
- `GET /api/posts` — list all posts (without full reply bodies, just reply count)
- `GET /api/posts/:id` — get one post with all its replies
- `POST /api/posts` — create a new post
- `POST /api/posts/:id/replies` — add a reply to a post
- `DELETE /api/posts/:id` — delete a post and its replies

**Key pedagogical value of this data model:**
- Nested resources teach that REST APIs can have sub-resources (`/posts/:id/replies`)
- The list endpoint returning a summary (reply count, not full replies) teaches API response shaping
- The detail endpoint loading full data teaches lazy loading patterns
- Multiple views (list vs detail) naturally introduces client-side routing/state-based navigation

---

## Lecture 1: REST + React (Traditional MERN-Style)

**Duration:** ~3 hours
**App:** Bulletin Board System

### Part 1: Fullstack Architecture Review (15 min)

- [ ] **Review the fullstack request lifecycle** from Lecture 6, now framed for React specifically: React component triggers fetch -> Express route -> controller -> model (in-memory) -> JSON response -> React updates state. This bridges Lectures 6, 7, 8, and today. Reference `6.md:505-515` for the end-to-end flow diagram.
- [ ] **Introduce the "ME" stack concept** (without MongoDB): Explain that MERN = MongoDB + Express + React + Node, but we are doing "ERN" today with in-memory data. Frame this as: same architecture, same patterns, just swapping the data layer later when databases are covered.
- [ ] **Introduce the BBS app concept**: Briefly describe what a bulletin board / forum is, show a visual of the two views (post list and post detail), and explain the data relationships (posts have replies). Emphasize this is a step up from simple CRUD because of the nested data.
- [ ] **Show the project structure** students will build: two separate directories (`bbs-api/` for Express backend, `bbs-client/` for React frontend), two dev servers, two `package.json` files. This is the traditional decoupled fullstack architecture.

### Part 2: Building the Express REST API (60 min)

- [ ] **Set up the Express project** (`bbs-api/`): `npm init`, install express and cors, create `server.js` with basic server setup. Reference `6.md:198-215` for the Node project setup pattern students have seen before.
- [ ] **Design RESTful endpoints** for the BBS: `GET /api/posts` (list all with reply counts), `GET /api/posts/:id` (single post with full replies), `POST /api/posts` (create post), `POST /api/posts/:id/replies` (add reply), `DELETE /api/posts/:id` (delete post). Explain REST conventions: nouns for resources, HTTP methods for actions, nested routes for sub-resources (`/posts/:id/replies`). Point out that the list endpoint should return a summary shape (title, author, date, reply count) while the detail endpoint returns full data — this teaches API response shaping.
- [ ] **Create in-memory data store**: An array of post objects, each containing a `replies` array. Include a helper to generate IDs (e.g., `Date.now()` or a counter). Seed with 2-3 sample posts with replies so the API has data to return immediately. Explain this is a stand-in for a database.
- [ ] **Implement GET /api/posts** (list all): Return posts without full reply bodies — map each post to a summary object that includes `replyCount: post.replies.length` instead of the full replies array. This teaches students to think about what data each view actually needs.
- [ ] **Implement GET /api/posts/:id** (get one): Find the post by id, return it with full replies. Return 404 when the post is not found. Show the response in browser.
- [ ] **Implement POST /api/posts** (create): Use `express.json()` middleware, validate required fields (`title`, `body`, `author`), create the post with an empty replies array, return 201 with the created post (including the server-generated id and timestamp). Reference `6.md:297-310` for req/res object patterns.
- [ ] **Implement POST /api/posts/:id/replies** (add reply): Find the parent post, validate the reply body, push the new reply object into the post's replies array, return 201 with the new reply. This is the key nested resource pattern.
- [ ] **Implement DELETE /api/posts/:id** (delete): Remove the post from the array (and its replies disappear with it). Return 200 or 204, 404 if not found.
- [ ] **Add CORS middleware**: Explain why browsers block cross-origin requests, install and configure the `cors` package. This is a critical fullstack concept that only matters when frontend and backend are on different ports.

### Part 3: Building the React Frontend (70 min)

- [ ] **Set up the React project** (`bbs-client/`): Use Vite to scaffold a React app. Reference `7.md:427-432` for the Vite setup pattern from React week.
- [ ] **Create the API service layer**: A separate file (e.g., `api/posts.js`) with functions like `getAllPosts()`, `getPost(id)`, `createPost(data)`, `createReply(postId, data)`, `deletePost(id)`. Each function uses `fetch()` with the full `http://localhost:3001/api/posts` URL. This reinforces the service layer pattern from `5.md:176-183`.
- [ ] **Implement simple client-side navigation**: Use a `currentView` state in App to switch between "list" and "detail" views. When a user clicks a post, set `currentView` to `{ type: "detail", postId: id }`. This avoids introducing React Router while still teaching the concept of view switching. Reference `8.md:127-160` for conditional rendering patterns.
- [ ] **Build PostList component**: Fetch all posts with useEffect on mount. Display loading state, error state, and a list of post summaries (title, author, date, reply count). Each post is clickable to navigate to the detail view. Reference `8.md:537-560` for the useEffect fetch pattern and `8.md:169-217` for list rendering with .map() and keys.
- [ ] **Build PostDetail component**: Receives `postId` as a prop. Fetches the full post (with replies) using `getPost(id)`. Displays the post title, body, author, and date. Renders all replies below. Shows a "Back to list" button that resets the view to the list. Reference `8.md:571-592` for loading/error state handling.
- [ ] **Build ReplyList component**: Renders the array of replies for the current post. Each reply shows author, body, and date. Simple list rendering with .map().
- [ ] **Build NewPostForm component**: Controlled form with fields for title, body, and author. On submit, calls `createPost()`. On success, navigate back to the list view (reset currentView). Reference `8.md:336-358` for controlled form patterns.
- [ ] **Build ReplyForm component**: Controlled form with fields for body and author. On submit, calls `createReply(postId, data)`. On success, re-fetch the post detail to show the new reply.
- [ ] **Add a delete button** on the PostDetail view: Calls `deletePost(id)`. On success, navigate back to the list. Optionally add a confirmation step.
- [ ] **Wire everything together in App**: App manages `currentView` state and conditionally renders either PostList or PostDetail based on the current view. This is the lifted state pattern from `8.md:738-760`.

### Part 4: Full Integration and Debugging (20 min)

- [ ] **Run both servers simultaneously**: Terminal tab 1 for Express (port 3001), Terminal tab 2 for Vite dev server (port 5173). Demonstrate the full round trip: create a post in React, see it appear in the list, click into it, add a reply, see the reply appear, go back to list and see the reply count updated.
- [ ] **Demonstrate error scenarios**: Stop the Express server and show the React error handling in action. Try submitting a post with missing fields and show validation. Try viewing a post that doesn't exist (404 handling).
- [ ] **Review the architecture**: Draw the separation on screen — React handles UI/state/view navigation, Express handles API/business logic/data. Two codebases, two servers, one application. Highlight the nested resource pattern (posts/:id/replies) as a key takeaway.

### Lecture 1 Wrap-Up (15 min)

- [ ] **Objective check**: Students should be able to trace a full request from React component through fetch to Express route and back, including nested resources.
- [ ] **Preview Lecture 2**: "Same BBS, different framework. Next.js combines what we just built into a single project."

---

## Lecture 2: Next.js (Alternative Fullstack Framework)

**Duration:** ~3 hours
**App:** Same Bulletin Board System

### Part 1: Why Next.js and What It Changes (20 min)

- [ ] **Recap Lecture 1 architecture**: Two projects, two servers, CORS configuration, manual API service layer, manual client-side view switching, separate deployments. This worked, but it introduced friction (CORS, two package.json files, two build processes, proxy configuration, no real routing).
- [ ] **Introduce Next.js as a fullstack React framework**: Explain that Next.js lets you write React components AND server-side API routes in the same project. One codebase, one dev server, no CORS issues, file-system-based routing replaces manual view switching.
- [ ] **Key Next.js concepts to cover**: App Router (modern approach), file-system routing (folders = routes, so `/posts` and `/posts/[id]` are just folders), Server Components vs Client Components, API Routes (Route Handlers), shared types/data between client and server.
- [ ] **Show the project structure comparison**: Side-by-side view of Lecture 1's two-project structure vs Next.js's single-project structure. Emphasize: same concepts (REST endpoints, React components, fetch), just organized differently. The BBS naturally maps to Next.js routes: `/` = post list, `/posts/[id]` = post detail.
- [ ] **Discuss the tradeoffs honestly**: Next.js advantages (simpler deployment, no CORS, built-in routing, SSR capability, shared types). Next.js costs (more magic/abstraction, Server vs Client Component learning curve, framework lock-in, opinionated structure). Reference the course's MVC discussion from `6.md:374-383` as the conceptual foundation.

### Part 2: Setting Up Next.js and API Routes (45 min)

- [ ] **Create the Next.js project**: Use `npx create-next-app` with App Router. Walk through the generated structure: `app/` directory, `layout.js`, `page.js`, `api/` folder.
- [ ] **Explain Server vs Client Components**: By default, components in Next.js App Router are Server Components (run on the server, no useState/useEffect). Mark components that need interactivity with `"use client"`. This is the biggest mental shift from Lecture 1. Rule of thumb: "If it has useState, useEffect, or event handlers, it needs 'use client'."
- [ ] **Build API routes (Route Handlers)**: Create `app/api/posts/route.js` for GET (list all) and POST (create). Create `app/api/posts/[id]/route.js` for GET (one post) and DELETE. Create `app/api/posts/[id]/replies/route.js` for POST (add reply). These use the same REST patterns from Lecture 1 but with Next.js's `NextResponse` and `NextRequest` objects. Reuse the same in-memory data store pattern.
- [ ] **Test API routes**: Use the browser or curl to verify each endpoint works. Point out: no CORS needed because the API and frontend share the same origin.

### Part 3: Building the React UI in Next.js (70 min)

- [ ] **Create the post list page** (`app/page.js`): This will be a Server Component that fetches all posts directly on the server (no useEffect needed for the initial load). Show how `fetch()` works on the server in Next.js. Render the post list with links to `/posts/[id]`.
- [ ] **Create the post detail page** (`app/posts/[id]/page.js`): Another Server Component that receives the `id` param from the URL, fetches the full post with replies on the server, and renders it. This replaces the manual `currentView` state switching from Lecture 1 with real URL-based routing.
- [ ] **Create Client Components for interactivity**: `NewPostForm` (needs useState for form state, marked `"use client"`), `ReplyForm` (needs useState, marked `"use client"`), `DeletePostButton` (needs onClick handler, marked `"use client"`). Import these into the server pages.
- [ ] **Implement NewPostForm with fetch POST**: Create a new post by fetching `/api/posts` from the client component. On success, use `router.push("/")` (Next.js built-in) to navigate to the updated list. Show how `useRouter` from `next/navigation` replaces manual view state management.
- [ ] **Implement ReplyForm**: Add a reply by fetching `/api/posts/[id]/replies`. On success, use `router.refresh()` to re-fetch server data and show the new reply without a full page navigation.
- [ ] **Implement DeletePostButton**: Delete by fetching `/api/posts/[id]` with DELETE method. On success, `router.push("/")` to return to the list.
- [ ] **Add loading UI**: Next.js provides `loading.js` files for automatic loading states (one in `app/loading.js` for the list, one in `app/posts/[id]/loading.js` for the detail page). Show how this replaces the manual `useState(true)` loading pattern from Lecture 1.
- [ ] **Compare to Lecture 1's React code**: Show that the component logic is nearly identical (same JSX, same state management, same fetch calls). The differences are: file-system routing replaces manual view switching, Server Components fetch data without useEffect, one project instead of two, no CORS configuration.

### Part 4: Comparison and Industry Context (30 min)

- [ ] **Side-by-side architecture comparison**: Draw both architectures on screen. Traditional MERN: separate client + server, REST API, CORS, manual view switching, two deployments. Next.js: unified project, API routes, file-system routing, same origin, one deployment.
- [ ] **When to use each approach**:
  - Traditional MERN/REST: When you want maximum flexibility, separate teams for frontend/backend, microservices architecture, or when the frontend framework might change.
  - Next.js: When you want developer productivity, simpler deployment, SEO/SSR needs, built-in routing, or when your team is all-React.
  - Other alternatives worth mentioning briefly: Remix (similar to Next.js, simpler), SvelteKit (if they encounter Svelte later), Nuxt (Vue equivalent).
- [ ] **Connect back to the course and final project**: Students' final project (course registration app) maps well to the BBS pattern — courses are like posts (list view + detail view), enrolled students are like replies. The patterns are the same regardless of framework choice.
- [ ] **Discuss what happens when databases are added**: Both approaches connect to MongoDB/PostgreSQL the same way on the server side. The in-memory store from this week gets replaced with database calls. The frontend code doesn't change. The nested relationship (posts → replies) maps directly to database relations (one-to-many).

### Lecture 2 Wrap-Up (15 min)

- [ ] **Objective check**: Students should be able to explain the architectural difference between traditional MERN and Next.js, and understand when each is appropriate.
- [ ] **Final takeaway**: The concepts (REST, components, state, fetch, nested resources) matter more than the framework. Learn the patterns, and you can work in any fullstack stack.

---

## Verification Criteria

### Lecture 1 (REST + React)
- Students can explain why CORS is needed and how to configure it
- Students can design RESTful endpoints including nested sub-resources
- Students can build an Express API that handles CRUD operations with nested data
- Students can connect a React frontend to a separate Express backend
- Students can implement client-side view navigation without a router library
- Students can trace a request from React fetch through Express route to response

### Lecture 2 (Next.js)
- Students can explain the difference between Server Components and Client Components
- Students can create API routes in a Next.js App Router project
- Students can build a fullstack CRUD app with nested resources in a single Next.js project
- Students can use file-system routing to replace manual view state management
- Students can articulate at least 3 tradeoffs between traditional MERN and Next.js
- Students understand when each approach is appropriate

### Overall Week
- Students can build the same application using two different fullstack architectures
- Students recognize that the underlying patterns (REST, components, state, fetch, nested resources) are framework-agnostic
- Students are prepared to make an informed architecture choice for their final project
- Students understand how the BBS's post/reply relationship maps to database one-to-many relations they will learn later

---

## Potential Risks and Mitigations

### Risk 1: Students struggle with running two dev servers simultaneously
**Likelihood:** Medium
**Impact:** High — blocks all of Lecture 1's integration work
**Mitigation:** Provide a clear terminal setup guide at the start. Consider using a single terminal with concurrent commands (`npm-run-all` or separate VS Code terminal tabs). Have a screenshot/diagram of what "both servers running" looks like.

### Risk 2: CORS issues consume too much time
**Likelihood:** High
**Impact:** Medium — frustrating but fixable
**Mitigation:** Install and configure CORS early in the Express setup. Have the exact configuration ready to paste if live coding goes wrong. Frame CORS as a learning moment, not a roadblock.

### Risk 3: Nested resources add complexity that slows the pace
**Likelihood:** Medium
**Impact:** Medium — the BBS has more moving parts than a simple CRUD app
**Mitigation:** Build incrementally. Get the flat post CRUD working first (list, create, delete), then add replies as a second pass. If time is tight, replies can become a stretch goal rather than a requirement.

### Risk 4: Client-side navigation without React Router is confusing
**Likelihood:** Low-Medium
**Impact:** Low — the currentView state pattern is straightforward
**Mitigation:** Frame it as conditional rendering (which students already know from `8.md:127-160`) applied to whole views. Keep it simple: a `view` state variable that is either `"list"`, `"form"`, or `{ type: "detail", id: 5 }`. Emphasize that Next.js Lecture 2 will solve this properly with real routing.

### Risk 5: Next.js Server vs Client Component confusion
**Likelihood:** High
**Impact:** High — fundamental misunderstanding of the framework
**Mitigation:** Introduce the concept early with clear rules of thumb: "If it has useState, useEffect, or event handlers, it needs 'use client'." Start with mostly client components to match their existing React knowledge, then show server component benefits for the data-fetching pages.

### Risk 6: Lecture 2 feels repetitive if Lecture 1 went well
**Likelihood:** Medium
**Impact:** Low — some repetition is intentional for comparison
**Mitigation:** Lean into the comparison angle. Make it explicit: "Notice this is the same fetch call, same state update, same JSX — just organized differently." Use speed for the rebuild parts and slow down for the genuinely new Next.js concepts (Server Components, API routes, file-system routing, loading.js).

### Risk 7: Running out of time in either lecture
**Likelihood:** Medium
**Impact:** Medium — core concepts may be rushed
**Mitigation:** Priority order for Lecture 1: Express API (GET + POST for posts) > React frontend (list + create post) > post detail view > replies > delete. Priority order for Lecture 2: API routes > Server Component pages > Client Component forms > loading.js > comparison. Have a "minimum viable demo" for each lecture that covers at least post list + create post end-to-end.

### Risk 8: Students confuse Next.js API routes with Express routes
**Likelihood:** Low-Medium
**Impact:** Low — concepts transfer well
**Mitigation:** Explicitly map Next.js Route Handler concepts to Express equivalents. Show the same POST handler written both ways. Emphasize: "Same REST pattern, different syntax."

---

## Alternative Approaches

### Alternative 1: Use a different app instead of BBS
A Notes app, Contact List, or Book Tracker would all work equally well. The BBS is recommended because it introduces nested resources and multiple views, which are more representative of real web applications. If the BBS feels too complex, a simpler Guestbook (posts only, no replies) reduces scope while keeping the fresh domain.

### Alternative 2: Use JSON Server instead of building Express API from scratch
**Trade-offs:** JSON Server gives you a full REST API in seconds with zero code. This saves ~30 minutes in Lecture 1 but loses the teaching value of students seeing how REST endpoints are actually implemented, and doesn't naturally support nested sub-resources like replies. **Recommendation:** Build the Express API from scratch. Students need to understand what's behind the API, not just consume one.

### Alternative 3: Skip Next.js and go deeper into MERN patterns
**Trade-offs:** More time for React+Express mastery, but students miss exposure to the most popular React fullstack framework in industry. Next.js is increasingly the default for new React projects. **Recommendation:** Keep Next.js. The comparison is pedagogically valuable and industry-relevant.

### Alternative 4: Use Pages Router instead of App Router in Next.js
**Trade-offs:** Pages Router is simpler and has more tutorials/resources. App Router is the current default and what students will encounter in new projects. **Recommendation:** Use App Router since it's the modern standard, but acknowledge Pages Router exists.

### Alternative 5: Add a brief database layer (e.g., lowdb or better-sqlite3)
**Trade-offs:** Makes the app feel more "real" but adds complexity and time. Databases are a separate module. **Recommendation:** Keep in-memory storage. Mention explicitly: "When we cover databases, you'll replace this array with database calls and nothing else changes." The post/reply relationship maps directly to one-to-many database relations.

### Alternative 6: Introduce React Router in Lecture 1 instead of manual view switching
**Trade-offs:** React Router is the standard way to handle navigation in React SPAs. However, it's another library to learn and configure, and Next.js Lecture 2 will make it feel redundant. **Recommendation:** Use manual view switching (currentView state) in Lecture 1 for simplicity, then show how Next.js file-system routing solves the same problem. If students ask about React Router, acknowledge it and mention it as an option for traditional MERN projects.
