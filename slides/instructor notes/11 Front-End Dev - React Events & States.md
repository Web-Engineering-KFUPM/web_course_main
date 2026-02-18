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
# Interactive Front-End Development

---

# Announcements 📣
- Midterm Exam 
  - Date: April 2nd
  - Time: 7:00-9:00 (pm)
  - Location: B22 (Rooms 119, 125,127, 130, 134)
- Command to get admin access in the lab PCs
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```
---

# In today's lecture:

- Event handling
- State

### Reference: 
- Zybook: 5.8-5.9 

---
# 5.8 Event handling

---
# What is Event Handling?

**Event handling** allows your React components to respond to user interactions

<div class="two-column-slide">
      <div class="column-left">
      
### Examples of Events:
- User clicks a button
- User types in an input field
- User submits a form
- User hovers over an element
</div>
<div class="column-right">

### Why do we need it?
- Makes web pages **interactive**
- Responds to user actions
- Creates dynamic user experiences
</div>
</div>

---

# Event Handling in React vs HTML

### HTML Event Handling:
```html
<button onclick="handleClick()">Click Me</button>
```

### React Event Handling:
```jsx
<button onClick={handleClick}>Click Me</button>
```

### Key Differences:
- **camelCase** naming (`onClick` not `onclick`)
- **Function reference** not string (`{handleClick}` not `"handleClick()"`)
- **Curly braces** around the function name

---

# Common React Events

| Event | When it triggers | Example |
|-------|------------------|---------|
| `onClick` | Element is clicked | Button clicks |
| `onChange` | Input value changes | Typing in text field |
| `onSubmit` | Form is submitted | Form submission |
| `onMouseEnter` | Mouse enters element | Hover effects |
| `onMouseLeave` | Mouse leaves element | Hover effects |

---

# Writing Event Handler Functions

```jsx
function MyComponent() {
  function handleClick() {
    console.log('Button was clicked!');
  }
  
  return <button onClick={handleClick}>Click Me</button>;
}
```

---

# Event Handler with Parameters

```jsx
function TaskList() {
  const tasks = ['Task 1', 'Task 2', 'Task 3'];
  
  function handleDelete(taskIndex) {
    console.log(`Deleting task at index: ${taskIndex}`);
  }
  return (
    <ul>
      {tasks.map((task, index) => (
        <li key={index}>
          {task}
          <button onClick={() => handleDelete(index)}> Delete </button>
        </li>
      ))}
    </ul>
  );
}
```

---

# Input Event Handling

### Handling text input changes:
```jsx
function TextInput() {
  function handleChange(event) {
    console.log('Input value:', event.target.value);
  }
  
  return (
    <input 
      type="text" 
      onChange={handleChange}
      placeholder="Type something..."
    />
  );
}
```

---

# Form Event Handling

### Handling form submission:
```jsx
function ContactForm() {
  function handleSubmit(event) {
    event.preventDefault(); // Prevents page refresh
    console.log('Form submitted!');
  }
  return (
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="Your name" />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### `event.preventDefault()` stops the default form behavior
---
# 5.9 State

---

# What is State?

**State** is data that can change over time in a React component
<div class="two-column-slide">
      <div class="column-left">

### Key Characteristics:
- **Mutable** - can be updated
- **Component-specific** - belongs to one component
- **Triggers re-renders** - when state changes, component re-renders
- **Persistent** - survives re-renders
</div>
<div class="column-right">

### Examples of State:
- Counter value
- User input text
- List of items
- Toggle visibility
</div>
</div>

---

# State vs Props

| **State** | **Props** |
|-----------|-----------|
| Internal to component | Passed from parent |
| Can be changed | Read-only |
| Managed with `useState` | Passed as attributes |
| Triggers re-render | Triggers re-render |

---

# State vs Props
### Example:
```jsx
function Counter({ initialValue }) { // props
  const [count, setCount] = useState(initialValue); // state
  return <div>{count}</div>;
}
```

---

# Using useState Hook

### Import useState:
```jsx
import { useState } from 'react';
```

### Basic Syntax:
```jsx
function MyComponent() {
  const [stateVariable, setStateFunction] = useState(initialValue);
  
  return <div>{stateVariable}</div>;
}
```
---

# Using useState Hook
### Example:
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <div>Count: {count}</div>;
}
```

### What each part means:
- `count` - **state variable** (current value)
- `setCount` - **setter function** (updates the state)
- `useState(0)` - **initial value** (starts at 0)
- `[count, setCount]` - **array destructuring**

---

# Using useState Hook
### Example:
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <div>Count: {count}</div>;
}
```
### Naming Convention:
- State variable: `count`, `name`, `items`
- Setter function: `setCount`, `setName`, `setItems`

---

# Updating State

### Correct way to update state:
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  
  function increment() {
    setCount(count + 1); // Correct
  }
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>+1</button>
    </div>
  );
}
```

---

# Updating State
### Wrong way:
```jsx
function increment() {
  count = count + 1; // Wrong! Don't modify state directly
}
```

---

# State with Different Data Types

### String State:
```jsx
const [name, setName] = useState('');
setName('John');
```

### Number State:
```jsx
const [age, setAge] = useState(0);
setAge(25);
```
---

# State with Different Data Types

### Boolean State:
```jsx
const [isVisible, setIsVisible] = useState(false);
setIsVisible(true);
```

### Array State:
```jsx
const [items, setItems] = useState([]);
setItems(['item1', 'item2']);
```

---

# State with Objects

### Object State:
```jsx
const [user, setUser] = useState({ name: '', email: '' });

// Update entire object
setUser({ name: 'John', email: 'john@example.com' });

// Update specific property
setUser({ ...user, name: 'Jane' });
```

---

# State with Objects
### Array of Objects:
```jsx
const [tasks, setTasks] = useState([
  { id: 1, text: 'Learn React', completed: false },
  { id: 2, text: 'Build app', completed: false }
]);
```

---

# Adding Items to Array State

### Adding to array:
```jsx
function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [inputValue, setInputValue] = useState('');
  
  function addTodo() {
    const newTodo = { id: Date.now(), text: inputValue, completed: false };
    setTodos([...todos, newTodo]);
    setInputValue(''); // Clear input
  }
  
  return (<div>
      <input value={inputValue} onChange={(e) => setInputValue(e.target.value)} />
      <button onClick={addTodo}>Add Todo</button>
    </div>);
}
```

---

# Removing Items from Array State

### Remove by ID:
```jsx
function removeTodo(id) {
  setTodos(todos.filter(todo => todo.id !== id));
}
```

### Remove all items:
```jsx
function clearAll() {
  setTodos([]);
}
```
---

# Updating Items in Array State
### Update specific item:
```jsx
function toggleComplete(id) {
  setTodos(todos.map(todo => 
    todo.id === id 
      ? { ...todo, completed: !todo.completed }
      : todo
  ));
}
```


---

# State Best Practices

### 1. Don't mutate state directly:
```jsx
todos.push(newTodo); // Wrong
setTodos(todos); // Wrong

setTodos([...todos, newTodo]); // Correct
```

### 2. Keep state minimal:
```jsx
// Too many states
const [firstName, setFirstName] = useState('');
const [lastName, setLastName] = useState('');

// Better state
const [name, setName] = useState({ first: '', last: '' });
```

---

# Common State Patterns

### Toggle Pattern:
```jsx
const [isVisible, setIsVisible] = useState(false);

function toggle() {
  setIsVisible(!isVisible);
}
```

### Counter Pattern:
```jsx
const [count, setCount] = useState(0);

function increment() { setCount(count + 1); }
function decrement() { setCount(count - 1); }
function reset() { setCount(0); }
```
---

# Common State Patterns
### Form Pattern:
```jsx
const [formData, setFormData] = useState({ name: '', email: '' });

function handleChange(field, value) {
  setFormData({ ...formData, [field]: value });
}
```

---

<!-- _class: demo -->

>30m
# Demo
5.4 More React

---

# Next Class

- More on React