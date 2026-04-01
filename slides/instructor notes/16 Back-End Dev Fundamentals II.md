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
- Node.js
- Modules

### Reference: 
- Zybook: 6.2-6.3
---
# 6.2 Node.js

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

# What Can Node.js Do?

- Run JavaScript on **command line** (CLI tools)
- Build **web servers** and APIs
- Read/write **files** on the server
- Connect to **databases**
- Handle **server requests** and responses

---

# Installing Node.js

**Download from:** [nodejs.org](https://nodejs.org/)

**Verify installation:**
```bash
node -v
npm -v
```

**macOS:** Use Homebrew or download installer  
**Windows:** Download and run installer

---

# Running Node.js

**Run a JavaScript file:**
```bash
node filename.js
```

**Example:**
```bash
node calculator.js
```

**Run JavaScript interactively:**
```bash
node
> console.log("Hello Node.js!")
Hello Node.js!
```

---

# What is npm?

> **npm** (Node Package Manager) is the default package manager for Node.js

**npm allows you to:**
- Install third-party packages
- Manage project dependencies
- Initialize new projects
- Run scripts

**npm comes with Node.js** - no separate installation needed!

---

# npm vs Node.js

<div class="two-column-slide">

<div class="column-left">

## Node.js
- JavaScript **runtime**
- Runs JavaScript code
- Command: `node`

</div>

<div class="column-right">

## npm
- Package **manager**
- Installs packages
- Command: `npm`

</div>

</div>

---

# Initiating a Project with npm

**Create a new project:**
```bash
npm init
```
Interactive prompts for project details

**Quick start (skip prompts):**
```bash
npm init -y
```
Creates `package.json` with default values

---

# What is package.json?

**package.json** is a configuration file that:
- Defines project metadata (name, version, description)
- Lists project dependencies
- Contains project scripts

---
# What is package.json?

**package.json** is a configuration 
**Example:**
```json
{
  "name": "calculator",
  "version": "1.0.0",
  "description": "CLI calculator",
  "main": "calculator.js",
  "scripts": {
    "test": "echo \"Error: no test specified\""
  },
  "dependencies": {
    "lodash": "^4.17.21"
  }
}
```

---

# Installing npm Packages

**Install a package:**
```bash
npm install package-name
# or
npm i package-name
```

**Install as dependency:**
```bash
npm install --save package-name
```

**Install as development dependency:**
```bash
npm install --save-dev package-name
```

---

# Viewing Installed Packages

**List installed packages:**
```bash
npm list
```

**Check specific package:**
```bash
npm list lodash
```

**View package.json dependencies:**
```bash
cat package.json
```

---

# package-lock.json

**package-lock.json:**
- Records **exact versions** of installed packages
- Ensures **consistent installs** across machines
- **Automatically generated** - don't edit manually!

**Why it matters:**
- Team members get same versions
- Production deployments are predictable

---

# Using Third-Party Packages

**Import a package:**
```js
import packageName from "package-name";
```

**Example with lodash:**
```js
import _ from "lodash";

const numbers = [1, 2, 3, 4, 5];
const sum = _.sum(numbers); // 15
```

**Use package functions:**
```js
packageName.function();
```

---

# Command Line Arguments

Node.js provides access to command-line arguments through `process.argv`

**process.argv is an array:**
- `process.argv[0]` = path to Node.js
- `process.argv[1]` = path to your script
- `process.argv[2+]` = your arguments

---

# Command Line Arguments Example

**Run:**
```bash
node script.js add 5 10
```

**In script.js:**
```js
const operation = process.argv[2]; // "add"
const num1 = process.argv[3];      // "5"
const num2 = process.argv[4];      // "10"
```

**Note:** All arguments are **strings** - convert to numbers if needed!

---

# Command Line Arguments Practice

**What would this code output?**

```js
console.log(process.argv[0]);
console.log(process.argv[1]);
console.log(process.argv[2]);
```

**When run as:**
```bash
node test.js hello
```

---

<!-- _class: center -->

# 6.3 Modules

---

# What Are Modules?

> **Modules** allow breaking code into smaller, reusable files

**Why use modules?**
- **Organization** - code is easier to find
- **Reusability** - write once, use many times
- **Maintainability** - easier to update and debug
- **Separation of concerns** - each file has a purpose

---

# Module Example

**Instead of one big file:**
```
calculator.js (500 lines)
```

**Use modules:**
```
calculator.js (main logic)
utils/
  ├── operations.js (math functions)
  └── parser.js (input parsing)
```

**Much easier to understand!**

---

# Two Module Formats

<div class="two-column-slide">

<div class="column-left">

## ES Modules (ESM)
- Modern format
- Uses `import` / `export`
- Supported by modern Node.js

</div>

<div class="column-right">

## CommonJS
- Traditional format
- Uses `require()` / `module.exports`
- Older Node.js style

</div>

</div>

**We'll focus on ES Modules!**

---

# Exporting from a Module

**Export a single function:**
```js
// operations.js
export function add(numbers) {
  return numbers.reduce((sum, num) => sum + num, 0);
}
```

**Export multiple functions:**
```js
export function add(numbers) { ... }
export function subtract(numbers) { ... }
export function multiply(numbers) { ... }
```

---

# Importing from a Module

**Import a single function:**
```js
import { add } from "./utils/operations.js";
```

**Import multiple functions:**
```js
import { add, subtract, multiply } from "./utils/operations.js";
```

**Import default export:**
```js
import lodash from "lodash";
```

---

# Import/Export Example

**utils/operations.js:**
```js
export function add(numbers) {
  return numbers.reduce((sum, num) => sum + num, 0);
}

export function subtract(numbers) {
  return numbers[0] - numbers.slice(1)
    .reduce((diff, num) => diff - num, 0);
}
```

**calculator.js:**
```js
import { add, subtract } from "./utils/operations.js";

const result = add([5, 10, 15]); // 30
```

---

# File Extensions Matter

**Always include `.js` extension:**
```js
import { add } from "./utils/operations.js";  //correct
import { add } from "./utils/operations";    //Incorrect
```

**Why?**
- ES Modules require explicit file extensions
- Helps Node.js find the correct file

---

# Module Paths

**Relative path (same folder):**
```js
import { func } from "./file.js";
```

**Relative path (parent folder):**
```js
import { func } from "../utils/file.js";
```

**Absolute path (node_modules):**
```js
import _ from "lodash";
```

---

# Creating a Custom Module

**Step 1: Create the module file**
```js
// utils/parser.js
import _ from "lodash";

export function parseNumbers(input) {
  const numbers = _.map(input, (str) => Number(str));
  return _.compact(numbers);
}
```

**Step 2: Import and use**
```js
// calculator.js
import { parseNumbers } from "./utils/parser.js";

const nums = parseNumbers(["5", "10", "15"]);
```

---

# Module Best Practices

**One responsibility per module:**
- `operations.js` → math operations only
- `parser.js` → input parsing only
- `validator.js` → validation only

**Clear file names:**
- `utils/operations.js` 

**Organize in folders:**
- `utils/` for utility functions
- `models/` for data models


---

<!-- _class: demo -->

>30m
# Demo
6.2 Introduction to Node

**Build a CLI calculator using:**
- Node.js command line arguments
- npm packages (lodash)
- Custom modules

---

# Next Class

- Express.js
- Building web servers