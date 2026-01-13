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
footer: 'SWE 363 | 251 | Sec F04 | KFUPM'
---


Web Engineering & Development (SWE 363) 
# Interactive Front-End Development
### Dr. Khadijah Al Safwan

---

# Announcements
- Please use the following link to inform us about your Github account: https://forms.office.com/r/HuvttUTp0A
- Quiz next Monday, Oct 20th on React
---

<!-- _class: activity -->

# React Sample Projects
[Github Repository](https://github.com/curioustushar/react-sample-projects)

---

# In today's lecture:
- Forms 
- Router

### Reference: 
- Zybook: 5.12-5.14
---
# 5.12 Forms (React)
---

# What are React Forms?

**React Forms** are controlled components where React manages the input values through state.

## Key Concepts:
- **Controlled Components** - React controls input values
- **State Management** - `useState` tracks form data
- **Validation** - Check data before submission
- **Event Handling** - Process form submission

---

# Controlled vs Uncontrolled Components

## Uncontrolled (Traditional HTML)
```jsx
<input type="text" />  // Browser manages value
```

## Controlled (React Way)
```jsx
const [email, setEmail] = useState("");

<input 
  type="email" 
  value={email} 
  onChange={(e) => setEmail(e.target.value)} 
/>
```

---

# Why Use Controlled Components?

### **Advantages:**
- **Single source of truth** - State controls the UI
- **Easy validation** - Check state before submission
- **Predictable behavior** - Same across all browsers
- **Dynamic updates** - UI updates as user types

### **Without controlled components:**
- Hard to validate
- Inconsistent behavior
- Difficult to reset forms

---

# Basic Form Structure

```jsx
import { useState } from "react";

function Registration() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [gender, setGender] = useState("");
  const handleSubmit = (e) => {
    e.preventDefault(); // Prevent page reload
    // Handle form submission
  };
  return (
    <form onSubmit={handleSubmit}>
      {/* Form fields go here */}
      <button type="submit">Register</button>
    </form>
  );
}
```
---

# Form Validation

### Why Validate?
- **User Experience** - Show helpful error messages
- **Data Quality** - Ensure correct information
- **Security** - Prevent invalid submissions

### Common Validation Rules:
- **Required fields** - Must not be empty
- **Email format** - Contains "@" and ends with ".com"
- **Password strength** - Minimum length, special characters
- **Radio selection** - Must choose an option

---

# Form - Validation Implementation

```jsx
const [errors, setErrors] = useState({});
const handleSubmit = (e) => {
  e.preventDefault();
  
  const nextErrors = {};
  // Email validation
  // ...

  // Password validation
  if (!password.trim()) {
    nextErrors.password = "Password is required";
  }
  setErrors(nextErrors);
  if (Object.keys(nextErrors).length > 0) return;
  
  alert(`User Registered: ${email}`); // Success! Show alert
};
```

---

# Form - Displaying Error Messages

## Error State
```jsx
const [errors, setErrors] = useState({});
```

## Error Display
```jsx
{errors.email && <p className="error">{errors.email}</p>}
{errors.password && <p className="error">{errors.password}</p>}
{errors.gender && <p className="error">{errors.gender}</p>}
```
---

# Form - Displaying Error Messages

## Complete Form Field with Error
```jsx
<div className="form-row">
  <label htmlFor="email">Email</label>
  <input
    id="email"
    type="email"
    value={email}
    onChange={(e) => setEmail(e.target.value)}
  />
  {errors.email && <p className="error">{errors.email}</p>}
</div>
```

---

# Form Submission Flow

## Step-by-Step Process:

1. **User fills form** → State updates
2. **User clicks submit** → `handleSubmit` runs
3. **Prevent default** → `e.preventDefault()`
4. **Validate data** → Check all fields
5. **Show errors** → Display validation messages
6. **Success action** → Show alert, reset form, navigate

---

# Disabling Form Submit Button

### Conditional Button State
```jsx
<button 
  type="submit" 
  disabled={!email || !password || !gender}
>
  Register
</button>
```

### Why Disable?
- **Prevents empty submissions**
- **Better UX** - Shows when form is ready
- **Visual feedback** - Button appears inactive

---
# 5.14 Router
---

# What is React Router?

**React Router** is a library that enables **client-side routing** in React applications.

## Key Benefits:
- **No page reloads** - Faster navigation
- **URL as state** - URLs represent user location
- **Better UX** - Smooth transitions between pages

## Think of it as:
> A **traffic controller** that decides which component to show based on the URL

---

# Traditional Web Navigation vs React Router

## Traditional Web (Server-Side)
```
User clicks link → Browser requests new page → Server sends HTML → Page reloads
```

## React Router (Client-Side)
```
User clicks link → URL changes → React shows new component → No reload!
```

---

# Basic Router Setup

### Step 1: Install React Router
```bash
npm i react-router-dom
```

### Step 2: Import Router Components
```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
```

### Step 3: Wrap Your App
```jsx
<BrowserRouter>
  <App />
</BrowserRouter>
```

---

# Creating Routes

### Basic Route Structure
```jsx
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
  <Route path="/registration" element={<Registration />} />
  <Route path="*" element={<h2>404 — Not Found</h2>} />
</Routes>
```

### Key Points:
- `path="/"` - Home page (exact match)
- `path="*"` - Catch-all for 404 pages
- `element={<Component />}` - What to render

---

# Navigation  Using Link Component

### Basic Link Syntax
```jsx
<Link to="/">Home</Link>
<Link to="/about">About</Link>
<Link to="/registration">Registration</Link>
```

## Key Features:
- **Changes URL** without page reload
- **Triggers route rendering** - Shows matching component
- **Simple navigation** - Basic link functionality
---

<!-- _class: demo -->

>30m
# Demo: Student Registration Portal
Starter code at: https://classroom.github.com/a/gd4XBP3Q

## What we'll build:
- **3 pages** with React Router
- **Registration form** with validation
- **Error handling** and success messages


---

# Common Mistakes to Avoid

## Router Mistakes:
-  Forgetting to wrap app in `BrowserRouter`
-  Using `href` instead of `to` prop
-  Not importing required components

## Form Mistakes:
-  Not using `e.preventDefault()`
-  Forgetting to validate before submission
-  Not handling empty state properly

---

# Next Class

- More on React