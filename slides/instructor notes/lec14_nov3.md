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
footer: 'SWE 363 | 252 | KFUPM'
---


Web Engineering & Development (SWE 363) 
# Back-end Development Fundamentals
### Dr. Khadijah Al Safwan

---

# Announcements
- Midterm and Quiz 2 on Tuesday, **Nov 4th**
  - 6:00-8:00 (pm)
  - Location: B22

---

# In today's lecture:
- Full-stack development (Node)

### Reference: 
- Zybook: 6.1
---
# 6.1 Full-stack Development

---

# What is Full-Stack Development?

<div class="two-column-slide">

<div class="column-left">

## Front-End (Client-Side)
- Code that runs **in the browser**
- What users **see and interact with**
- Built with: **React**, HTML, CSS, JavaScript
- Examples: buttons, forms, navigation

</div>

<div class="column-right">

## Back-End (Server-Side)
- Code that runs **on the server**
- Handles **data and business logic**
- Built with: **Node.js + Express**
- Examples: databases, APIs, authentication

</div>

</div>

---

# Front-End vs Back-End

<!-- _class: boxes -->

- **Front-End**
  User interface 
  
  Running in browser
  
  React components
  
- **Back-End**
  Server logic
  
  Running on server

  Handles requests
  
- **Full-Stack**
  
  Both together!
  
  Complete applications

---

# What is Node.js?

> **Node.js** is a JavaScript runtime environment

- Allows you to run JavaScript **outside the browser**
- Makes it possible to write **back-end code** using JavaScript
- Same language for front-end and back-end!

---

# Before Node.js

<div class="two-column-slide">

<div class="column-left">

**Without Node.js:**

**Front-End:**
- JavaScript 

**Back-End:**
- Python, Java, PHP, etc.

**Different languages!**

</div>

<div class="column-right">

**Now with Node.js:**

**Front-End:**
- JavaScript 

**Back-End:**
- JavaScript 

**Same language!**

</div>

</div>

---

# How Does Node.js Help Back-End?

Node.js allows the server to:

- **Handle server requests** from browsers
- **Read/write files** on the server
- **Respond with data** to the browser
- **Manage databases** and APIs

---

# What is Express?

> **Express** is a minimal web framework built on top of Node.js

- Makes back-end development **easier**
- Provides tools to create **routes**
- Handles **requests** and **responses** simply

---

# Why Use Express?

- **Simple** to create APIs
- **Handles JSON** easily
- **Less code** than raw Node.js
-  **Fast** to set up routes

---

# Request and Response

<div class="two-column-slide">

<div class="column-left">

## Request
**When the front-end asks for something**

Example:
> "Give me all students"

Browser sends:
```
GET /api/students
```

</div>

<div class="column-right">

## Response
**When the server sends back the answer**

Example:
> Server responds with JSON

```json
[
  { "id": 1, "name": "Ali" },
  { "id": 2, "name": "Sara" }
]
```

</div>

</div>

---

# HTTP Methods

Two main methods we'll use:

| Method | Purpose | Example |
|--------|---------|---------|
| **GET** | Request data | "Show me all students" |
| **POST** | Send data | "Add a new student" |

---

# Creating Routes in Express

A **route** is a path on the server that handles requests

```javascript
// GET route - request data
app.get('/api/students', (req, res) => {
  res.json(students);
});
```

- `/api/students` → the URL path
- `req` → the request from front-end
- `res` → the response we send back

---

# POST Route Example

```javascript
// POST route - send data to server
app.post('/api/students', (req, res) => {
  const newStudent = req.body; // data from front-end
  // Add to database/array
  students.push(newStudent);
  res.json(newStudent); // send back the new student
});
```

---

# How Data Flows

<div class="two-column-slide">

<div class="column-left">

## 1. Front-End
```javascript
fetch('http://localhost:3000/api/students')
  .then(r => r.json())
  .then(data => setStudents(data));
```

**Sends REQUEST** →

</div>

<div class="column-right">

## 2. Back-End
```javascript
app.get('/api/students', (req, res) => {
  res.json(students);
});
```

**← Sends RESPONSE**

</div>

</div>

---

# Complete Flow Diagram

```
Front-End (React)          Back-End (Express)
     │                            │
     │ 1. REQUEST                 │
     │ GET /api/students ────────>│
     │                            │
     │                            │ 2. Process request
     │                            │    Find students data
     │                            │
     │ 3. RESPONSE                │
     │ <──────────────── JSON ────│
     │                            │
     │ 4. Update UI               │
     │    Display students        │
```

---

# Testing the Back-End

1. **Start the server:**
```bash
node server.js
```

2. **Open browser:**
```
http://localhost:3000/api/students
```

3. **See JSON directly in browser!** 

---


# Key Takeaways

- **Full-stack** = Front-end + Back-end
- **Node.js** = Run JavaScript on server
- **Express** = Framework to build APIs easily
- **Request** = Front-end asks for data
- **Response** = Back-end sends data (JSON)
- **Routes** = Server paths that handle requests

---

<!-- _class: demo -->

>30m
# Demo
Starter code at: https://classroom.github.com/a/wtcNr7U4

---

# Next Class

- More on NodeJS