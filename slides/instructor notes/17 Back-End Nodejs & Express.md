---
marp: true
paginate: true
style: |
    :root {
      --background:rgb(25, 27, 32);
      --background-light:rgb(93, 102, 121);
      --foreground: #ffffff;
      --light-background: #ffffff;
      --accent: #ffcc00;
      --sedondary:rgb(76, 22, 114);
    }
    section { background-color: var(--background); color: var(--foreground); }
    h1,h2,h3,h4,h5 {color:var(--foreground);}
    section.boxes ul { display: flex; list-style: none; padding: 0; width: 100%; }
    section.boxes li { background-color:var(--foreground); color:var(--background); padding: 20px; margin: 10px; border-radius: 10px; flex: 1; text-align: center; font-size: 0.85em; overflow: auto; }
    blockquote { color: white; }
    strong { color: var(--accent); }
    header, footer {width:100%; margin:0 auto; color:var(--background-light)}
    section.activity { background: var(--accent); color:var(--background)}
    section.activity h1,section.activity h2, section.activity h3, section.activity h4, section.activity h5 { color: var(--background) }
    section.activity footer { display: none; }
    section.activity blockquote {display:inline-block; border: 4px solid black; color: white; border-radius: 10px; 
    background-color:var(--background)}
    section.activity a {
        color: var(--background);
        text-decoration: underline;
        font-weight: bold;
    }
    a { color:var(--accent) }
    section.demo { background: var(--sedondary); color:var(--foreground)}
    section.demo h1,section.demo h2, section.demo h3, section.demo h4, section.demo h5 { color: var(--foreground) }
    section.demo footer, section.footer-none footer { display: none; }
    section.demo blockquote {display:inline-block; color: var(--sedondary); border-radius: 10px; background-color: var(--foreground)}
    section.light { background-color: var(--light-background); color: var(--background); }
    section.light h1, section.light h2, section.light h3, section.light h4, section.light h5 { color: var(--background); }
    section.grraph pre {
        background-color: #ffffff;
        color: var(--background);
        padding: 10px;
        border-radius: 5px;
        overflow-x: auto;
    }
    table {
        background: transparent !important;
        background-color: transparent !important;
        border-collapse: collapse;
        margin: 0 auto;
        text-align: center;
    }
    table, table * {
        background: transparent !important;
        background-color: transparent !important;
    }
    table th, table td {
        background: transparent !important;
        background-color: transparent !important;
        border: 1px solid var(--foreground);
        padding: 8px;
    }
    table th {
        background: transparent !important;
        background-color: transparent !important;
        font-weight: bold;
    }
    /* Override Marp default table styles */
    section table {
        background: transparent !important;
        background-color: transparent !important;
        margin: 0 auto;
        text-align: center;
    }
    section table th,
    section table td {
        background: transparent !important;
        background-color: transparent !important;
    }
    section.center {text-align:center}
    section.big-code pre {font-size:2rem}
    pre {font-size:0.8rem}
    .two-column-slide {
      display: flex;
      height: 100%; /* Ensure the container takes full slide height */
    }

    .column-left {
      flex: 1; /* Distribute space equally */
      padding: 20px;
    }

    .column-right {
      flex: 1;
      padding: 20px;
    }
footer: 'SWE 363 | KFUPM'
---



Web Engineering & Development (SWE 363) 
# Back-End Development: Node.js & Express

---

# In today's lecture:
- Serving static files
- Routes: GET and POST
- Middleware and `next()`
- Third-party middleware (morgan)
- The Express application generator

### Reference: 
- Zybook: 6.4
---

<!-- _class: activity -->

> Activity: Warm-up, remember Lecture 15? (2 min)

```js
const express = require("express");
const app = ______();

app.___("/hello", function(req, res) {
  res.send("<h1>Hello, Express!</h1>");
});

app.______(3000, function() {
  console.log("Listening on port 3000...");
});
```

1. Fill in the three blanks. Word bank: `listen`, `get`, `express`, `send`
2. True or False: `express()` starts the Express server.
3. Which method sends an object as JSON: `res.send()` or `res.json()`?
4. What does the browser get for `http://localhost:3000/bye`?

<!--
Answers:
1. express, get, listen
2. False: express() creates the app object; app.listen() starts the server.
3. res.json()
4. A 404 error: no route matches /bye.
Tip: today we add static files, POST routes, and middleware to this same server.
-->

---
# 6.4 Express

<!-- Timing: ~36 min for 6.4 (including activities): ~20 min content + ~16 min activities -->

---

# The public Directory

<div class="two-column-slide">

<div class="column-left">

```
myproject
├── node_modules
│   └── express
├── public
│   └── hello.html
├── package.json
└── server.js
```

</div>

<div class="column-right">

- `node_modules/express` → the installed **express** package
- **public** → stores **static files** (HTML, images, etc.) served by the Express server
- **server.js** → the application code, run with `node server.js`

</div>

</div>

---

# Serving Static Files

```js
// server.js
const express = require("express");
const app = express();

// Serve static files from the public dir
app.use(express.static("public"));

// Start the web server
app.listen(3000, function() {
  console.log("Listening on port 3000...");
});
```

- `express.static()` → names the directory with the static files
- `app.use()` → applies it to the Express app
- `http://localhost:3000/hello.html` → the server responds with `hello.html`

<!--
Live: create public/hello.html, run node server.js, open /hello.html, then try /bye.html (404).
-->

---

<!-- _class: activity -->

> Activity: Predict what the browser shows

```
myproject
├── public
│   └── hello.html
└── server.js       // app.use(express.static("public"));
```

1. `http://localhost:3000/hello.html`
2. `http://localhost:3000/bye.html`
3. `http://localhost:3000/public/hello.html`
4. To serve `images/dog.jpg`, the `images` directory must be in `public` or `node_modules`?

<!--
Answers:
1. The hello.html page ("Hello, Express!").
2. A 404 status code: there is no bye.html in public.
3. A 404 status code: URLs start inside public, so "public" is not part of the URL.
4. public (then the URL is http://localhost:3000/images/dog.jpg).
-->

---

# Routes

> An Express **route** = a URL **path** + an HTTP request **method**, with an assigned **callback function**

```js
app.method(path, callback)
```

- `app` → the Express instance
- `method` → the HTTP request method (`get`, `post`, etc.)
- `path` → the URL path
- `callback` → the function executed when the route **matches**
  - Parameters `req` and `res` → the HTTP request and response

---

# GET vs. POST Routes

```js
// Called for GET request to http://localhost:3000/hello
app.get("/hello", function(req, res) {
  res.send("<h1>Hello, Express!</h1>");
});

// Called for POST request to http://localhost:3000/goodbye
app.post("/goodbye", function(req, res) {
  res.send("<h1>Goodbye, Express!</h1>");
});
```

- **GET** → requests a resource (the most common browser request)
- **POST** → often sends information from a web form: `<form method="POST">`
- A route matches only when **both** the method and the path match

<!--
Live: add the POST /goodbye route, then type /goodbye in the browser's address bar. The browser sends a GET request, so no route matches (404).
-->

---

<!-- _class: activity -->

> Activity: Which route matches? (server on port 3000)

```js
app.get("/hello", callback);
app.post("/goodbye", callback);
app.get("/droids", callback);
```

1. A POST request to `/hello`: `/hello`, `/goodbye`, or neither?
2. Which URL matches `/droids`?
   `http://localhost/droids`, `http://localhost:3000/droidssss`, or `http://localhost:3000/Droids`
3. Which route matches a POST request to `http://localhost:3000/apply`?
   `app.get("/apply", cb)`, `app.post("/apply", cb)`, or `app.post("http://localhost:3000/apply", cb)`

<!--
Answers:
1. Neither route: /hello only matches GET, and /goodbye has a different path.
2. http://localhost:3000/Droids (the first URL is missing the port, and "droidssss" is a different path; Express paths are not case-sensitive by default).
3. app.post("/apply", cb): the path is only the URL path, not the full URL.
-->

---

# What is Middleware?

> A **middleware function** (or just **middleware**) examines or modifies the **request** and/or **response** objects

**Why use middleware?**
- Runs **before** the route, for **every** request
- Write common code **once** with `app.use()`, instead of in every route
- Ex: `express.static()` serves files, **morgan** logs requests

**Three parameters:** `req` (request), `res` (response), `next` (call when done)

```
Request → middleware → next() → route → Response
```

<!--
Ask: without middleware, how would you log every request? (Copy console.log into every route: repetitive and easy to forget.)
-->

---

# A Middleware That Logs Requests

```js
const logRequest = function(req, res, next) {
  console.log(`Request: ${req.method} for ${req.path}`);
  next();
};

app.use(logRequest);
app.get("/hello", function(req, res) {
  res.send("<h1>Hello, Express!</h1>");
});
// app.listen(3000, ...) as before
```

**Console** after the browser requests `http://localhost:3000/hello`:
```
Listening on port 3000...
Request: GET for /hello
```

<!--
Live: add logRequest, request /hello and then /, and watch the server console.
-->

---

<!-- _class: activity -->

> Activity: What happens if (each change on its own)

```js
const logRequest = function(req, res, next) {
  console.log(`Request: ${req.method} for ${req.path}`);
  next();
};
app.use(logRequest);
app.get("/hello", function(req, res) {
  res.send("<h1>Hello, Express!</h1>");
});
```

1. The browser requests `/`, which has no route: what is logged?
2. `app.use()` is removed: what does GET `/hello` log?
3. `next()` is removed: what does GET `/hello` log? What does the browser show?
4. `app.use()` is moved after `app.get()`: what does GET `/hello` log?

<!--
Answers:
1. Request: GET for / (the middleware runs for every request; then no route matches, so 404).
2. Nothing is logged: the middleware is never enabled.
3. Request: GET for /hello is logged, but the /hello route never runs, so the browser never gets "Hello, Express!".
4. Nothing is logged: the /hello route responds first and does not call next(), so logRequest() never runs.
Tip: try each change live and restart the server between changes.
-->

---

# Middleware: Order and `next()`

- `next()` → allows **other middleware** and the **route** to execute
- No `next()` → the request stops in the middleware
- `app.use()` **before** the routes → the middleware runs first

```
app.use(logRequest);     →  logs "Request: GET for /hello", then /hello responds
app.get("/hello", ...);

app.get("/hello", ...);  →  /hello responds; logRequest() never runs
app.use(logRequest);
```

- `express.static("public")` is also enabled with `app.use()`

---

# Third-Party Middleware: morgan

Many useful middleware functions can be **installed with npm**

<div class="two-column-slide">

<div class="column-left">

```bash
npm install morgan
```

```js
const express = require("express");
const morgan = require("morgan");
const app = express();

// Show HTTP requests in the console
app.use(morgan("dev"));

app.listen(3000);
```

</div>

<div class="column-right">

**Example console logging of requests:**
```
GET /hello.html 200 8.645 ms - 132
POST /hello 200 4.280 ms - 25
GET /blah 404 1.297 ms - -
```

- **morgan** logs HTTP requests
- `"dev"` → the output format

</div>

</div>

<!--
Live: npm install morgan, add app.use(morgan("dev")), refresh the browser, and request a missing page to show a 404 line.
-->

---

<!-- _class: activity -->

> Activity: Put the steps in order

A. `app.use(morgan("dev"));` enables morgan

B. `npm install morgan`

C. The browser requests `http://localhost:3000/hello.html`

D. `const morgan = require("morgan");` imports morgan

E. The console shows `GET /hello.html 200 8.645 ms - 132`

F. `node server.js` starts the server

<!--
Answer:
B → D → A → F → C → E
Follow-up: what would E show if hello.html were not in public? (GET /hello.html 404 ...)
-->

---

# Popular Third-Party Middleware

| Middleware | Description |
|------------|-------------|
| **morgan** | Logs HTTP request information |
| **cookie-parser** | Parses the cookie header in an HTTP request |
| **errorhandler** | Aids debugging during development |
| **csurf** | Protects against cross-site request forgery (CSRF) |
| **compression** | Compresses response bodies |
| **express-session** | Manages session data on the server |

---

<!-- _class: activity -->

> Activity: Which middleware?

Choose from: morgan, cookie-parser, errorhandler, csurf, compression, express-session

1. Indicates that an HTTP request returned a 404 status code
2. Protects an Express server from a malicious CSRF attack
3. Tracks the user's temporary session data
4. Makes response bodies smaller
5. Reads the cookie header of a request
6. Aids debugging during development

<!--
Answers:
1. morgan
2. csurf
3. express-session
4. compression
5. cookie-parser
6. errorhandler
-->

---

# Express Application Generator

> **express-generator** automatically creates an Express **application skeleton**

- Saves time writing code that is common to many Express applications
- Generated projects use the **Pug** template engine to create views (webpages)
- The views interact with the **MongoDB** database

---

<!-- _class: activity -->

> Activity: Find the 3 bugs (exit ticket)

Goal: `http://localhost:3000/hello` shows "Hello!" and every request is logged.

```js
const express = require("express");
const app = express();

const logRequest = function(req, res) {
  console.log(`Request: ${req.method} for ${req.path}`);
};

app.use(morgan("dev"));
app.use(logRequest);

app.post("/hello", function(req, res) {
  res.send("<h1>Hello!</h1>");
});

app.listen(3000);
```

<!--
Answers:
1. morgan is never imported → npm install morgan and add const morgan = require("morgan");
2. logRequest() never calls next() → add the next parameter and call next(); otherwise the request stops in the middleware.
3. Typing the URL in the browser sends a GET request, but the route uses app.post() → use app.get("/hello", ...).
Tip: these are the most common mistakes in today's lab (forgetting to install/import morgan, and route method/path mismatches).
-->

---

# Key Takeaways

- `app.use(express.static("public"))` → serves the static files in **public**
- **Route:** `app.method(path, callback)` → method **and** path must match
- **Middleware** `(req, res, next)` is enabled with `app.use()`
- Call `next()` so other middleware and the route can execute
- **Third-party middleware** is installed with npm, e.g., `morgan("dev")`
- **express-generator** creates an Express application skeleton

---

<!-- _class: demo -->

>30m
# Demo
6.3 Express

- Routes that send text and JSON
- Logging requests with morgan
- Connect the React front end

<!--
Setup: cd 6-3-node-express; npm install; npm install morgan (morgan is not in package.json yet); npm run dev (front end). In a 2nd terminal: cd backend && node server.js (back end).
Tasks: TODO 1–7. backend/server.js: create the app and PORT, enable cors, enable morgan("dev"), routes / (plain text) and /api/quote (JSON), app.listen. backend/utils/random.js: getRandomInt(max). backend/quotes.js: getRandomQuote().
Test: http://localhost:3000/ and http://localhost:3000/api/quote in the browser; click Get Quote in the React app; check the morgan lines in the backend terminal.
Not in zyBooks ch6 (the lab's TODO hints in utils/random.js explain them):
- import express from "express" / import morgan from "morgan" with "type": "module" (ES modules from 6.3; the 6.4 examples use require)
- cors (zyBooks 7.4; the CORS concept is in 5.3): needed because React (port 5173) and Express (port 3000) are different origins
- Arrow-function route callbacks in the hints (arrow functions are in zyBooks 4.6; 6.4 uses function(req, res))
- Math.random() / Math.floor() for getRandomInt (zyBooks 4.13)
- fetch / async / await / useState in App.jsx (zyBooks 5.17 and 5.9; already written in the starter)
-->

---

# Next Class

- Express request data (6.5)
- Query strings, form data, and route parameters
