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
# Back-End Development: Node.js & Express II

---

# In today's lecture:
- Query string parameters
- Posting form data
- Route parameters
- Route parameter middleware

### Reference: 
- Zybook: 6.5
---

<!-- _class: activity -->

> Activity: Warm-up from last lecture (2 min)

```js
const logRequest = function(req, res, next) {
  console.log(`Request: ${req.method} for ${req.path}`);
  next();
};
app.use(logRequest);
app.use(express.static("public"));
app.post("/goodbye", function(req, res) {
  res.send("<h1>Goodbye, Express!</h1>");
});
```

1. Which route matches a GET request to `/goodbye`?
2. What do the parameters `req`, `res`, and `next` represent?
3. If `next()` is removed, what is logged for `GET /goodbye`?
4. To be served, must `hello.html` be in `public` or in `node_modules`?

<!--
Answers:
1. Neither: the only /goodbye route is a POST route, so the server returns a 404 status code.
2. req = the HTTP request object, res = the HTTP response object, next = the callback that lets the next middleware or route run.
3. "Request: GET for /goodbye" is still logged, but nothing after logRequest runs.
4. In the public directory.
Tip: today every route reads data from req.
-->

---

# 6.5 Express Request Data

<!-- Timing: ~35 min for 6.5 (including activities) -->

---

# How do we get data from the client?

| Data | Example request | Read it from |
|------|-----------------|----------------|
| **Query string** | `GET /hello?name=Bob&age=21` | `req.query` |
| **Posted form data** | `POST /hello` with body `name=Tamika&age=24` | `req.body` |
| **Route parameter** | `GET /users/jblack` | `req.params` |

&nbsp;

Each one is an object: `req.query.name`, `req.body.name`, `req.params.username`

---

# What are Query String Parameters?

> A **query string** = `name=value` pairs after the `?` in a URL, separated by `&`

```
http://localhost:3000/hello?name=Bob&age=21
```

- Path → `/hello`
- Query string → `name=Bob&age=21`
- Express **automatically parses** it into the **`req.query`** object
- Forms with `method="get"` send their data this way

---

# Reading Query Parameters in Express

```js
// GET http://localhost:3000/hello?name=Bob&age=21
app.get("/hello", function(req, res) {
  const html = `<h1>Hello, ${req.query.name}!</h1>
    <p>You are ${req.query.age} years old.</p>`;
  res.send(html);
});
```

**Browser shows:** Hello, Bob! You are 21 years old.

- The query string doesn't change the route: `/hello` still matches

<!--
Live: run the /hello route, then change the URL: different name, remove age, add an extra parameter.
-->

---

<!-- _class: activity -->

> Activity: Predict what the page shows

```js
app.get("/hello", function(req, res) {
  const html = `<h1>Hello, ${req.query.name}!</h1>
    <p>You are ${req.query.age} years old.</p>`;
  res.send(html);
});
```

1. `/hello?name=Sara&age=20`
2. `/hello?age=20`
3. `/hello?name=Doctor+Who&age=900` (in a URL, `+` encodes a space)
4. `/hello?city=Dallas`: is the city in `res.query.city` or `req.query.city`?

<!--
Answers:
1. Hello, Sara! You are 20 years old.
2. Hello, undefined! You are 20 years old. (name is not in the query string)
3. Hello, Doctor Who! A space in form data is URL-encoded as + (zyBooks 2.8), and Express decodes it back to a space, so the page does not say "Doctor+Who".
4. req.query.city (res is the response object). The page itself shows "Hello, undefined! You are undefined years old."
-->

---

# Posting Form Data

> A form that **posts** to an Express route sends its data **URL-encoded** in the **body**

**public/hello.html** and the **HTTP request** it sends on Submit:
```html
<form method="post" action="/hello">
  <p><label>Name? <input type="text" name="name"></label></p>
  <p><label>Age? <input type="number" name="age"></label></p>
  <input type="submit" value="Submit">
</form>
```
```
POST /hello HTTP/1.1
Content-Type: application/x-www-form-urlencoded

name=Tamika&age=24
```

---

# Receiving URL-Encoded Data

```js
const express = require("express");
const app = express();

app.use(express.static("public"));               // serves hello.html
app.use(express.urlencoded({extended: false}));  // parses the form data

app.post("/hello", function(req, res) {
  const html = `<h1>Hello, ${req.body.name}!</h1>
    <p>You are ${req.body.age} years old.</p>`;
  res.send(html);
});

app.listen(3000);
```

- `express.urlencoded()` → **middleware** that adds the parsed values to **`req.body`**
- Only parses bodies with `Content-Type: application/x-www-form-urlencoded`

<!--
Live: open http://localhost:3000/hello.html, submit Tamika / 24. Then comment out the express.urlencoded() line, restart, and submit again (sets up the next activity).
-->

---

<!-- _class: activity -->

> Activity: Put the steps in order

A. The middleware parses the body and attaches the data to `req.body`

B. The browser requests `hello.html`, and `express.static()` serves it

C. The `/hello` POST route sends back "Hello, Tamika!"

D. The user types Tamika and 24 and presses Submit

E. The browser sends `POST /hello` with `name=Tamika&age=24` in the body

<!--
Answer:
B → D → E → A → C
Follow-up: which steps happen in the browser (B's request, D, E) and which on the server (B's response, A, C)?
-->

---

<!-- _class: activity -->

> Activity: What happens if... (each change on its own)

<div class="two-column-slide">

<div class="column-left">

```html
<!-- public/hello.html -->
<form method="post" action="/hello">
  <input type="text" name="name">
  <input type="number" name="age">
  <input type="submit" value="Submit">
</form>
```

```js
app.use(express.static("public"));
app.use(express.urlencoded({extended: false}));

app.post("/hello", function(req, res) {
  res.send(`<h1>Hello, ${req.body.name}!</h1>`);
});
```

</div>

<div class="column-right">

1. Submit is clicked with no name?
2. `express.urlencoded()` is removed?
3. The form uses `method="get"`?
4. The request's Content-Type is `application/json` instead of `application/x-www-form-urlencoded`?
5. `app.use(express.static("public"))` is removed?

</div>

</div>

<!--
Answers:
1. The page says "Hello, !" (the name is empty).
2. Nothing parses the body, so req.body.name can't be read: the server responds with an error instead of the greeting.
3. The data goes in the query string (GET /hello?name=Tamika&age=24). There is no GET /hello route, so the server returns a 404 status code.
4. express.urlencoded() only parses bodies with Content-Type: application/x-www-form-urlencoded, so req.body is not filled in and the name can't be read.
5. hello.html is no longer served: http://localhost:3000/hello.html returns a 404, so the user never sees the form.
Follow-up (ask aloud): is express.static() middleware? Yes: it is enabled with app.use(), like express.urlencoded().
-->

---

# What are Route Parameters?

> A **route parameter** = a value near or at the end of the URL path; its name is defined with a **colon** (`:`)

```js
// GET http://localhost:3000/users/jblack
app.get("/users/:username", function(req, res) {
  const username = req.params.username;   // jblack
  res.send("<h1>Profile for " + username + "</h1>");
});
```

- Route parameters are attached to the **`req.params`** object
- One route → a **dynamic webpage** for every username

**Browser shows:** Profile for jblack

<!--
Live: request /users/jblack, then /users/abc, then /users/ (404).
-->

---

<!-- _class: activity -->

> Activity: 
Which req property (`req.query`, `req.params`, or `req.body`)? What value?

1. Route `/users/:username`, request `GET /users/abc`
2. Route `/search`, request `GET /search?term=node`
3. Route `app.post("/major", ...)`, a form posts `major=SWE`
4. Route `/city/:cityName`, `GET /city/Denver`: is it `req.params.city`?
5. Route `/users/:username`, request `GET /users/`: does the page say "Profile for "?

<!--
Answers:
1. req.params.username is abc, so the page says "Profile for abc".
2. req.query.term is node.
3. req.body.major is SWE (needs app.use(express.urlencoded(...))).
4. No: it is req.params.cityName (the name after the colon).
5. No: /users/ has no value for :username, so the route doesn't match and the server returns a 404 status code.
-->

---

# Route Parameter Middleware

> `app.param()` defines **parameter middleware** that executes **before** a route's callback function

- The middleware function has a **fourth parameter** → the route parameter's value
- It can add data to `req` for the route to use, then calls `next()`

```
GET /users/jblack
  → app.param("username", ...)         sets req.user, calls next()
  → app.get("/users/:username", ...)   uses req.user
  → Profile for Jack Black
```

A real application would look up the user in a **database** (next class)

---

# Param Middleware Example

```js
// Parameter middleware executes before the route
app.param("username", function(req, res, next, username) {
  // Check if username is recognized
  if (username === "jblack") {
    req.user = { name: "Jack Black", username: username };
  }
  else {
    req.user = { name: "Unknown", username: username };
  }
  // Continue processing the request
  next();
});

app.get("/users/:username", function(req, res) {
  // req.user contains the user info set in the parameter middleware
  res.send("<h1>Profile for " + req.user.name + "</h1>");
});
```

<!--
Live: request /users/jblack (Jack Black) and /users/sara (Unknown). Add a console.log in app.param to show it runs first.
-->

---

# Sending JSON Responses

```js
app.get("/users/:username", function(req, res) {
  if (req.user.name !== "Unknown") {
    res.json(req.user);
  }
  else {
    res.status(404).json({ error: "Unknown user" });
  }
});
```

- `res.json()` → encodes a JavaScript object as **JSON** (`application/json`)
- `res.status(404)` → sets the **status code** (404 = Not Found) before sending
- `/users/jblack` → `{ "name": "Jack Black", "username": "jblack" }`
- `/users/sara` → 404 and `{ "error": "Unknown user" }`

<!--
Live: replace res.send() with this route; show the 404 status in DevTools (Network tab).
-->

---

<!-- _class: activity -->

> Activity: Predict the response

```js
app.param("zip", function(req, res, next, zip) {
  if (zip === "80015") {
    req.forecast = {high: 95, low: 72};
  }
  next();
});
app.get("/weather/:zip", function(req, res) {
  if (req.forecast) { res.json(req.forecast); }
  else { res.status(404).json({ error: "Unknown ZIP code" }); }
});
```

1. `/weather/80015`
2. `/weather/12345`: what status code?
3. `next()` is removed: `/weather/80015`?
4. `app.param("zipcode", ...)` instead of `"zip"`: `/weather/80015`?

<!--
Answers:
1. The JSON { "high": 95, "low": 72 } (status 200).
2. The JSON { "error": "Unknown ZIP code" } with a 404 status code.
3. The server does not return a response (the route callback never runs).
4. { "error": "Unknown ZIP code" } with 404: no route has a :zipcode parameter, so the middleware never runs and req.forecast is never set.
-->

---

<!-- _class: activity -->

> Activity: Exit ticket: find the 4 bugs

```js
app.param("courseId", function(req, res, next, courseId) {
  req.course = { code: courseId, title: "Web Engineering" };
});
app.get("/courses/:code", function(req, res) {
  res.json(req.course);
});
// GET /search?term=node
app.get("/search", function(req, res) {
  res.send("Searching for " + req.params.term);
});
// A form posts major=SWE (no other app.use() calls)
app.post("/major", function(req, res) {
  res.send("Major: " + req.body.major);
});
```

<!--
Answers:
1. app.param() never calls next() → add next(); at the end of the middleware.
2. The parameter names don't match: app.param("courseId") but the route uses :code → use the same name in both.
3. term is in the query string → req.query.term, not req.params.term.
4. No express.urlencoded() middleware → add app.use(express.urlencoded({extended: false})); before the routes so req.body is filled in.
Tip: bugs 1, 2, and 3 are the most common mistakes in the lab.
-->

---

# Key Takeaways

- **Query string** (`?name=Bob&age=21`) → `req.query`
- **Posted form data** → `express.urlencoded()` parses it into `req.body`
- **Route parameter** (`/users/:username`) → `req.params`
- `app.param()` runs **before** the route's callback and must call `next()`
- `res.json()` sends JSON; `res.status(404).json()` also sets the status code

---

<!-- _class: demo -->

>30m
# Demo
6.4 Request Data in Express

- Query string parameters
- Route parameters
- Param middleware
- JSON responses with status codes

<!--
Setup: cd 6-4-express-request-data; npm install; node server.js (prints "API running at http://localhost:3000").
Tasks (TODOs in server.js): 1 create the app and listen on 3000; 2 GET /echo reads name and age from req.query (400 JSON if one is missing); 3 GET /profile/:first/:last returns fullName; 4 app.param("userId") converts to a number, 400 JSON if not positive, else req.userIdNum and next(); 5 GET /users/:userId returns req.userIdNum.
Test: the URLs listed at the end of the server.js comment block (browser for GET routes, curl -i to see the status codes).
Not in zyBooks ch6 (the lab's TODO hints and README explain them):
- import express from "express" and "type": "module" in package.json: ch6 examples use require(); 6.3 covers import/export but not importing an npm package.
- Arrow functions (req, res) => { ... }: zyBooks 4.6; ch6 uses function(req, res).
- Object destructuring const { name, age } = req.query: zyBooks only covers array destructuring (5.9 useState).
- Status code 400 with res.status(400): zyBooks 7.4 (Music API); ch6 only shows 404, and Table 1.3.2 doesn't list 400.
- return res.status(...).json(...) to stop the callback early: zyBooks 8.2.
- Converting to a number and checking "positive": Number() / Number.isFinite() are not in zyBooks (parseInt() and isNaN() are in ch4); the lab README shows Number.isFinite().
- Two route parameters in one path (/profile/:first/:last): ch6 only shows one; the TODO hint gives the route.
- curl for testing: not in zyBooks.
- express.json() (JSON request bodies): zyBooks 7.3; mentioned in the README but not needed for the TODOs.
-->

---

# Next Class

- Mongoose (7.1)
- MongoDB (7.2)
