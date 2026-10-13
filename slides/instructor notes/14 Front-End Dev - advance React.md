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
    section.boxes li { background-color:var(--foreground); color:var(--background); padding: 40px; margin: 10px; border-radius: 10px; flex: 1; text-align: center; }
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
# Advanced React


---

# In today's lecture:
- Styling
- React Bootstrap
- Fetching Data


### Reference: 
- Zybook: 5.15-5.17
---
# 5.15 Styling (React)

---

# Three Ways to Style React Components

## Key Concepts:
- **Inline**: `style={{ ... }}` — camelCase CSS props (e.g. `backgroundColor`)
- **CSS file**: `import "./App.css"` + `className="..."` (not `class`)
- **CSS Modules**: `import styles from './X.module.css'` → scoped class names

```jsx
<div style={{ backgroundColor: 'blue', padding: '20px' }}>Inline</div>

import "./Welcome.css";
<div className="my-card">CSS file</div>

import styles from './Card.module.css';
<div className={styles.card}>CSS Module</div>
```

---

# CSS Variables & Responsive Design

```css
:root {
  --primary-color: #0d6efd;
  --light-color: #f8f9fa;
}
.my-button { background-color: var(--primary-color); }

/* Mobile first, then larger screens */
.user-avatar { width: 50px; }
@media (min-width: 768px)  { .user-avatar { width: 60px; } }
@media (min-width: 1024px) { .user-avatar { width: 80px; } }
```

- **CSS variables**: define once in `:root`, reuse with `var(--name)`
- **Media queries**: change styles by viewport width

---

# 5.16 React Bootstrap

---

# What is React Bootstrap?

**Bootstrap** = CSS framework (pre-built, responsive components)

**React-Bootstrap** = Bootstrap as React components (props instead of only classes)

```bash
npm install react-bootstrap bootstrap
```

```html
<!-- public/index.html -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
```

---
<!-- _class: activity -->

# [React Bootstrap docs](https://react-bootstrap.netlify.app/)

---

# Layout & Utility Classes

```jsx
import { Container, Row, Col } from 'react-bootstrap';

<Container>
  <Row>
    <Col md={6} lg={4}>Column 1</Col>
    <Col md={6} lg={4}>Column 2</Col>
    <Col md={12} lg={4}>Column 3</Col>
  </Row>
</Container>
```

**Utilities (className):**
- Spacing: `mb-4`, `mt-5`, `py-3`, `px-2`
- Color: `bg-primary`, `text-white`, `bg-light`
- Layout: `d-flex`, `justify-content-center`, `align-items-center`, `text-center`

---

# 5.17 Fetching Data

---

# The Problem: When to Fetch?

You already know `fetch()` — but **when** do you call it in a component?

```jsx
function Users() {
  // ❌ Don't fetch here — runs on every render, can cause infinite loops
  fetch('https://jsonplaceholder.typicode.com/users')
    .then(r => r.json())
    .then(data => setUsers(data));

  return <div>...</div>;
}
```

**Need:** run the fetch **once** after the component appears on the screen → use **`useEffect`**

---

# What is `useEffect`?

`useEffect` = run **side effects** after React paints the UI (fetching, timers, subscriptions)

```jsx
import { useEffect } from 'react';
useEffect(() => {
  // code here runs AFTER the first render
  console.log('Component mounted');
}, []);
```

- **1st argument**: a function — the effect to run
- **2nd argument**: **dependency array** — when to re-run
  - `[]` → run **once** after mount
  - `[userId]` → re-run when `userId` changes
  - omitted → run after **every** render (usually avoid)

---

# State for Fetched Data

Use **three pieces of state** while waiting for the API:

```jsx
import { useState } from 'react';

const [users, setUsers] = useState([]);      // the data
const [loading, setLoading] = useState(true); // still waiting?
const [error, setError] = useState(null);     // something went wrong?
```

| State | Purpose |
|-------|---------|
| `users` | Store the JSON you get back |
| `loading` | Show a spinner / “Loading...” |
| `error` | Show an error message |

---

# Putting It Together

```jsx
import { useState, useEffect } from 'react';

useEffect(() => {
  const fetchUsers = async () => {
    try {
      setLoading(true);
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      if (!response.ok) throw new Error(`HTTP ${response.status}`);
      setUsers(await response.json());
    } catch (err) { setError(err.message);
    } finally { setLoading(false);
    }
  };
  fetchUsers();          // call the async function from inside the effect
}, []);                  // [] = fetch once when the component mounts
```

**Note:** `useEffect` itself cannot be `async` — define an `async` function **inside**, then call it.

---

# Loading, Error & Empty UI

Always handle all three states when rendering fetched data:

```jsx
{loading && <p>Loading users...</p>}

{error && <Alert variant="danger">{error}</Alert>}

{!loading && !error && users.length === 0 && (
  <Alert variant="info">No users found.</Alert>
)}

{!loading && !error && users.map(user => (
  <div key={user.id}>{user.name}</div>
))}
```

---


<!-- _class: demo -->

>30m
# Demo
5.6 React Styling & Fetching 


