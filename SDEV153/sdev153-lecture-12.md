---
marp: true
theme: gaia
class: invert
paginate: true
---

<style>
section {
	font-size: 1.9rem;
}

h1 {
	font-size: 3.5rem !important;
	height: 100%;
	text-align: center;
	display: flex;
	justify-content: center;
	align-items: center;
}

h2 {
	font-size: 2.25rem !important;
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

# HTTP & Client-Server Architecture

Understanding how the web works

---

# Part 1 - Client-Server Model

---

## What is Client-Server Architecture?

**Client-Server:** A computing model where tasks are divided between:

- **Client:** Requests services or resources
- **Server:** Provides services or resources

**Examples:**

- Browser (client) ↔ Web server
- Email app (client) ↔ Email server
- Mobile app (client) ↔ API server

---

## The Web's Client-Server Model

```
┌─────────────┐                    ┌─────────────┐
│   Browser   │                    │ Web Server  │
│  (Client)   │                    │             │
│             │                    │             │
│  - Chrome   │ ──── Request ────> │ - Apache    │
│  - Firefox  │                    │ - Nginx     │
│  - Safari   │ <─── Response ──── │ - IIS       │
│             │                    │             │
└─────────────┘                    └─────────────┘
```

**Client:** Your web browser  
**Server:** Computer hosting the website

---

## How You Fit In

**What you've been building:**

- HTML files (structure)
- CSS files (styling)
- These files live on a **server**

**Everything else:**

- How browsers **request** these files
- How servers **respond** with files
- The protocol that makes it all work: **HTTP**

---

## Real-World Analogy

**Restaurant model:**

- **You (Client):** Order food from menu
- **Waiter (HTTP):** Takes order, brings food
- **Kitchen (Server):** Prepares your order

**Web model:**

- **Browser (Client):** Requests webpage
- **HTTP (Protocol):** Carries request/response
- **Server:** Sends back HTML/CSS/images

---

# Part 2 - What is HTTP?

---

## HTTP Definition

**HTTP:** HyperText Transfer Protocol

- **Protocol:** Set of rules for communication
- **HyperText:** Documents with links (HTML)
- **Transfer:** Moving data between client and server

**Purpose:** Defines how messages are formatted and transmitted on the web

**Created:** 1991 by Tim Berners-Lee (inventor of the web)

---

## Why HTTP Matters

**Every web interaction uses HTTP:**

- Loading a webpage
- Submitting a form
- Clicking a link
- Loading an image
- Fetching CSS files
- API calls

**Without HTTP:** No web communication!

---

## HTTP vs HTTPS

**HTTP:** Plain text communication

- Anyone can read the data
- Not secure for sensitive info

**HTTPS:** Encrypted communication

- Data is scrambled
- Secure for passwords, credit cards, personal info
- Shows padlock 🔒 in browser

**Always use HTTPS** for production websites!

---

## HTTP is Just Text

**That's it. HTTP is literally just plain text.**

Here's a complete HTTP request:

```
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Chrome
```

Here's a complete HTTP response:

```
HTTP/1.1 200 OK
Content-Type: text/html

<html><body>Hello!</body></html>
```

**No magic. No binary. Just text.**

---

## How HTTP Works: The Basics

1. **You type URL:** `https://example.com`
2. **Browser sends HTTP request** (just text)
3. **Server processes request**
4. **Server sends HTTP response** (just text)
5. **Browser displays the webpage**

---

# Part 3 - Request-Response Cycle

---

## The Request-Response Cycle

```
┌──────────┐                           ┌──────────┐
│ Browser  │                           │  Server  │
└──────────┘                           └──────────┘
     │                                       │
     │  1. HTTP Request                      │
     │  GET /index.html HTTP/1.1             │
     │────────────────────────────────────>  │
     │                                       │
     │                                   2. Process
     │                                       │
     │  3. HTTP Response                     │
     │  200 OK                               │
     │  <html>...</html>                     │
     │ <──────────────────────────────────   │
     │                                       │
  4. Display                                 │
     │                                       │
```

---

## Anatomy of an HTTP Request

**That's really it - a request is just a few lines:**

```http
GET /about.html HTTP/1.1
Host: www.example.com
```

**What each line means:**

- `GET` - What method (retrieve data)
- `/about.html` - What resource
- `HTTP/1.1` - Protocol version
- `Host:` - What domain

You can add more headers, but these are the essentials.

---

## A Real Request Example

```http
GET /about.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows)
Accept: text/html
```

Browser sends this text to server. That's the whole request!

---

## Anatomy of an HTTP Response

**A response is also just text:**

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<html>...</html>
```

**What each part means:**

- `HTTP/1.1 200 OK` - Status (success!)
- Headers describe the content
- Blank line
- Then the actual HTML/CSS/data

---

## A Real Response Example

```http
HTTP/1.1 200 OK
Content-Type: text/html

<!DOCTYPE html>
<html>
<head>
    <title>About Us</title>
</head>
<body>
    <h1>Welcome!</h1>
</body>
</html>
```

Server sends this text back to browser. Browser reads it, displays the HTML. Done!

---

## Request-Response in Action

**When you visit a page with CSS and images:**

```
Request 1: GET /index.html     → Response: HTML file
Request 2: GET /style.css      → Response: CSS file
Request 3: GET /logo.png       → Response: Image file
Request 4: GET /script.js      → Response: JavaScript file
```

**Each resource = separate HTTP request!**

Browser automatically requests everything the HTML references.

---

# Part 4 - URLs and URIs

---

## Anatomy of a URL

**URL:** Uniform Resource Locator (address of web resource)

```
https://www.example.com:443/path/page.html?id=123#section2
```

**Breaking it down:**

- `https://` - Protocol/Scheme
- `www.example.com` - Domain/Host
- `:443` - Port (optional, 443 is HTTPS default)
- `/path/page.html` - Path
- `?id=123` - Query string
- `#section2` - Fragment/Anchor

---

## URL Components: Protocol

**Protocol/Scheme:** How to access resource

```
http://     - Unencrypted HTTP
https://    - Encrypted HTTP (SSL/TLS)
ftp://      - File Transfer Protocol
file://     - Local file
```

**Always use `https://` for web apps**

---

## URL Components: Domain

**Domain:** Server's address on internet

```
www.example.com
blog.example.com
api.example.com
```

**Parts:**

- `com` - Top-level domain (TLD)
- `example` - Domain name
- `www` - Subdomain (optional)

---

## URL Components: Port

**Port:** Number identifying specific service

```
https://example.com:443/page
```

**Default ports:**

- HTTP: 80 (usually omitted)
- HTTPS: 443 (usually omitted)
- Custom: 8080, 3000, 5000, etc. (development servers)

**In production:** Use default ports (omit from URL)

---

## URL Components: Path

**Path:** Location of resource on server

```
https://example.com/products/shoes/nike.html
                    └─────────────────────┘
                           Path
```

**Examples:**

- `/index.html` - Homepage file
- `/css/style.css` - CSS file
- `/images/logo.png` - Image
- `/about/team` - About team page

---

## URL Components: Query String

**Query String:** Parameters passed to server

```
https://store.com/search?q=laptop&price=500-1000&sort=rating
                         └──────────────────────────────────┘
                                  Query String
```

**Format:**

- Starts with `?`
- Key-value pairs: `key=value`
- Multiple params separated by `&`
- URL encoded (spaces become `%20` or `+`)

---

## URL Components: Fragment

**Fragment (Anchor):** Specific location within page

```
https://example.com/docs#installation
                         └──────────┘
                          Fragment
```

**Characteristics:**

- Starts with `#`
- Not sent to server (browser only)
- Used for scrolling to page sections
- Common in single-page apps

---

## URL Encoding

**Problem:** URLs can't contain spaces or special characters

**Solution:** URL encoding (percent encoding)

```
Space:          %20  or  +
Ampersand (&):  %26
Question mark:  %3F
Hash (#):       %23
```

**Examples:**

```
"Hello World"      →  Hello%20World  or  Hello+World
"Tom & Jerry"      →  Tom%26Jerry
"What is this?"    →  What%20is%20this%3F
```

---

## Absolute vs Relative URLs

**Absolute URL:** Complete address

```html
<a href="https://example.com/about.html">About</a>
<img src="https://example.com/logo.png" />
```

**Relative URL:** Relative to current page

```html
<a href="about.html">About</a>
<a href="/about.html">About</a>
<a href="../about.html">About</a>
<img src="images/logo.png" />
```

**Relative is simpler** for internal links!

---

# Part 5 - HTTP Methods

---

## What are HTTP Methods?

**HTTP Methods:** Just the verb that says what you want to do

```
GET     - "Get me this resource"
POST    - "Here's new data, process it"
PUT     - "Replace this resource"
DELETE  - "Remove this"
```

**That's it.** They're just words in the first line of your request.

---

## GET Method

**GET:** Retrieve a resource

```http
GET /products.html HTTP/1.1
Host: store.example.com
```

**Key point:** No data in body. Just ask for a resource.

---

## GET with Query Parameters

**Passing data in URL:**

```
GET /search?q=shoes&size=10 HTTP/1.1
Host: store.com
```

**Data goes in the URL:** `?key=value&key=value`

Simple as that.

---

## POST Method

**POST:** Send data to the server

```http
POST /contact HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

name=John&email=john@example.com
```

**Key point:** Data goes in the body (hidden, not in URL).

---

## GET vs POST

| Aspect          | GET                   | POST                  |
| --------------- | --------------------- | --------------------- |
| Purpose         | Retrieve data         | Send data             |
| Data in         | URL (visible)         | Body (hidden)         |
| Use case        | Loading pages         | Forms, login          |
| --------------- | --------------------- | --------------------- |
| Purpose         | Retrieve data         | Submit data           |
| Data location   | URL (query string)    | Request body          |
| Visible in URL  | Yes                   | No                    |
| Bookmarkable    | Yes                   | No                    |
| Cached          | Yes                   | No                    |
| Data size limit | Limited (~2000 chars) | Large                 |
| Security        | Less secure (visible) | More secure (in body) |
| Use case        | Search, read articles | Login, create post    |

---

## PUT Method

**PUT:** Update/replace an existing resource

```http
PUT /users/123 HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "John Smith",
  "email": "john@example.com"
}
```

**Idempotent:** Multiple identical PUT requests have same effect as one

---

## DELETE Method

**DELETE:** Remove a resource

```http
DELETE /posts/456 HTTP/1.1
Host: blog.example.com
```

**Example use cases:**

- Delete user account
- Remove blog post
- Clear shopping cart item

---

## Other HTTP Methods

**PATCH:** Partially update a resource

```http
PATCH /users/123 HTTP/1.1

{ "email": "newemail@example.com" }
```

**HEAD:** Like GET, but only returns headers (no body)

**OPTIONS:** Ask server what methods are allowed

**CONNECT, TRACE:** Specialized uses

---

# Part 6 - HTTP Status Codes

---

## What are Status Codes?

**Status Code:** 3-digit number indicating request outcome

**Format:** `Status-Code Reason-Phrase`

```http
200 OK
404 Not Found
500 Internal Server Error
```

**5 categories:** Based on first digit

---

## Status Code Categories

**1xx - Informational:** Request received, processing continues

**2xx - Success:** Request successfully received and processed

**3xx - Redirection:** Further action needed to complete request

**4xx - Client Error:** Request has error (bad syntax, not found)

**5xx - Server Error:** Server failed to fulfill valid request

---

## 2xx Success Codes

**200 OK:** Request succeeded

```http
HTTP/1.1 200 OK
Content-Type: text/html

<html>...</html>
```

**201 Created:** Resource successfully created (POST)

**204 No Content:** Success, but no content to return

---

## 3xx Redirection Codes

**301 Moved Permanently:** Resource has new permanent URL

```http
HTTP/1.1 301 Moved Permanently
Location: https://example.com/new-page
```

**302 Found:** Temporary redirect

**304 Not Modified:** Cached version is still valid

Browser uses cached copy instead of downloading again.

---

## 4xx Client Error Codes

**400 Bad Request:** Malformed request

**401 Unauthorized:** Authentication required

**403 Forbidden:** Server understood, but refuses (no permission)

**404 Not Found:** Resource doesn't exist

```http
HTTP/1.1 404 Not Found
Content-Type: text/html

<h1>Page Not Found</h1>
```

---

## The Famous 404

**404 Not Found:** Most well-known status code

**Why you see it:**

- Typo in URL
- Page was deleted
- Link is broken
- File moved

**Good practice:** Create custom 404 page with:

- Friendly message
- Link back to homepage
- Search box

---

## 5xx Server Error Codes

**500 Internal Server Error:** Generic server failure

```http
HTTP/1.1 500 Internal Server Error
Content-Type: text/html

<h1>Something went wrong</h1>
```

**502 Bad Gateway:** Server acting as gateway got invalid response

**503 Service Unavailable:** Server temporarily overloaded or down

**504 Gateway Timeout:** Gateway didn't get response in time

---

## Common Status Codes Summary

| Code | Meaning               | When You See It             |
| ---- | --------------------- | --------------------------- |
| 200  | OK                    | Page loads successfully     |
| 301  | Moved Permanently     | Redirected to new URL       |
| 304  | Not Modified          | Using cached version        |
| 400  | Bad Request           | Form data invalid           |
| 401  | Unauthorized          | Need to log in              |
| 403  | Forbidden             | Don't have permission       |
| 404  | Not Found             | Page doesn't exist          |
| 500  | Internal Server Error | Server broken               |
| 503  | Service Unavailable   | Server down for maintenance |

---

# Part 7 - HTTP Headers

---

## What are Headers?

**Headers:** Metadata passed with requests and responses

**Format:** `Header-Name: value`

```http
Content-Type: text/html
Content-Length: 1234
Cache-Control: no-cache
```

**Two types:**

- **Request headers:** Client → Server
- **Response headers:** Server → Client

---

## Common Request Headers

**Host:** Domain name of server

```http
Host: www.example.com
```

**User-Agent:** Browser and OS info

```http
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
```

**Accept:** Content types client can handle

```http
Accept: text/html, application/json
```

---

## More Request Headers

**Accept-Language:** Preferred languages

```http
Accept-Language: en-US, en;q=0.9, es;q=0.8
```

**Cookie:** Stored cookies sent to server

```http
Cookie: session_id=abc123; user_pref=dark_mode
```

**Referer:** Previous page URL

```http
Referer: https://google.com/search?q=example
```

---

## Common Response Headers

**Content-Type:** Type of content in body

```http
Content-Type: text/html; charset=UTF-8
Content-Type: application/json
Content-Type: image/png
```

**Content-Length:** Size of body in bytes

```http
Content-Length: 3456
```

---

## More Response Headers

**Cache-Control:** How to cache response

```http
Cache-Control: max-age=3600, public
Cache-Control: no-cache
```

**Set-Cookie:** Server sending cookie to browser

```http
Set-Cookie: session_id=xyz789; Path=/; HttpOnly
```

**Location:** Redirect URL (with 3xx codes)

```http
Location: https://example.com/new-page
```

---

## Server & Security Headers

**Server:** Web server software

```http
Server: Apache/2.4.41 (Ubuntu)
```

**X-Content-Type-Options:** Prevent MIME sniffing

```http
X-Content-Type-Options: nosniff
```

**Strict-Transport-Security:** Force HTTPS

```http
Strict-Transport-Security: max-age=31536000
```

---

# Part 8 - Common Scenarios

---

## Scenario 1: Loading a Simple Page

**You type:** `https://example.com/index.html`

**What happens:**

```
1. Browser: GET /index.html
2. Server:  200 OK
            Content-Type: text/html
            <html>...</html>

3. Browser finds <link rel="stylesheet" href="style.css">
4. Browser: GET /style.css
5. Server:  200 OK
            Content-Type: text/css
            body { color: blue; }
```

---

## Scenario 2: Form Submission

**User fills out contact form and clicks Submit**

```
1. Browser: POST /contact
            Content-Type: application/x-www-form-urlencoded

            name=John&email=john@example.com

2. Server processes form

3. Server: 200 OK  or  302 Found (redirect to thank-you page)
           Location: /thank-you.html

4. Browser: GET /thank-you.html

5. Server: 200 OK
           <html>Thank you!</html>
```

---

## Scenario 3: 404 Error

**User clicks broken link**

```
1. Browser: GET /old-page.html

2. Server looks for file... not found!

3. Server: 404 Not Found
           Content-Type: text/html

           <html>
             <h1>Page Not Found</h1>
           </html>

4. Browser displays 404 page
```

---

## Scenario 4: Redirect

**User goes to old URL**

```
1. Browser: GET /old-url

2. Server: 301 Moved Permanently
           Location: https://example.com/new-url

3. Browser: GET /new-url

4. Server: 200 OK
           <html>New page content</html>

5. Browser displays new page
   Updates address bar to new URL
```

---

## Scenario 5: Cached Content

**User revisits page**

```
First visit:
1. Browser: GET /page.html
2. Server:  200 OK
            Cache-Control: max-age=3600
            <html>...</html>
3. Browser caches page

Second visit (within 1 hour):
1. Browser checks cache
2. Still fresh! Uses cached version
3. NO request to server
4. Page loads instantly
```

---

# Summary

---

## Key Concepts: Client-Server

**Client-Server Model:**

- Client requests, server responds
- Browser is the client
- Web server hosts files

**HTTP:**

- Protocol for web communication
- HTTPS is encrypted version
- Every web interaction uses HTTP

---

## Key Concepts: Request-Response

**HTTP Request contains:**

- Method (GET, POST, etc.)
- URL path
- Headers
- Optional body

**HTTP Response contains:**

- Status code
- Headers
- Body (HTML, CSS, images, etc.)

---

## Key Concepts: Methods & Status Codes

**HTTP Methods:**

- GET: Retrieve data
- POST: Submit data
- PUT: Update data
- DELETE: Remove data

**Status Codes:**

- 2xx: Success (200 OK)
- 3xx: Redirection (301, 302)
- 4xx: Client error (404 Not Found)
- 5xx: Server error (500)

---

## Key Concepts: URLs

**URL structure:**

```
https://example.com:443/path?query=value#fragment
```

**Components:**

- Protocol (https://)
- Domain (example.com)
- Port (443, optional)
- Path (/path)
- Query string (?query=value)
- Fragment (#fragment)

---

## Why This Matters

**Understanding HTTP helps you:**

- Debug why pages don't load
- Understand form submissions
- Fix broken links
- Optimize page loading
- Build better web apps
- Work with APIs
- Understand web security

**HTTP is the foundation of the web!**

---

## Next Steps

**Practice:**

1. Observe HTTP in action when browsing websites
2. Notice status codes in error pages (404, 500, etc.)
3. Pay attention to URL structures and query parameters
4. Think about GET vs POST when submitting forms

**Learn more:**

- REST APIs (use HTTP methods)
- AJAX (HTTP requests from JavaScript)
- Web security (HTTPS, headers, CORS)
- Performance optimization (caching, compression)
