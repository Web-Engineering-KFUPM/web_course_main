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
- Midterm Exam 
  - Date: Nov 4th
  - Time: 6:00-7:30 (pm)
  - Location: B22 (Rooms TBA)
- Command to get admin access in the lab PCs
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```
---

# In today's lecture:

- Conditional Rendering
- Lists (React)

### Reference: 
- Zybook: 5.10-5.11

---
# 5.10 Conditional Rendering

---

# What is Conditional Rendering? 

**Conditional rendering** means showing or hiding parts of the UI depending on certain conditions.


### Real-world examples:
- Show "Login" button when user is logged out
- Display "Loading..." while data is being fetched
- Show "No tasks yet" when a list is empty
- Hide error messages when there are no errors

---

# Why is Conditional Rendering Useful? 

- **Dynamic content** that reacts to data changes
- **Better user experience** by showing relevant information
- **Cleaner UI** by avoiding unnecessary clutter

---

# Three Ways to Do Conditional Rendering

## 1. **if Statements** 
```jsx
function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  } else {
    return <h1>Please log in.</h1>;
  }
}
```
---

# Three Ways to Do Conditional Rendering
## 2. **Ternary Operator** 
```jsx
{isLoading ? <Spinner /> : <DataList />}
```

## 3. **Logical AND** 
```jsx
{error && <div className="error">{error}</div>}
```

---

# Conditional Rendering: if Statements

### When to use:
- **Complex logic** that's hard to read inline
- **Multiple conditions** to check
- **Different components** to return entirely


---

# Conditional Rendering: Ternary Operator

### When to use:
- **Simple true/false** conditions
- **Two different elements** to show
- **Inline rendering** within JSX

### Syntax:
```jsx
condition ? trueValue : falseValue
```

---

# Conditional Rendering: Logical AND

### When to use:
- **Show/hide** a single element
- **Simple conditions** that are either true or false
- **Optional content** that only appears when needed

### Syntax:
```jsx
condition && <Element />
```

---

# Common Conditional Rendering Patterns

## Pattern 1: Empty State
```jsx
if(tasks.length === 0) {
  return <p>No tasks yet. Add your first one!</p>
} else {
  return <ul>
    {tasks.map(task => <TaskItem key={task.id} task={task} />)}
  </ul>
}
```
---

# Common Conditional Rendering Patterns
## Pattern 2: Loading State
```jsx
{isLoading ?
  return <div>Loading...</div>
} else {
  return <DataComponent data={data} />
}
```

## Pattern 3: Error Handling
```jsx
{error && <ErrorMessage error={error} />}
{!error && <MainContent />}
```

---

# 5.11 Lists

---

# Lists in React - What are Lists in React?

**Lists** are collections of similar items displayed dynamically.

### Real-world examples:
- Shopping cart items
- User comments on a post
- Todo tasks
- Product catalog
- Search results

---

# Lists in React - How to render Lists in React?
### Use `.map()`
- **Dynamic rendering** based on data
- **Automatic updates** when data changes
- **Reusable components** for each item
- **Clean, declarative code**

---

# Lists in React - How to render Lists in React?

### Basic Syntax:
```jsx
{items.map(item => (
  <Component key={item.id} data={item} />
))}
```

### Step-by-step:
1. **Start with an array** of data
2. **Use `.map()`** to transform each item
3. **Return JSX** for each item
4. **Add a unique `key`** prop

---

# The Importance of Keys

### What are keys?
**Keys** are unique identifiers that help React track which items have changed, been added, or removed.

### Why are they important?
- **Performance**: React can efficiently update only changed items
- **State preservation**: Form inputs keep their values
- **Animation**: Smooth transitions between states
- **Prevents bugs**: Avoids UI glitches

---

# Key Best Practices

### Good Keys:
```jsx
// Use unique, stable IDs
{users.map(user => (
  <UserCard key={user.id} user={user} />
))}

// Use unique properties
{products.map(product => (
  <ProductCard key={product.sku} product={product} />
))}
```
---

# Key Best Practices
### Bad Keys:
```jsx
// Don't use array index for dynamic lists
{tasks.map((task, index) => (
  <TaskItem key={index} task={task} />  // X Bad!
))}

// Don't use random values
{tasks.map(task => (
  <TaskItem key={Math.random()} task={task} />  // X Bad!
))}
```

---

# When Index is OK for Keys

### Safe to use index when:
- **List never reorders** (items stay in same position)
- **Items are never added/removed** from middle
- **Simple, static lists**

### Example:
```jsx
// Static menu items - order never changes
const menuItems = ['Home', 'About', 'Contact'];

{menuItems.map((item, index) => (
  <MenuItem key={index} text={item} />
))}
```
---


<!-- _class: demo -->

>30m
# Demo
Starter code at: https://classroom.github.com/a/4OG8kbSm

---

# Next Class

- More on React