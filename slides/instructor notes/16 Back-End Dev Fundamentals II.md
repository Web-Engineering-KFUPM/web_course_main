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
# Back-end Development Fundamentals II

---

# In today's lecture:
- Node.js
- npm
- Modules

### Reference: 
- Zybook: 6.2-6.3
---
# 6.2 Node.js

<!-- Timing: ~22 min for 6.2 (including activities) -->

---

# What is Node.js?

> **Node.js** is a JavaScript runtime environment, mainly used to run **server-side** web applications

- **Event-driven, non-blocking I/O** → handles high loads
- **JavaScript** on both the server and the client
- Simple way to create and share **modules**
- Works well with **MongoDB** and **JSON**

**Used by:** Netflix, Walmart, eBay, LinkedIn

---

# Running Node.js

<div class="two-column-slide">

<div class="column-left">

**Interactive shell**
```bash
$ node
> console.log("Hello, Node.js!")
Hello, Node.js!
undefined
> x = 2
2
> .exit
```

</div>

<div class="column-right">

**Run a file**
```js
// hello.js
for (let i = 0; i < 3; i++) {
  console.log("Hello, Node.js!");
}
```
```bash
$ node hello.js
```

</div>

</div>

---

<!-- _class: activity -->

> Activity: Predict the output

1. What does the shell display?
```bash
$ node
> console.log("Hi")
> x = 5
> .exit
```

2. True or False: `node test.js` starts the interactive shell.

3. True or False: Node.js programs run in the web browser.

<!--
Answers:
1. Hi, then undefined (as in the zyBooks shell example); then 5; then the shell exits.
2. False: it runs the program in test.js.
3. False: Node.js programs run on the server (or on the command line).
-->

---

# A Simple Web Server: the `http` Module

```js
// server.js
const http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/html"});
  response.write("<h1>Hello, Node.js!</h1>");
  response.end();
}).listen(3000);
```

- `require()` → imports a module (CommonJS)
- `createServer()` → creates the server; the callback runs on each HTTP request
- `writeHead()` → sets the **status code** and content type
- `write()` / `end()` → writes the HTML / **sends** the response
- `listen(3000)` → starts listening → `http://localhost:3000/` (stop with **Ctrl+C**)

---

# npm & Node.js Projects

- **Project** → a directory of JavaScript files, packages, and configuration files
- **Package** → a directory with one or more modules + a `package.json` file
- **npm** (Node Package Manager) → downloads, installs, and updates packages
  - Installed with Node.js: `npm -v`

```
myproject
├── node_modules
│   └── underscore
├── package.json
├── package-lock.json
└── server.js
```

---

# Local vs. Global Install

<div class="two-column-slide">

<div class="column-left">

## Local (default)
```bash
npm install underscore
```
- Saved in the project's `node_modules`
- For **project dependencies**

</div>

<div class="column-right">

## Global (`-g`)
```bash
npm install nodemon --global
```
- Saved in `{prefix}/node_modules`
- For **command-line tools**

</div>

</div>

**Dependency** = a package the project must be able to access to run

`nodemon server.js` → restarts the app whenever project files change

---

# Common npm Commands

| Command | Example |
|---------|---------|
| Install a package locally / globally | `npm install lodash` / `npm install nodemon -g` |
| Install **all** project dependencies | `npm install` |
| List local / global packages | `npm list` / `npm list -g` |
| Update a package | `npm update lodash` |
| Uninstall a package | `npm uninstall lodash` |
| Show the global install location | `npm config get prefix` |

---

# package.json

```json
{
  "name": "my-web-server",
  "version": "1.0.0",
  "description": "A simple web server",
  "main": "server.js",
  "dependencies": { "underscore": "^1.13.6" },
  "scripts": { "start": "node server.js" },
  "license": "ISC"
}
```

- Lists the project's name, version, license, and **dependencies**
- Create it by hand or with `npm init`
- `npm install` → installs **all** dependencies listed
- `"start"` script → `npm start` runs `node server.js`

---

# Versions & package-lock.json

**Semantic versioning:** `major.minor.patch` → `1.9.1`
- **major** → new functionality; may change how old functions work
- **minor** → bug fixes and minor changes
- **patch** → a bug fix to a minor version

`"^1.9.1"` → highest version with major number **1** (1.9.2 yes, 2.0.0 no)

**package-lock.json** → records the **exact** versions to use
- The same versions on every machine
- Created or modified when dependencies are added or removed

---

<!-- _class: activity -->

> Activity: Answer the following questions

1. In the `http` server, which method starts listening for requests: `require()`, `createServer()`, or `listen()`?

2. What URL accesses a web server running locally on port 8080?

3. Where does `npm install grunt -g` install the package?

4. `"lodash": "^4.17.0"`, and versions `4.17.21`, `4.18.0`, `5.0.0` exist. With no package-lock.json, which is installed?

5. A project has package.json but no `node_modules`. What single command installs everything?

<!--
Answers:
1. listen()
2. http://localhost:8080/
3. {prefix}/node_modules (find {prefix} with npm config get prefix)
4. 4.18.0: the highest version with major number 4.
5. npm install
-->

---

# Using a Third-Party Package

```bash
npm install underscore
```

```js
const _ = require("underscore");   // underscore is usually named _

// Use underscore to get a random number between 1 and 6
let randNum = _.random(1, 6);
```

- The module is stored in `node_modules/underscore`
- Good practice: name the variable after the module (`http` for "http")

---

<!-- _class: activity -->

> Activity: Predict

```js
const http = require("http");
const _ = require("underscore");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/html"});
  for (let i = 0; i < 5; i++) {
    let randNum = _.random(1, 6);
    response.write("<p>" + randNum + "</p>");
  }
  response.end();
}).listen(3000);
```

1. How many numbers does `http://localhost:3000/` show? In what range?
2. What happens when you refresh the page?
3. What happens if `npm install underscore` was never run?

<!--
Answers:
1. 5 numbers, each between 1 and 6 (a dice roll).
2. New random numbers: the callback runs again for every request.
3. require("underscore") fails: the package isn't in node_modules.
-->

---

<!-- _class: center -->

# 6.3 Modules

<!-- Timing: ~12 min for 6.3 (including activities) -->

---

# Why Modules?

<div class="two-column-slide">

<div class="column-left">

## Separate files
```js
// flights.js
const max = 10;
function purchaseTicket() { ... }

// hotels.js
const max = 10;   // Error: max conflicts
function bookRoom() { ... }
```
```html
<script src="flights.js"></script>
<script src="hotels.js"></script>
```

</div>

<div class="column-right">

## Separate modules
```js
// flights.js
const max = 10;
function purchaseTicket() { ... }
export { purchaseTicket };

// hotels.js
const max = 10;   // no error
function bookRoom() { ... }
export { bookRoom };
```
You control **what is exported**

</div>

</div>

---

# Two Module Formats

<div class="two-column-slide">

<div class="column-left">

## ES Modules
- Supported by all major browsers
- `import` / `export`

```js
import { bookRoom } from "./hotels.js";
```

</div>

<div class="column-right">

## CommonJS
- Commonly used in Node.js
- `require()`

```js
const http = require("http");
```

</div>

</div>

**This section covers ES modules**

---

# Exporting

<div class="two-column-slide">

<div class="column-left">

## Named exports (many)
```js
// hello.js
function sayHello() { alert("Hello!"); }
function sayHi() { alert("Hi!"); }

export { sayHello, sayHi };
```
or before each declaration:
```js
export function sayHello() { ... }
```

</div>

<div class="column-right">

## Default export (one)
```js
// goodbye.js
function sayGoodbye() { alert("Goodbye!"); }

export default sayGoodbye;
```
or before the declaration:
```js
export default function sayGoodbye() { ... }
```

</div>

</div>

---

# Importing

```js
import { sayHello, sayHi } from "./hello.js";   // non-default → braces
import sayGoodbye from "./goodbye.js";          // default → no braces
```

- `"./"` → the file is in the **same directory**

**In a webpage:**
```html
<script type="module">
  import { sayHello, sayHi } from "./hello.js";
  sayHello();
</script>
```

- `type="module"` is **required** for `import` to work
- Files must be on a **web server** (not opened with `file://`)

---

<!-- _class: activity -->

> Activity: What happens if (each change on its own)

```js
// hello.js                          // index.html
export { sayHello, sayHi };          <script type="module">
                                       import { sayHello, sayHi } from "./hello.js";
// goodbye.js                          import sayGoodbye from "./goodbye.js";
export default sayGoodbye;             sayHello(); sayHi(); sayGoodbye();
                                     </script>
```

1. The call `sayHi();` is removed from index.html?
2. `sayHi` is removed from the export in hello.js?
3. `type="module"` is removed from the `<script>` tag?
4. The import uses `"hello.js"` instead of `"./hello.js"`?
5. `export default function sayAdios() {...}` is added to goodbye.js?

<!--
Answers:
1. Runs without errors.
2. Error when importing sayHi: it is not exported.
3. Error when executing the hello.js import statement.
4. Error when executing the hello.js import statement.
5. Error: a module can only have one default export.
-->

---

<!-- _class: activity -->

> Activity: Find the 3 bugs

```js
// hello.js
function sayHello() { alert("Hello!"); }

// goodbye.js
export default function sayGoodbye() { alert("Goodbye!"); }
export default function sayAdios() { alert("Adios!"); }
```

```html
<script type="module">
  import { sayHello } from "./hello.js";
  import { sayGoodbye } from "./goodbye.js";
  sayHello();
  sayGoodbye();
</script>
```

<!--
Answers:
1. hello.js doesn't export sayHello → add export { sayHello };
2. goodbye.js has two default exports → only one is allowed.
3. sayGoodbye is a default export → import it without braces: import sayGoodbye from "./goodbye.js";
-->

---

# Key Takeaways

- **Node.js** runs JavaScript on the server: `node file.js`
- The **http** module: `createServer()`, `writeHead()`, `end()`, `listen()`
- **npm** installs packages locally (`node_modules`) or globally (`-g`)
- **package.json** = dependency ranges; **package-lock.json** = exact versions
- **Modules:** named exports `{ }` or one default export; local paths start with `./`

---

<!-- _class: demo -->

>30m
# Demo
6.2 Introduction to Node

**Build a CLI calculator using:**
- npm packages
- Custom modules

<!--
Setup: npm init -y; npm install lodash; add "type": "module" to package.json (avoids Node's module-type warning).
Test: node calculator.js add 5 10 15 → Result: 30
Not in zyBooks ch6 (calculator.js and the README explain them):
- process.argv (command-line arguments; all values are strings)
- lodash functions _.map, _.compact, _.includes (zyBooks uses underscore)
- import _ from "lodash" (importing an npm package with ES module syntax)
- npm init -y and "type": "module"
-->

---

# Next Class

- Express.js
- Building web servers
