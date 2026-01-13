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
    section.demo { background: var(--sedondary); color:var(--foreground)}
    section.demo h1,section.demo h2, section.demo h3, section.demo h4, section.demo h5 { color: var(--foreground) }
    section.demo footer { display: none; }
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
footer: 'SWE 363 | 252 | KFUPM'
---

<!-- 

# Goals 

By the end of this lecture students will:

1. Be motivated to take the course 
2. Have a clear expectations about the course 
3. Have a birdeye view of the core concepts 
4. Practiced setting up an building a fullstack web app

# Agenda (11-12:15)

- Getting to know each other (15m)
- Slides (15m): 
-- What is course about? 
-- History of the web <<NEEDS READING>>
-- HTML, CSS & JS <<NEEDS READING>>
- Demo: Building a Full stack app (15m)
- Hands-on: Building a full stack app (30m)

-->

<!-- 
Assalamu Alaykom All
Thank you for beign here today 
 -->



# Web Engineering & Development (SWE 363) 


 ---

 <!-- 
Before we start let's get to know you ..
 -->

<!-- _class: activity -->


> Activity
# Knowing each other 
- Name, Major 
- What is something interesting about you? 

---
<!-- _class: light -->

# Course Repository
[https://github.com/Web-Engineering-KFUPM/web_course_main](https://github.com/Web-Engineering-KFUPM/web_course_main)    

---

<!-- These are the course learning outcomes .. -->

# Course Learning Outcomes:
By the end of this course you will be able to :

1. Identify candidate **tools and technologies** for developing web applications.
2. Recognize the **social impact and professional** responsibility towards web applications.
3. Conceptualize and recognize **design principles** in building front-end and back-end web applications.
4. **Build and publish** cross-platform, data-driven, and dynamic web applications.
5. Incorporate best practices to boost the **sustainability, usability, and accessibility** of web applications.

---
# Web development tools and technologies to explore

- Browser (e.g., [Chrome](https://www.google.com/chrome/), [Firefox](https://www.mozilla.org/en-US/firefox/new/), [Safari](https://www.apple.com/safari/), etc.)
- Revision control with Git (e.g., [Git](https://git-scm.com/), [GitHub](https://github.com/), [GitLab](https://gitlab.com/), etc.)
- Integrated Development Environment (IDE) (e.g., [Visual Studio Code](https://code.visualstudio.com/), [WebStorm](https://www.jetbrains.com/webstorm/), [cursor](https://www.cursor.com/), etc.)
- Front-end development (e.g., [HTML](https://www.w3schools.com/html/), [CSS](https://www.w3schools.com/css/), [JavaScript](https://www.w3schools.com/js/), [React](https://react.dev/), etc.)
- Back-end development (e.g., [Node.js](https://nodejs.org/en/), [Express](https://expressjs.com/), etc.)
- Database (e.g., [MongoDB](https://www.mongodb.com/) etc.)

---

<!-- _class: activity -->

> Activty

## github.com/Web-Engineering-KFUPM/web_course_main
- visit the link
- Star the repository
- Explore the repository 
- Read the syllabus 
- Ask questions 

