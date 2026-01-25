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
footer: 'SWE 363 | 252 | KFUPM'
---


Web Engineering & Development (SWE 363) 
# Interactive Front-End Development

---

# Announcements
- Demo submission, commit each TODO
- Demo grading issue, send email to Muhannad Mufti <g202392310@kfupm.edu.sa> and copy Dr. Al Safwan and Qurratulain


---

# In today's lecture:

- Getting started with React
- JSX
- Components

### Reference: 
- Zybook: 5.5 to 5.7 

---

# 5.5 Getting Started with React

---

# What is React? 

React is a **JavaScript library** for building user interfaces

- Created by **Facebook (Meta)** in 2013
- Makes building web apps **easier** and **more organized**
- Focuses on **components** - reusable pieces of UI

**Think of it as:** A better way to build interactive websites!

---

# Why Do We Need React? 

## Traditional Web Development Problems:
- **Complex DOM manipulation** with vanilla JavaScript
- **Hard to maintain** large applications
- **Repetitive code** for similar UI elements
- **Difficult to manage** state and data flow

---

# Why Do We Need React? 
## React Solution:
- **Component-based** architecture
- **Automatic UI updates** when data changes
- **Reusable components** reduce code duplication
- **Better organization** and maintainability


---
<!-- _class: activity -->

# React.js: The Documentary

[How A Small Team of Developers Created React at Facebook](https://www.youtube.com/embed/8pDqJVdNa44?si=2LVEC6lqvFA9bJgy)

---

# React vs Traditional Approach

## Traditional Way:
```html
<!-- HTML -->
<div id="user-card">
  <h3 id="user-name">Loading...</h3>
  <p id="user-email">Loading...</p>
</div>
```

```javascript
// JavaScript - Manual DOM manipulation
document.getElementById('user-name').textContent = 'Ahmed';
document.getElementById('user-email').textContent = 'ahmed@kfupm.edu.sa';
```
---

# React vs Traditional Approach
## React Way:
```jsx
// One component handles everything
function UserCard({ name, email }) {
  return (
    <div>
      <h3>{name}</h3>
      <p>{email}</p>
    </div>
  );
}
```

---

# Key Benefits of React

| Benefit | Explanation |
|---------|-------------|
| **Reusable Components** | Build once, use everywhere. Like LEGO blocks for web development |
| **Virtual DOM** | Faster updates than direct DOM manipulation. React figures out what changed and updates only that part |
| **Strong Ecosystem** | Backed by Meta (Facebook). Huge community and many tools |
| **Single Page Applications (SPA)** | No page reloads. Smooth, app-like experience |

---

# How React Works

## The React Process:
1. **You write components** using JSX
2. **React creates a Virtual DOM** (in-memory representation)
3. **When data changes**, React compares old vs new Virtual DOM
4. **React updates only the changed parts** in the real DOM

## Result:
&emsp;&emsp;**Faster performance** &emsp;&emsp;&emsp; **Less work for developers** &emsp;&emsp;&emsp; **Automatic updates**

---

# Setting Up a React Project 

## Using Vite (Modern & Fast):
```bash
# Create new React project
npm create vite@latest my-react-app


# Navigate to project
cd my-react-app

# Install dependencies
npm install

# Start development server
npm run dev
```

---

# React Project Structure 📁

```
my-react-app/
├── node_modules/        # Dependencies
├── public/              # Static files (images, etc.)
├── src/                 # Your code lives here
│   ├── App.jsx          # Main app component
│   ├── main.jsx         # Entry point
│   └── components/      # Your custom components
├── package.json         # Project configuration
└── vite.config.js       # Vite settings
```

---

# How React Renders Your App 

## 1. `main.jsx` (Entry Point):
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

---

# How React Renders Your App

## 2. `App.jsx` (Main Component):
```jsx
function App() {
  return (
    <div>
      <h1>Hello React!</h1>
    </div>
  )
}

export default App
```

---

# Your First React Component 

## Create `src/components/Welcome.jsx`:
```jsx
function Welcome() {
  return (
    <div>
      <h1>Welcome to React!</h1>
      <p>This is my first component</p>
    </div>
  );
}

export default Welcome;
```

---

# Using Your Component 

## Use it in `App.jsx`:
```jsx
import Welcome from './components/Welcome';

function App() {
  return (
    <div>
      <Welcome />
    </div>
  );
}

export default App;
```

---

# 5.6 JSX

---

# What is JSX? 

**JSX** = JavaScript XML

- A special syntax that lets you write **HTML-like code inside JavaScript**
- Makes React components **easier to read and write**
- **Not HTML** - it's JavaScript that looks like HTML

**Example:**
```jsx
function MyComponent() {
  return <h1>Hello, World!</h1>;
}
```

---

# Why Use JSX? 

### Without JSX (Traditional JavaScript):
```javascript
function createElement() {
  const h1 = document.createElement('h1');
  h1.textContent = 'Hello, World!';
  h1.className = 'title';
  return h1;
}
```

### With JSX (React):
```jsx
function MyComponent() {
  return <h1 className="title">Hello, World!</h1>;
}
```

**JSX is much cleaner and easier to read!**

---

# JSX Rules 📋

## 1. **Must Return a Single Element**
```jsx
// WRONG - Multiple elements
function BadComponent() {
  return ( <h1>Title</h1>
           <p>Paragraph</p> );
}
// CORRECT - Wrapped in one element
function GoodComponent() {
  return (
    <div>
      <h1>Title</h1>
      <p>Paragraph</p>
    </div>
  );
}
```

---

# JSX Rules

## 2. **Use `className` Instead of `class`**
```jsx
// WRONG
<div class="container">Content</div>

// CORRECT
<div className="container">Content</div>
```
---

# JSX Rules
## 3. **Self-Closing Tags Must Have `/`**
```jsx
//  WRONG
<img src="image.jpg">

//  CORRECT
<img src="image.jpg" />
```

---

# JSX Rules (cont.) 📋

## 4. **Use `{}` for JavaScript Expressions**
```jsx
function Greeting({ name, age }) {
  return (
    <div>
      <h1>Hello, {name}!</h1>
      <p>You are {age} years old</p>
      <p>Next year you'll be {age + 1}</p>
    </div>
  );
}
```

---

# JSX Rules

## 5. **Use `camelCase` for Attributes**
```jsx
//  WRONG
<div tabindex="0" onclick={handleClick}>

// CORRECT
<div tabIndex="0" onClick={handleClick}>
```

---

# JSX Examples 💡

## Basic JSX:
```jsx
function UserCard() {
  const userName = "Ahmed";
  const userEmail = "ahmed@kfupm.edu.sa";
  
  return (
    <div className="card">
      <h2>{userName}</h2>
      <p>{userEmail}</p>
      <button onClick={() => alert('Hello!')}>
        Click Me
      </button>
    </div>
  );
}
```

---

# JSX with Conditional Rendering 

```jsx
function UserStatus({ isLoggedIn, userName }) {
  return (
    <div>
      {isLoggedIn ? (
        <p>Welcome back, {userName}!</p>
      ) : (
        <p>Please log in</p>
      )}
    </div>
  );
}
```

---

# JSX with Lists 

```jsx
function StudentList({ students }) {
  return (
    <ul>
      {students.map(student => (
        <li key={student.id}>
          {student.name} - {student.grade}
        </li>
      ))}
    </ul>
  );
}
```
---

# 5.7 Components

---

# What is a Component? 

A **component** is a **reusable piece of UI**

- Like a **function** that returns HTML
- **Small, focused** on one thing
- **Reusable** - use it multiple times
- **Composable** - combine components to build complex UIs

**Think of it as:** A custom HTML element you create!

---

# Component Analogy

## Building a House:
- **Foundation** (App component)
- **Rooms** (Header, Sidebar, MainContent components)
- **Furniture** (Button, Card, Input components)

## Building a Website:
- **App** (main container)
- **Header, Navigation, Footer** (layout components)
- **Button, Card, Form** (reusable components)


---

# Creating and Using Components

## Step 1: Create `src/components/StudentCard.jsx`:
```jsx
function StudentCard() {
  return (
    <div className="student-card">
      <h3>Ahmed Al-Saeed</h3>
      <p>ID: 202333345</p>
      <p>Department: Computer Science</p>
    </div>
  );
}

export default StudentCard;
```

---

# Creating and Using Components

## Step 2: Use it in `App.jsx`:
```jsx
import StudentCard from './components/StudentCard';

function App() {
  return (
    <div>
      <h1>Student Directory</h1>
      <StudentCard />
    </div>
  );
}
```

---

# Making Components Dynamic with Props

## Updated `StudentCard.jsx`:
```jsx
function StudentCard({ name, id, department }) {
  return (
    <div className="student-card">
      <h3>{name}</h3>
      <p>ID: {id}</p>
      <p>Department: {department}</p>
    </div>
  );
}

export default StudentCard;
```

---

# Using Props in App.jsx 

## Using it in `App.jsx`:
```jsx
import StudentCard from './components/StudentCard';

function App() {
  return (
    <div>
      <h1>Student Directory</h1>
      <StudentCard 
        name="Ahmed Al-Saud" id="202312345" department="Computer Science" 
      />
      <StudentCard 
        name="Sara Al-Rashid" id="202312346" department="Software Engineering" 
      />
    </div>
);}
```

---

# Props Explained 

**Props** = Properties

- **Data passed from parent to child** component
- Make components **reusable** and **dynamic**
- **Read-only** - child can't change props
- Like **function parameters** but for components


---

# Component Types 

## 1. **Function Components** (Modern & Recommended):
```jsx
function Welcome({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

## 2. **Arrow Function Components**:
```jsx
const Welcome = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};
```
---

# Component Types 
## 3. **Class Components** (Older, still works):
```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```

---

# Component Best Practices 

## 1. **One Component Per File**
```
src/
├── components/
│   ├── StudentCard.jsx
│   ├── Header.jsx
│   └── Footer.jsx
```

## 2. **Descriptive Names**
```jsx
// Good
function UserProfileCard() { ... }
// Bad
function Card() { ... }
```
---

# Component Best Practices 

## 3. **Export Default**
```jsx
function MyComponent() { ... }
export default MyComponent;
```

## 4. **Keep Components Small**
```jsx
// Good - One responsibility
function StudentName({ name }) { return <h3>{name}</h3>; }
// Bad - Too many responsibilities
function StudentCard({ name, id, department, grades, schedule }) {
  // Too much code here
}
```

---

# Component Best Practices 

## 5. **Use Meaningful Props**
```jsx
// Good
<StudentCard name="Ahmed" studentId="123" />

// Bad
<StudentCard a="Ahmed" b="123" />
```

---

<!-- _class: demo -->

>30m
# Demo
Starter code at: https://classroom.github.com/a/09PRaIoj

---

# Next Class

- More on React