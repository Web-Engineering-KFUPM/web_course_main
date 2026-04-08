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

---

# In today's lecture:
- Express.js Request data 
  - Query String Parameters
  - Route Parameters
  - Param Middleware
  - Request Body
  - Sending JSON Responses
  - Status Codes

### Reference: 
- Zybook: 6.5
---
# 6.5 Express request data 

---

# How do we get data from the client?

When a client makes a request to our server, they often send **data**:

- **Query parameters**: `/search?q=react&page=2`
- **Route parameters**: `/users/123` or `/profile/John/Doe`
- **Request body**: JSON data, form data, etc.

Today we'll learn how to **read** this data in Express!

---

# Three ways to send data

| Method | Location | Example | Use Case |
|--------|----------|---------|----------|
| **Query String** | URL | `/search?q=react&page=2` | Optional filters, search terms |
| **Route Parameters** | URL path | `/users/123` | Identifying specific resources |
| **Request Body** | HTTP body | POST with JSON | Creating/updating data |

---

# 1. Query String Parameters

---

# What are Query String Parameters?

**Query strings** are key-value pairs added to URLs after `?`

```
http://localhost:3000/search?q=react&page=2&sort=date
```
**Format**: `?key1=value1&key2=value2&key3=value3`

---

# Why use Query Strings?

**Optional** - can be added or removed easily  
**Bookmarkable** - URLs can be saved/shared  
**Cacheable** - browsers can cache different query combinations  
**Flexible** - don't change the resource path

**Common uses**: Search terms, filters, pagination, sorting

---

# Reading Query Parameters in Express

Use `req.query` to access query string parameters

```js
app.get("/search", (req, res) => {
  const { q, page, sort } = req.query;
  // q = "react"
  // page = "2"
  // sort = "date"
  
  res.json({ query: q, page, sort });
});
```

**Important**: Values are always **strings**!

---

# Query Parameters: Important Notes

 **Values are strings** - convert if needed:
```js
const page = Number(req.query.page) || 1;
```

 **Always validate** - check if required params exist:
```js
if (!req.query.name) {
  return res.status(400).json({ error: "name required" });
}
```

 **Optional by nature** - missing params are `undefined`

---

# 2. Route Parameters

---

# What are Route Parameters?

**Route parameters** are **named placeholders** in the URL path

```js
app.get("/users/:userId", (req, res) => {
  // :userId is a route parameter
});
```

**URL**: `/users/123`  
**Parameter**: `userId = "123"`

They identify **specific resources** in the path!

---

# Why use Route Parameters?

**Clean URLs** - `/users/123` vs `/users?id=123`  
**RESTful** - follows REST API conventions  
**Descriptive** - makes the resource clear  
**Hierarchical** - supports nested resources

**Example**: `/orders/987/items/2` (order 987, item 2)

---

# Reading Route Parameters

Use `req.params` to access route parameters

```js
app.get("/users/:userId", (req, res) => {
  const { userId } = req.params;
  // userId = "123" (string)
  
  res.json({ userId });
});
```

**URL**: `/users/123` → `userId = "123"`

---

# Multiple Route Parameters

You can have multiple parameters in one route:

```js
app.get("/profile/:first/:last", (req, res) => {
  const { first, last } = req.params;
  
  res.json({
    ok: true,
    fullName: `${first} ${last}`
  });
});
```

**URL**: `/profile/Jack/Black`  
**Result**: `{ ok: true, fullName: "Jack Black" }`

---

# Route Parameters: Important Notes

 **Values are strings** - convert to numbers if needed:
```js
const userId = Number(req.params.userId);
```

 **Required by route** - if missing, route won't match

 **Order matters** - `/users/:id/posts/:postId` vs `/users/:postId/posts/:id`

---

# Query vs Route Parameters

| Feature | Query Parameters | Route Parameters |
|--------|------------------|------------------|
| **Syntax** | `?key=value` | `/:paramName` |
| **Required?** | Optional | Required (for route match) |
| **Use Case** | Filters, search, pagination | Resource identification |
| **Example** | `/search?q=react` | `/users/123` |
| **Access** | `req.query` | `req.params` |

---

# 3. Route Parameter Middleware

---

# The Problem: Repeated Validation

What if multiple routes use the same parameter? **Problem**: Code duplication! 

```js
app.get("/users/:userId", (req, res) => {
  const userId = Number(req.params.userId);
  if (!Number.isFinite(userId) || userId < 1) {
    return res.status(400).json({ error: "Invalid userId" });
  }
  // ... use userId
});

app.delete("/users/:userId", (req, res) => {
  const userId = Number(req.params.userId);
  if (!Number.isFinite(userId) || userId < 1) {
    return res.status(400).json({ error: "Invalid userId" });
  }
  // ... same validation again!
});
```

---

# Solution: Param Middleware

`app.param()` runs **once** when a route with that parameter matches

```js
app.param("userId", (req, res, next, userId) => {
  const num = Number(userId);
  if (!Number.isFinite(num) || num < 1) {
    return res.status(400).json({
      ok: false,
      error: "userId must be positive number"
    });
  }
  req.userIdNum = num; // Store validated value
  next(); // Continue to route handler
});
```

**Runs automatically** for any route with `:userId`!

---

# Using Param Middleware

After defining param middleware, routes can use the validated value:

```js
// Middleware (runs first)
app.param("userId", (req, res, next, userId) => {
  const num = Number(userId);
  if (!Number.isFinite(num) || num < 1) {
    return res.status(400).json({ 
      ok: false, error: "userId must be positive number"
    });
  }
  req.userIdNum = num;
  next();
});
// Route (uses validated value)
app.get("/users/:userId", (req, res) => {
  res.json({ ok: true, userId: req.userIdNum });
});
```

---

# Param Middleware: How It Works

1. **Request comes in**: `/users/42`
2. **Express matches route**: `GET /users/:userId`
3. **Param middleware runs**: `app.param("userId", ...)`
   - Validates and converts `"42"` → `42`
   - Stores in `req.userIdNum`
   - Calls `next()`
4. **Route handler runs**: Uses `req.userIdNum`

**One validation, multiple routes benefit!** 

---

# Param Middleware: Benefits

**DRY** - Don't Repeat Yourself  
**Centralized validation** - one place to fix bugs  
**Consistent** - all routes get same validation  
**Reusable** - works for GET, POST, DELETE, etc.

**Best for**: Type conversion, validation, normalization

---

# 4. Receiving JSON Data

---

# Request Body: Another Way to Send Data

So far we've seen data in URLs (query strings, route params)

**Request body** is data sent in the HTTP request body:

- **JSON**: `{ "name": "Ali", "age": 22 }`
- **Form data**: `name=Ali&age=22`
- **Files**: multipart/form-data

Common for **POST** and **PUT** requests

---

# Why Use Request Body?

**URLs have limits**:
- Query strings get long and messy
- Route params are for resource IDs
- Sensitive data shouldn't be in URLs

**Request body is better for**:
- Large amounts of data
- Complex objects
- Sensitive information (passwords, etc.)
- Creating/updating resources

---

# Receiving JSON in Express

To receive JSON data, you need **middleware** to parse it:

```js
import express from "express";
const app = express();

// Enable JSON parsing middleware
app.use(express.json());

// Now you can read JSON from req.body
app.post("/users", (req, res) => {
  const { name, age } = req.body;
  // name = "Ali"
  // age = 22
  res.json({ ok: true, user: { name, age } });
});
```

**Important**: `app.use(express.json())` must come **before** your routes!

---

# Receiving URL-Encoded Data

For traditional HTML forms, use `express.urlencoded()`:

```js
app.use(express.urlencoded({ extended: true }));

app.post("/login", (req, res) => {
  const { username, password } = req.body;
  // Data comes from form: username=john&password=secret
  // ...
});
```

**Difference**:
- `express.json()` - parses JSON bodies
- `express.urlencoded()` - parses form data (`key=value&key2=value2`)

---

# Request Body: Important Notes

**Always validate** - check required fields:
```js
if (!req.body.name) {
  return res.status(400).json({ error: "name required" });
}
```

**Middleware order matters** - `app.use(express.json())` before routes

**Data types** - JSON preserves types (numbers, booleans, etc.)

**Security** - validate and sanitize all input!

---

# Summary: All Ways to Get Data

| Source | Access | Example | Use Case |
|--------|--------|---------|----------|
| **Query String** | `req.query` | `/search?q=react` | Optional filters |
| **Route Params** | `req.params` | `/users/123` | Resource ID |
| **Request Body** | `req.body` | POST with JSON | Creating/updating data |

---

# 5. Sending JSON Responses

---

# Sending JSON in Express

Use `res.json()` to send JSON responses:

```js
app.get("/data", (req, res) => {
  res.json({ ok: true, message: "Success!" });
});
```

**Automatically**:
- Sets `Content-Type: application/json`
- Converts object to JSON string
- Sends response

---

# Setting Status Codes

Use `res.status()` before `res.json()`:

```js
// Success (200 is default)
res.json({ ok: true, data: result });

// Error (400 Bad Request)
res.status(400).json({
  ok: false,
  error: "Invalid input"
});

// Not Found (404)
res.status(404).json({
  ok: false,
  error: "Resource not found"
});
```

---

# Common Status Codes

| Code | Meaning | Use Case |
|------|---------|----------|
| `200` | OK | Successful request |
| `400` | Bad Request | Invalid input/parameters |
| `404` | Not Found | Resource doesn't exist |
| `500` | Server Error | Server-side error |

**Always include status codes for errors!**

---

# Summary: Request Data in Express

| Type | Access | Example | Use Case |
|------|--------|---------|----------|
| **Query** | `req.query` | `/search?q=react` | Optional filters |
| **Route** | `req.params` | `/users/123` | Resource ID |
| **Body** | `req.body` | POST with JSON | Creating/updating data |
| **Param Middleware** | `app.param()` | Validates route params | Reusable validation |


---

<!-- _class: demo -->

>30m
# Demo
6.4 Request Data in Express
