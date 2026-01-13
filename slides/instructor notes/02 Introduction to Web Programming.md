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

Web Engineering & Development (SWE 363) 
# Introduction to Web Development  


---


# Announcements 📣

- Clone the course repository from [GitHub](https://github.com/Web-Engineering-KFUPM/web_course_main)
- Join Blackboard Common section 
- Start looking for a project team (3-4 students)


---

# Today's plan: 

We will get to know the web, explore the journey of an HTTP request, and build a simple web application.

- The world wide web (WWW)
- Infrastructure of the web
- HTTP Requests and Responses
- IP addresses
- DNS (Domain names system)
- URLs (Uniform Resource Locator)
- intro to HTML, CSS & JS


---


<!-- So what is the web? or the world wide web -->

So .. 
# What is the web?
*aka World Wide Web or WWW*


---

<!-- _class: light -->

# The web 
*A vast network of interconnected documents and resources, accessible via the **internet**, that allows users to share and access information globally.*
![bg right](./web3.png)

---

<!-- Ok what technologies make the web possible? -->

# What technologies makes the web possible?

---

<!-- _class: boxes -->
 

# What technologies makes the web possible?
- Internet
- HTTP 
- Servers 
- Clients 
- HTML 
- URLs

<!--  

---

Internet: A global network of interconnected computers that communicate using standardized protocols.
// 
HTTP: Hypertext Transfer Protocol, the foundation of data communication on the web, used for transmitting web pages.
// 
Servers: Computers or systems that provide resources, data, services, or programs to other computers, known as clients, over a network.
// 
Clients: Devices or programs that request and use resources or services from a server.
// 
HTML: Hypertext Markup Language, the standard language for creating and designing web pages and web applications.
// 
URLs: Uniform Resource Locators, the addresses used to access resources on the internet. 

---

-->

---

<!-- This is a simple architecture of the web -->

# What makes a web application?
A web application is a software application that runs on a **web server** and is accessed through a **web client**. 

---

### Architecture of a simple web app
<!-- _class: graph -->
<!-- footer: | -->

```
┌─────────────────┐    HTTP Request     ┌─────────────────┐
│                 │ ──────────────────► │                 │
│    CLIENT       │                     │    SERVER       │
│   (Browser)     │                     │   (Python/      │
│                 │                     │    Node.js/     │
│ ┌─────────────┐ │                     │    etc.)        │
│ │   HTML      │ │                     │                 │
│ │   CSS       │ │                     │ ┌─────────────┐ │
│ │ JavaScript  │ │                     │ │   Routes    │ │
│ └─────────────┘ │                     │ │   Logic     │ │
│                 │                     │ │   Database  │ │
│ ┌─────────────┐ │                     │ └─────────────┘ │
│ │ User Input  │ │                     │                 │
│ │ Interactions│ │                     │ ┌─────────────┐ │
│ └─────────────┘ │                     │ │   API       │ │
│                 │    HTTP Response    │ │ Endpoints   │ │
│                 │ ◄────────────────── │ └─────────────┘ │
└─────────────────┘                     └─────────────────┘
```



---

<!-- _class: activity -->

>~10m
# Explore it yourself 
- Go to google.com
- Right click > inspect 
- Search for any keyword (e.g. KFUPM)
- Notice: # requets, requests latecny, type of resource requested, size of response)
![bg right](./img/google.png)


---

# What happens when we Google "KFUPM"? 
- Where does our request be **directed**?
- How does it know the **path**?
- How does it ask for specific **results**?
- How are the results **displayed**?
---

<!-- NEEDS VIZ -->

# The Journey of a Web Request 🌐

1. User types **URL**
2. **DNS** Lookup
3. **IP Address** Found
5. HTTP **Request** Sent
7. HTTP **Response**
8. Browser **Renders** Page

---

<!-- Explain each part  -->

# 1. User types a URL 
## https://www.google.com/search?q=kfupm

- Shceme
- Hostname
- Path
- Query string


---

# 2. DNS Lookup

• **Browser** checks its **cache** first  
• If not found, check **OS cache**  
• If not found, check **router cache**  
• If not found, ask **ISP DNS server**  
• **ISP** asks **Root DNS servers**  
• **Root** points to **TLD servers** (.com)  
• **TLD** points to **authoritative server**  
• **Authoritative server** returns **IP address**  
• **Result** is **cached** at all levels  


---

# 3. IP Address found 

Google.com -> 172.217.18.36

- A unique number that **identifies** each computer using the Internet Protocol to communicate over the internet


---

# 4. HTTP Request Sent 
```
┌─────────────────────────────────────────────────────────────┐
│                    HTTP REQUEST                             │
├─────────────────────────────────────────────────────────────┤
│ GET /search?q=KFUPM HTTP/1.1                                │
│ Host: google.com                                            │
│ User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)       │
│ Accept: text/html,application/xhtml+xml,application/xml     │
│ Accept-Language: en-US,en;q=0.9                             │
│                                                             │
│ [Empty body for GET request]                                │
└─────────────────────────────────────────────────────────────┘
```

---

# 5. HTTP Response Recieved


```
┌─────────────────────────────────────────────────────────────┐
│                    HTTP RESPONSE                            │
├─────────────────────────────────────────────────────────────┤
│ HTTP/1.1 200 OK                                             │
│ Date: Mon, 26 Aug 2024 12:34:56 GMT                         │
│ Content-Type: text/html; charset=UTF-8                      │
│ Content-Length: 10240                                       │
│ Connection: keep-alive                                      │
│                                                             │
│ <!DOCTYPE html>                                             │
│ <html>                                                      │
│   <head><title>Search results for KFUPM</title></head>      │
│   <body>... (HTML content) ...</body>                       │
│ </html>                                                     │
└─────────────────────────────────────────────────────────────┘
```


---

# 6. Browser Renders Page

Response is returned in HTML, CSS and JS

---

# A Simple HTML Page
```html
<!doctype html>
<html>
  <head>
    <style>
      body { background-color: lightblue; }
    </style>
  </head>
  <body>
    Hello, world!
    <script>
      console.log('Hello from JavaScript!');
    </script>
  </body>
</html>
```
---

<!-- _class: demo -->
> Demo ~15m
# Build a simple HTML page 
- Go to our repo (also found in BB)
- Go to demos folder and open 1.2 hello html
- Read the instrutions in the README.md file
---

<!-- _class: demo -->

> Demo ~15m
# Building a real web app
- Go to our repo (also found in BB)
- Go to demos folder and open 1.1 Hello Web
- Fork the repository to your own Github account
- Read the instructions in the README.md file 
- Complete the code and push to Github 

---

# Next class:
- HTML Document
- Basic HTML Tags
- HTML Lists
- HTML Tables 
- HTML Images

