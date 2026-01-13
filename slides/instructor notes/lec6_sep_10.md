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

<!-- 

Todays goals: 

 - Explain CSS properties: Color, Font, Box model, Flexbox, Positioning

 -->


Web Engineering & Development (SWE 363) 
# 3.2 CSS Properties
### Created by: Dr. Omar Hammad and Dr. Khadijah Al Safwan

---

# Announcements 📣
- Phase 2 added 
- Grading started 

---

# In today's Lecture: 

- Font: size, weight, family
- Text: alignment, decoration, transform
- Color: background, text 
- Display: block, inline, inline-block
- Box model: border, padding, margin
- Flexbox: display, flex-direction, justify-content, align-items
- Positioning: static, relative, absolute, fixed, z-index

### Reference: 
- Zybook: 3.4 to 3.8

---

# Inspirational Websites
https://www.awwwards.com/
https://www.producthunt.com/
https://www.raycast.com

---

# RGB vs HEX 
 <!-- Hue, Saturation, and Lightness -->
 <!-- Hue, Whiteness, and Blackness -->
 <img src="color.png" alt="Color" width="500">
 
 [HTML Color Codes](https://htmlcolorcodes.com/)

---

# Box model 
<img src="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_box_model/boxmodel.png" alt="Box model Image" width="500">

[The Box Model Game](https://preview.webflow.com/preview/the-box-model-game-ca6721?utm_medium=preview_link&utm_source=designer&utm_content=the-box-model-game-ca6721&preview=3e6d150df85e31264571f886d38b8468&workflow=)

---

# Flexbox 
<img src="https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Flexbox/flex_terms.png" alt="Flexbox Image" width="500">

[The Flexbox Game](https://preview.webflow.com/preview/flexbox-game?utm_medium=preview_link&utm_source=designer&utm_content=flexbox-game&preview=d1a26b027c4803817087a91c651e321f&workflow)

[Flexbox Froggy Game](https://flexboxfroggy.com/)


---
# Positioning 
<img src="https://www.csssolid.com/images/csspositions/css-position-all.png" alt="Positioning" width="500">

---
<!-- _class: demo -->

>30m
# Demo
Starter code at: web-engineering-kfupm-classroom-3-2-css-properties/

---

# Next Class
- JS