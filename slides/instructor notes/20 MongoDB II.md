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
# RESTful Web APIs

---

# In today's lecture:
- RESTful web APIs with Express
- Connecting the API to MongoDB
- Using the API with Fetch

### Reference: 
- Zybook: 7.3, 7.4 (parts), 7.5

---

<!-- _class: activity -->

> Activity: Think-Pair-Share (2 min)

1. Which Mongoose method would you use to add a student, list all students, find one student by ID, change a GPA, and remove a student? 
Choose from: `find()`, `findById()`, `create()`, `updateOne()`, `deleteOne()`
2. In 5.17, how did a React app get forecast data from a web API?
3. Which Express method sends a JavaScript object as JSON?

<!--
Answers:
1. Add: Student.create() (or new Student(...) + save()). List all: Student.find(). Find by ID: Student.findById(). Change: Student.updateOne(). Remove: Student.deleteOne().
2. It called fetch(url), checked response.ok, then called response.json() to get a JavaScript object.
3. res.json()
Tip: today connects these three pieces: fetch in the browser → Express route → Mongoose → MongoDB.
-->

---

# 7.3 RESTful Web APIs (Node)

<!-- Timing: ~13 min for 7.3 (including activities; warm-up before this header ~2 min) -->

---

# What is a RESTful Web API?

> A **RESTful web API** implements **CRUD** operations on **resources** (data at a URL) using HTTP **verbs**; data is sent as **JSON**

**Why:** one standard interface for browsers, mobile apps, and other clients

```
POST   /api/students       → Create a new student
GET    /api/students       → Retrieve all students
GET    /api/students/42    → Retrieve student 42
PUT    /api/students/42    → Update student 42
DELETE /api/students/42    → Delete student 42
```

<!--
Definitions (zyBooks 7.3): a web API provides a standard interface to application data. A client is a program that sends web API requests. REST (representational state transfer) is an architectural style for distributed hypermedia systems. A resource is a data entity whose representation is accessible via a URL (ex: a "customer" resource at http://paypal.com/customer).
Flow (7.3.1 animation): web browser (JS) → GET /api/students/42 → web API → query → database → results → web API → { student } as JSON → web browser.
-->

---

# Status Codes

> Every API response includes a **status code** that tells the client what happened

**Why:** the front end checks it: `response.ok` is true for a **2xx** code

| Code | Meaning | Example |
|------|---------|---------|
| **200** OK | Success, with data | `GET /api/students` |
| **201** Created | New resource created | `POST /api/students` |
| **204** No Content | Success, **no** body | `PUT`, `DELETE` |
| **404** Not Found | Resource doesn't exist | `GET /api/students/999` |
| **400** | Error (e.g., invalid ID) | any route |

<!--
Table 7.3.1 (Music API) uses the same codes: 200 for GET, 201 for POST, 204 for PUT and DELETE, 404 for a non-existing song. 400 comes from 7.4 (an exception in the route).
-->

---

<!-- _class: activity -->

> Activity: Classify (verb, URL, and status code)

A Movie API has the endpoint `/api/movies`.

Verbs: GET, POST, PUT, DELETE 
Status codes: 200 OK, 201 Created, 204 No Content, 404 Not Found

1. List all movies
2. Add a new movie
3. Change the title of movie 7
4. Remove movie 7
5. Get movie 500, which does not exist
6. Which of these requests usually send JSON to the server?

<!--
Answers:
1. GET /api/movies → 200 OK
2. POST /api/movies → 201 Created
3. PUT /api/movies/7 → 204 No Content
4. DELETE /api/movies/7 → 204 No Content
5. GET /api/movies/500 → 404 Not Found
6. POST and PUT (GET and DELETE don't send JSON in the body).
Tip: zyBooks 7.3.3 asks the same questions about the Music API.
-->

---

# Express Router

> `express.Router` creates modular route callbacks for the API **endpoints** (URLs used to access a resource)

**Why:** all API routes share one prefix, `/api`

```js
const router = express.Router();

// GET request returns JSON-encoded student
router.get("/students", function(req, res) {
  res.json({ name: "Sue Black", gpa: 3.1 });
});

// All requests to API begin with /api
app.use("/api", router);     // → GET /api/students
```

<!--
Full server: const express = require("express"); const app = express(); ... app.listen(8080);
Live: run node server.js and open http://localhost:8080/api/students in the browser; then try /students (404).
-->

---

# Receiving JSON: `express.json()`

> `express.json()` is middleware that converts a JSON request body into a JavaScript object in `req.body`

**Why:** POST and PUT send their data as JSON (`Content-Type: application/json`)

```js
// Middleware that parses HTTP requests with JSON body
app.use(express.json());

router.post("/students", function(req, res) {
  console.log(req.body);   // { name: 'Jack White', gpa: 2.5 }
  res.sendStatus(201);
});
```

<!--
Testing (zyBooks 7.3): a web browser is fine for GET; the VS Code extension REST Client sends POST, PUT, and DELETE from a .http or .rest file. Requests are separated by ###, each has a Send Request link, and a blank line separates the headers from the JSON body:
POST http://localhost:8080/api/students
Content-Type: application/json
(blank line)
{ "name": "Jack White", "gpa": 2.5 }
Live: send the POST with REST Client, then comment out app.use(express.json()) and show that req.body is no longer the student.
-->

---

<!-- _class: activity -->

> Activity: Predict, then what happens if

```js
app.use(express.json());
router.get("/students", function(req, res) {
  res.json([{ name: "Sue" }, { name: "Li" }]);
});
router.post("/students", function(req, res) {
  console.log(req.body);
  res.sendStatus(201);
});
app.use("/api", router);
```

1. What does a GET request to `http://localhost:8080/students` return?
2. A student is POSTed, then `/api/students` is requested. How many students?
3. `Content-Type` is removed from the POST request. What does the server output?
4. `app.use(express.json())` is removed. Can the route still read `req.body`?

<!--
Answers:
1. 404: all API routes begin with /api.
2. Two: the POST route only logs the student and returns 201; the GET route always returns the same array.
3. {} : the body is not parsed as JSON without the Content-Type header.
4. No: express.json() is the middleware that converts the JSON body into a JavaScript object.
Tip: zyBooks 7.3.5 and 7.3.6 ask the same questions about the Music API.
-->

---

# 7.4 RESTful Web APIs: Using a Database

<!-- Timing: ~7 min for 7.4 (parts needed by the demo, including activities) -->

---

# Routes with Mongoose

> API routes use `async` callbacks that `await` a **Mongoose** method (7.1)

**Why:** the resources now live in MongoDB, not in the code

```js
router.get("/students/:id", async function(req, res) {
  try {
    const stu = await Student.findById(req.params.id);
    if (stu === null) {
      res.sendStatus(404);
    } else {
      res.json(stu);
    }
  } catch (ex) { res.status(400).send(ex.message); }
});
```

<!--
Every route uses the same try/catch: an exception (e.g., an ID that is not a valid ObjectId) → res.status(400).send(ex.message).
Project files (zyBooks 7.4): db.js connects to MongoDB, server.js creates the Express server, models/student.js creates the schema and model, routes/students.js creates the API routes.
Live: POST a student with REST Client, copy its _id, then GET /api/students/<id>.
-->

---

# One Mongoose Method per Route

> Each CRUD route calls **one** Mongoose method on the `Student` model

**Why:** every route in the lab follows this pattern

| Route | Mongoose method | Code |
|-------|-----------------|------|
| `GET /students` | `find({})` | 200 |
| `GET /students/:id` | `findById(req.params.id)` | 200 |
| `POST /students` | `create(req.body)` | 201 |
| `PUT /students/:id` | `updateOne({ _id: req.params.id }, req.body)` | 204 |
| `DELETE /students/:id` | `deleteOne({ _id: req.params.id })` | 204 |

<!--
Code (zyBooks 7.4 style), each inside try { ... } catch (ex) { res.status(400).send(ex.message); }:
GET all: const students = await Student.find({}); res.json(students);
POST: const stu = await Student.create(req.body); res.status(201).json(stu);
PUT: const result = await Student.updateOne({ _id: req.params.id }, req.body); if (result.matchedCount === 0) res.sendStatus(404); else res.sendStatus(204);
DELETE: const result = await Student.deleteOne({ _id: req.params.id }); if (result.deletedCount === 0) res.sendStatus(404); else res.sendStatus(204);
-->

---

<!-- _class: activity -->

> Activity: Predict the status code (in every route, an exception → 400)

| Route | Sends |
|-------|-------|
| `GET /api/students/:id` | 404 if `findById()` returns `null`, else JSON |
| `PUT /api/students/:id` | 404 if `matchedCount` is 0, else 204 |
| `DELETE /api/students/:id` | 404 if `deletedCount` is 0, else 204 |
| `POST /api/students` | 201 + JSON |

1. `GET /api/students/abc` (not a valid ObjectId)
2. `PUT /api/students/<valid ID>` with `{ "gpa": 3.5 }`
3. `DELETE /api/students/<valid ID, not in the database>`
4. `POST /api/students` with a valid student

<!--
Answers:
1. 400: the invalid ID throws an exception.
2. 204 (No Content): the student was found and updated.
3. 404: deletedCount is 0.
4. 201 with the JSON-encoded student (including its new _id).
Follow-up (ask aloud): what is in the body of a DELETE request, and of its response? Nothing in both: the ID is in the URL, and 204 has no message body.
Tip: zyBooks 7.4.2–7.4.4 ask the same questions about the Music API.
-->

---

# 7.5 Using RESTful Web APIs with Fetch

<!-- Timing: ~10 min for 7.5 (including activities and the exit ticket) -->

---

# Getting Data with `fetch()`

> `fetch()` sends an HTTP request from the browser; `response.json()` parses the JSON response

**Why:** this is how the front end reads the API's data (as in 5.17)

```js
addEventListener("DOMContentLoaded", async function() {
  const response = await fetch("/api/students");
  const students = await response.json();
  let html = "";
  for (let stu of students) {
    html += `<li>${stu.name}</li>`;
  }
  document.querySelector("ul").innerHTML = html;
});
```

<!--
The page (students.html with an empty <ul>) and the API are on the same Express server, so the URL is just /api/students.
response.json() returns an array of student objects. Check response.ok before using a single resource (7.5.3).
Live: show the GET request in the browser's Network tab.
-->

---

# Sending Data: POST with `fetch()`

> A second argument to `fetch()` sets the request **method**, **headers**, and **body**

**Why:** without `Content-Type: application/json`, the server won't accept the JSON

```js
const stu = { name: "Jack White", gpa: 2.5 };
const response = await fetch("/api/students", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify(stu)
});
if (response.ok) {
  const results = await response.json();
  alert("Added student with ID " + results._id);
}
```

- **PUT:** same, with `"PUT"` and the ID in the URL; **DELETE:** only `method`

<!--
JSON.stringify() converts a JavaScript object to a JSON string.
zyBooks 7.5 reads the student from form fields (document.querySelector("#name").value) and shows an error in a <p id="error"> when response.ok is false: document.querySelector("#error").textContent = "Cannot add student.";
PUT: fetch("/api/students/" + id, { method: "PUT", headers: { "Content-Type": "application/json" }, body: JSON.stringify(stu) })
DELETE: fetch("/api/students/" + id, { method: "DELETE" }) → nothing in the request body; on success, reload the list.
Ask: if the API returns 400, what does the page do? (Shows the error message; no alert.)
-->

---

<!-- _class: activity -->

> Activity: Put the steps in order

A. Mongoose's `Student.create()` saves the student in MongoDB

B. The user clicks Add, and `fetch()` sends a POST with the JSON-encoded student

C. The page checks `response.ok` and shows the new student's ID

D. `express.json()` converts the request body into `req.body`

E. The route sends a 201 response with the JSON-encoded student

F. The `/api` router sends the request to the `/students` POST route

<!--
Answer:
B → D → F → A → E → C
Follow-up: which steps run in the browser (B, C), and which on the server (D, F, A, E)?
-->

---

<!-- _class: activity -->

> Activity: Exit ticket - find the 4 bugs

```js
// server.js
const app = express();
const router = express.Router();
router.post("/students", async function(req, res) {
  try {
    const stu = Student.create(req.body);
    res.status(200).json(stu);
  } catch (ex) {
    res.status(400).send(ex.message);
  }
});
app.use("/api", router);

// page.js
const response = await fetch("/api/students", {
  method: "POST",
  body: JSON.stringify(stu)
});
```

<!--
Answers:
1. Missing app.use(express.json()) → req.body is not the parsed student.
2. Missing await before Student.create() → stu is not the saved student.
3. Wrong status code: a successful create returns 201, not 200.
4. The fetch() call is missing headers: { "Content-Type": "application/json" }.
Tip: these are the most common mistakes in the lab.
-->

---

# Key Takeaways

- A **RESTful web API** does CRUD on resources: **POST, GET, PUT, DELETE**
- Status codes: **200** OK, **201** Created, **204** No Content, **404** Not Found, **400** error
- `app.use("/api", router)` + `express.json()` → API routes that read `req.body`
- Routes `await` Mongoose: `find`, `findById`, `create`, `updateOne`, `deleteOne`
- `fetch(url, { method, headers, body })` + `response.ok` + `response.json()`

---

<!-- _class: demo -->

>30m
# Demo
7.2 RESTful APIs

- Songs API: Express + Mongoose CRUD routes
- React front end with Fetch

<!--
Setup: cd 7-2-restful-api; npm install. Front end: cd client; npm run dev. Back end (2nd terminal): cd server; npm install express cors mongoose dotenv; create server/.env with MONGO_URL (Atlas connection string ending in /swe363_songs) and PORT=5174; node server.js.
Tasks (see the TODOs in client/src/App.jsx): load .env with dotenv in server.js; Song schema + model in server/models/song.model.js (title, artist, year); routes in server/server.js: GET /api/songs, GET /api/songs/:id, POST /api/songs, PUT /api/songs/:id, DELETE /api/songs/:id. client/src/lib/api.js (fetch calls) is already written: walk through it and compare with 7.5.
Not in zyBooks 7.3/7.5 (the lab's TODO hints explain them):
- 7.4 parts (routes with Mongoose, 400/404 handling, project files) are on the slides because the lab needs them; the rest of 7.4 (search by genre with req.query, PUT vs. PATCH) is optional reading.
- cors / app.use(cors()) (zyBooks 7.4): React (port 5173) and Express (port 5174) are different origins; already written in server.js.
- dotenv, .env, process.env.MONGO_URL and process.env.PORT (not in zyBooks; lab TODO 1–2 hints).
- connectDB() helper in db.js with top-level await (lab file; 7.4 only says db.js connects to MongoDB).
- import / export and "type": "module" instead of require() (ES modules from 6.3); arrow-function route callbacks.
- Routes on app instead of express.Router (7.3 shows both work).
- Song.findByIdAndUpdate() with { new: true, runValidators: true }, Song.findByIdAndDelete(), .sort({ createdAt: -1 }), schema options trim and { timestamps: true } (not in zyBooks; 7.1/7.4 use updateOne/deleteOne).
- PUT returns the updated song as JSON (200) and errors as { message } JSON; DELETE uses res.status(204).end() (zyBooks uses sendStatus(204)).
- React front end: useState/useEffect (5.9, 5.17), components with props (5.7), Vite dev server, import.meta.env.VITE_API_URL.
- Testing with Postman (README); zyBooks uses the REST Client extension.
-->

---

# Next Class

- Third-party web APIs and token-based authentication (8.1–8.2)
- Password hashing (8.3)
