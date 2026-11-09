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
- Three ways to send data: query string, form body, route parameter
- Route parameter middleware
- Sending JSON responses

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

<!-- Timing: ~32 min for 6.5 (including activities) -->

---

# Three Ways to Send Data

> The client sends data in the **query string**, the request **body**, or the URL **path**

Express puts each one in its own object on `req`, ready for the route to use

| Data | Example request | Read it from |
|------|-----------------|--------------|
| **Query string** | `GET /hello?name=Bob` | `req.query.name` |
| **Form POST body** | `POST /hello` (body `name=Tamika`) | `req.body.name` |
| **Route parameter** | `GET /users/jblack` | `req.params.username` |

---

# Query String Parameters

> Express **automatically parses** the `name=value` pairs after the `?` into **`req.query`**

The same route can greet anyone: only the URL changes

```js
// GET http://localhost:3000/hello?name=Bob&age=21
app.get("/hello", function(req, res) {
  const html = `<h1>Hello, ${req.query.name}!</h1>
    <p>You are ${req.query.age} years old.</p>`;
  res.send(html);
});
```

**Browser shows:** Hello, Bob! You are 21 years old.

<!--
Details to say aloud:
- Path = /hello; query string = name=Bob&age=21 (pairs separated by &).
- The query string doesn't change the route: /hello still matches.
- Forms with method="get" send their data this way (zyBooks 2.8).
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

> A form with `method="post"` sends its data **URL-encoded** in the **body** of the HTTP request

The data reaches the server without appearing in the URL

```html
<!-- public/hello.html -->
<form method="post" action="/hello">
  <label>Name? <input type="text" name="name"></label>
  <label>Age? <input type="number" name="age"></label>
  <input type="submit" value="Submit">
</form>
```

Body sent on Submit: `name=Tamika&age=24`

<!--
The full HTTP request the browser sends:
POST /hello HTTP/1.1
Content-Type: application/x-www-form-urlencoded

name=Tamika&age=24
Each input's name attribute becomes a key in the body.
-->

---

# Reading Form Data

> `express.urlencoded()` is **middleware** that parses the URL-encoded body and adds the values to **`req.body`**

Enable it with `app.use()` before the route that reads `req.body`

```js
app.use(express.static("public"));               // serves hello.html
app.use(express.urlencoded({extended: false}));  // body → req.body

app.post("/hello", function(req, res) {
  const html = `<h1>Hello, ${req.body.name}!</h1>
    <p>You are ${req.body.age} years old.</p>`;
  res.send(html);
});
```

<!--
Details to say aloud:
- express.urlencoded() only parses bodies with Content-Type: application/x-www-form-urlencoded.
- The full flow: the browser requests hello.html (express.static serves it) → the user types Tamika / 24 and presses Submit → the browser sends POST /hello with name=Tamika&age=24 in the body → the middleware attaches the data to req.body → the /hello POST route sends "Hello, Tamika!".
Live: open http://localhost:3000/hello.html, submit Tamika / 24. Then comment out the express.urlencoded() line, restart, and submit again (sets up the next activity).
-->

---

<!-- _class: activity -->

> Activity: What happens if... (each change on its own)

<div class="two-column-slide">

<div class="column-left">

```html
<form method="post" action="/hello">
  <input type="text" name="name">
  <input type="submit" value="Submit">
</form>
```

```js
app.use(express.static("public"));
app.use(express.urlencoded({extended: false}));
app.post("/hello", function(req, res) {
  res.send("Hello, " + req.body.name + "!");
});
```

</div>

<div class="column-right">

1. Submit is clicked with no name?
2. `express.urlencoded()` is removed?
3. The form uses `method="get"`?
4. The body is sent as `application/json`?
5. The `express.static()` line is removed?

</div>

</div>

<!--
Answers:
1. The page says "Hello, !" (the name is empty).
2. Nothing parses the body, so req.body.name can't be read: the server responds with an error instead of the greeting.
3. The data goes in the query string (GET /hello?name=Tamika). There is no GET /hello route, so the server returns a 404 status code.
4. express.urlencoded() only parses bodies with Content-Type: application/x-www-form-urlencoded, so req.body is not filled in and the name can't be read.
5. hello.html (the form page in public) is no longer served: http://localhost:3000/hello.html returns a 404, so the user never sees the form.
Follow-up (ask aloud): is express.static() middleware? Yes: it is enabled with app.use(), like express.urlencoded().
-->

---

# Route Parameters

> A **route parameter** is a value in the URL path, named with a **colon** (`:username`); Express attaches it to **`req.params`**

One route makes a dynamic webpage for every username

```js
// GET http://localhost:3000/users/jblack
app.get("/users/:username", function(req, res) {
  const username = req.params.username;   // jblack
  res.send("<h1>Profile for " + username + "</h1>");
});
```

**Browser shows:** Profile for jblack

<!--
Details to say aloud:
- A route parameter is near or at the end of the URL path.
- The name after the colon is the property name: :username → req.params.username.
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

> `app.param()` defines middleware that runs **before** the route's callback; its **fourth parameter** is the parameter's value

It prepares data (`req.user`) for the route, then **must call `next()`**

```js
app.param("username", function(req, res, next, username) {
  if (username === "jblack") { req.user = { name: "Jack Black" }; }
  else { req.user = { name: "Unknown" }; }
  next();   // continue processing the request
});

app.get("/users/:username", function(req, res) {
  res.send("<h1>Profile for " + req.user.name + "</h1>");
});
```

<!--
Flow to draw on the board:
GET /users/jblack → app.param("username", ...) sets req.user, calls next() → app.get("/users/:username", ...) uses req.user → Profile for Jack Black
- zyBooks Figure 6.5.1 is the same example (it also stores username in req.user).
- A real application would replace the if-else with a database query (next class).
Live: request /users/jblack (Jack Black) and /users/sara (Unknown). Add a console.log in app.param to show it runs first.
-->

---

# Sending JSON Responses

> `res.json()` encodes a JavaScript object as **JSON**; `res.status(404)` sets the **status code** before it

A **web API** sends data (JSON) instead of an HTML page

```js
app.get("/users/:username", function(req, res) {
  if (req.user.name !== "Unknown") {
    res.json(req.user);                               // {"name":"Jack Black"}
  }
  else {
    res.status(404).json({ error: "Unknown user" });  // 404 = Not Found
  }
});
```

<!--
Details to say aloud:
- res.json() sends the response with Content-Type: application/json.
- Without res.status(), a successful response has the 200 status code.
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
  req.course = { code: courseId };
});
app.get("/courses/:code", function(req, res) { res.json(req.course); });
// GET /search?term=node
app.get("/search", function(req, res) { res.send(req.params.term); });
// A form posts major=SWE (no other app.use() calls)
app.post("/major", function(req, res) { res.send(req.body.major); });
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
- **Form POST body** → `express.urlencoded()` parses it into `req.body`
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
