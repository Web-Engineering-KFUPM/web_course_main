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
    section.center {text-align:center}
    section.big-code pre {font-size:2rem}
footer: 'SWE 363 | 251 | Sec F04 | KFUPM'
---

Web Engineering & Development (SWE 363) 
# 3.1 Intro to CSS
### Created by: Dr. Omar Hammad
### Lectured by: Dr. Khadijah Al Safwan

---

 Announcements 📣
 - Reminder of the projects submissions 
 - SWE 363 Midterm date: Tuesday, November 4th
 - Github submission issues - useage of templates forks 

 ---

 # In today's Lecture: 

 - Intro to CSS 
 - Basic Selectors 
 - Review project ideas

Reference: 
- Zybook: 3.1 to 3.3

---

<!-- Goals of lecture:

- show them one website with multiple stylesheets 
- explain the idea of CSS
- where to put it ? inline, internal, external

 -->

# https://www.apple.com/
# https://htmlcheatsheet.com/css/

---

# CSS Rule
<!-- _class: big-code center-->
```
p { color: red };
```

---

## More rules
```
p { 
    color: crimson; 
    font-size: 16px; 
    line-height: 1.5;
}
h1 { 
    color: navy; 
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 2px;
}
ul { 
    color: forestgreen; 
    font-weight: normal;
    list-style-type: square;
}
```

---

<!-- _class: boxes -->

# Where to put it ?
```
<!-- inline -->
<p style="color: red; font-size: 16px;">This is a paragraph</p>
```

```
<!-- internal -->
<style>
    p { color: red; font-size: 16px; }
</style>
```

```
<!-- external -->
<link rel="stylesheet" href="styles.css">

```

---

<!-- _class: center-->

# Who wins?

---

<!-- _class: center-->

### who wins?
# The more specific wins

---

<!-- _class: activity -->

>Activity: What will the color of each sentence be?

```html
<style>
p    { color:orange; }
span { color:green; }
</style>

<p>
    Part of this sentence is orange,
    <span>while the rest is green.</span>
</p>

<p>
    Part of this sentence is orange,
    <span style="color:blue">while the rest is blue.</span>
</p>

<p style="color:red">
    This sentence is red.
</p>
```     

---

# But !important overrides everything

```
<style>
p    { color:orange !important; }
span { color:green; }
</style>
<p style="color:red">
    This sentence was red. But orange overrides it.
</p>
```

---



# How can we select elements?
analyze the following code and tell what is the selection pattern

- tag: p, span, h1, div
- id: #main
- class: .highlight
- group: p, span, h1, div
- universal: *

---

<!-- _class: activity -->

> Activity: Analyze the following code and tell what is the selection pattern


```css
<style>
    #main { color: red; }
    .highlight { color: blue; }
    p { color: green; }
    span { color: yellow; }
    h1 { color: purple; }
    div { color: orange; }
    * { color: black; }
    p, span, h1, div { color: brown; }
</style>
```
```html
<div>
<h1 id="main">This is a heading</h1>
<p>This is a paragraph</p>
<p class="highlight">This is a highlighted paragraph</p>
<h2 class="highlight">This is a highlighted paragraph</p>
</div>
```

---

# A bit advanced selectors
decendant, psudo-class

- decendant: ```p span``` 
- psudo-class: ```:hover```

---

<!-- _class: activity -->

> Activity: Analyze the following code and tell what is the selection pattern

```css
<style>
    p { color: blue; }
    p span { color: red; }
    button:hover { color: green; }
</style>
```
```html
<div>
    <span>there</span>
</div>
<p>
    Hello <span>there</span>
</p>
<button>Click me</button>
```

---

<!-- _class: demo -->
>30m
# Let's practice CSS selectors

Starter code at: https://github.com/Web-Engineering-KFUPM/web-engineering-kfupm-classroom-3-1-css-basics-3.1-css-basics
https://classroom.github.com/a/AmqNvXqN

---

# Next Class
- Common properties
- Fonts 
- Box Model
- Flexbox

