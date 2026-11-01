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
# Back-End Development Fundamentals

---

# In today's lecture:
- Full-stack development
- A first look at Express

### Reference: 
- Zybook: 6.1, 6.4 (intro only)
---

<!-- _class: activity -->

> Activity: Think-Pair-Share (2 min)

You log in to the KFUPM portal and see your grades.

1. What happened between clicking Login and seeing your grades?
2. Which parts ran on your laptop? Which ran somewhere else?
3. Where are the grades actually stored?

<!--
Answers:
1. The browser sent a request to the web server. The server got your grades from the database and sent a response back. The browser then displayed the page.
2. Your laptop (web browser): the page, the button, and displaying the grades. Somewhere else (web server): fetching the grades from the database.
3. In a database that the web server talks to, not in the browser.
Tip: collect answers on the board in three columns (browser / server / database) and reuse them on the next two slides.
-->

---
# 6.1 Full-stack Development

<!-- Timing: ~15 min for 6.1 (including activities) -->

---

# What is Full-Stack Development?

- **Front end** → runs in the **web browser** (HTML, CSS, JavaScript)
- **Back end** → runs on the **web server** (PHP, Node.js, Python)
- **Database** → stores the application data
- **Full-stack development** → developing **both** ends

```
Front End (Web browser)       Back End (Web server)         Database
     │ ──── 1. REQUEST ───────────> │                           │
     │                              │ ──── 2. Query ──────────> │
     │                              │ <─── 3. Data ──────────── │
     │ <─── 4. RESPONSE ─────────── │                           │
```

---

<!-- _class: activity -->

> Activity: Front end, back end, or database? (hands up)

1. An "Add to cart" button styled with CSS
2. Code that fetches and modifies product information
3. The table that stores every product
4. A React component that shows a product card
5. A Python program that generates a personalized webpage
6. A layout that works on different screen sizes

<!--
Answers:
1. Front end
2. Back end
3. Database
4. Front end
5. Back end
6. Front end
-->

---

# Front-End Development

- Focuses on the **user interface (UI)**
- Must work on **different devices and screen sizes**
- Must be **accessible** (e.g., screen readers)

**Library** = functions for a related set of tasks
**Framework** = a suite of libraries, a more complete platform

| Name | Type |
|------|------|
| Bootstrap, Tailwind | CSS framework |
| **React** | JavaScript library |
| Vue.js, Angular | JavaScript framework |

---

# Back-End Development: Two Approaches

<div class="two-column-slide">

<div class="column-left">

## Dynamic Webpage
- Page **generated on the web server** when requested
- Personalized to the user

</div>

<div class="column-right">

## Web API
- Functions invoked using **HTTP**
- The front end uses **JavaScript** to call them

</div>

</div>

---

<!-- _class: activity -->

> Activity: Dynamic webpage or web API?

1. Becky is shown a webpage that lists the items in her shopping cart.
2. A retailer's front end uses JavaScript to request all sale items, then displays them.
3. A PHP program generates a profile page for the logged-in user.

<!--
Answers:
1. Dynamic webpage
2. Web API
3. Dynamic webpage
Tip: point out that today's lab builds a tiny web API.
-->

---

# Server-Side Platforms

| Platform | Language | Popular Frameworks |
|----------|----------|--------------------|
| ASP.NET | C# | Blazor, MVC |
| Java | Java | Spring Boot |
| **Node.js** | **JavaScript** | **Express**, NestJS |
| PHP | PHP | Laravel, Symfony |
| Python | Python | Django, Flask, FastAPI |

### In this course: **Node.js + Express**

---

# Databases

<div class="two-column-slide">

<div class="column-left">

## Relational (SQL)
- Data in **tables**
- MySQL, PostgreSQL

```sql
SELECT * FROM product
WHERE price < 900;
```

</div>

<div class="column-right">

## Document (NoSQL)
- Data in **JSON** format
- **MongoDB**

```js
db.products.find(
  { price: { $lt: 900 } }
);
```

</div>

</div>

---

<!-- _class: activity -->

> Activity: Predict

| id | title | price |
|----|-------|-------|
| 123 | Laptop | 350.99 |
| 445 | Smart TV | 1199.99 |
| 876 | Tablet | 499.99 |

&nbsp;

1. Which products does `SELECT * FROM product WHERE price < 900;` return?
2. Adding a fourth product adds a new table, row, or column?
3. True or False: the front end pulls data directly from the database.

<!--
Answers:
1. Laptop (350.99) and Tablet (499.99)
2. Row
3. False: the front end interacts with the back end, and the back end works with the database.
-->

---

# A First Look at Express

<!-- Timing: ~12 min. Only what the 6.1 lab needs; static files, POST routes, and middleware come with the full 6.4 lecture. -->

---

# What is Express?

> **Express** is a popular **Node.js framework** for creating web applications and **web APIs**

**Install it with npm:**
```bash
npm install express
```

After installing, the package is in the project's `node_modules` directory

---

# A Minimal Express Server

```js
// server.js
const express = require("express");   // import the express module
const app = express();                 // create the Express app object

// routes go here

app.listen(3000, function() {          // start listening on port 3000
  console.log("Listening on port 3000...");
});
```

```bash
node server.js     # stop with Ctrl+C
```

- `express()` **creates** the app; it does not start the server
- `app.listen()` **starts** the server

---

# Routes

> A **route** = an HTTP method + a URL path + a **callback function**: `app.method(path, callback)`

```js
// Called for GET request to http://localhost:3000/hello
app.get("/hello", function(req, res) {
  res.send("<h1>Hello, Express!</h1>");
});

// Called for GET request to http://localhost:3000/course
app.get("/course", function(req, res) {
  res.json({ code: "SWE 363", title: "Web Engineering" });
});
```

- `req` / `res` → the HTTP **request** and **response**
- `res.send()` → sends HTML; `res.json()` → sends an object as **JSON**

<!--
Live: add the /hello route, restart the server, and refresh the browser.
-->

---

<!-- _class: activity -->

> Activity: Predict what the browser shows

```js
app.get("/hello", function(req, res) {
  res.send("<h1>Hello, Express!</h1>");
});
app.get("/course", function(req, res) {
  res.json({ code: "SWE 363" });
});
app.listen(3000);
```

1. `http://localhost:3000/hello`
2. `http://localhost:3000/course`
3. `http://localhost:3000/contact`
4. `http://localhost/hello`

<!--
Answers:
1. The heading "Hello, Express!"
2. The JSON { "code": "SWE 363" }
3. A 404 error: no route matches /contact.
4. It doesn't reach the server: the URL is missing port 3000.
-->

---

<!-- _class: activity -->

> Activity: Put the steps in order

A. `app.listen()` starts the server on port 3000

B. The browser requests `http://localhost:3000/hello`

C. `require("express")` imports Express, and `express()` creates the app

D. `res.send()` sends the response, and the browser displays it

E. The `/hello` route's callback function runs

<!--
Answer:
C → A → B → E → D
Follow-up: which steps happen on the server, and which in the browser? (Server: C, A, E, D. Browser: B and displaying the result.)
-->

---

# Key Takeaways

- **Front end** = browser, **back end** = server, **database** = stored data
- Back ends generate **dynamic webpages** or provide a **web API**
- **Express:** `express()` creates the app, `app.listen()` starts it
- **Route:** `app.method(path, callback)`
- `res.send()` → HTML, `res.json()` → JSON

---

<!-- _class: demo -->

>30m
# Demo
6.1 Back-End Fundamentals

<!--
Setup: npm install; npm install express cors; npm run dev (front end); cd backend && node server.js (back end, 2nd terminal).
Tasks: backend/server.js (import Express, create app, enable cors, listen on 3000, routes /, /about, /student) and src/App.jsx (fetch /student on load, store in state, display it).
Not in zyBooks ch6 (the lab's TODO hints explain them):
- import express from "express" (the lab uses import instead of require; ES modules are covered in 6.3 next lecture)
- cors (covered in zyBooks ch7): needed because React (port 5173) and Express (port 3000) run on different origins
- fetch / useEffect / useState in React (from zyBooks 5.17)
-->

---

# Next Class

- Node.js & npm (6.2)
- Modules (6.3)
