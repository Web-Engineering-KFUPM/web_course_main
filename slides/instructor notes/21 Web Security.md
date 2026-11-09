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
# Web Security

---

# In today's lecture:
- Third-party web APIs
- Token-based user authentication (JWT)
- Password hashing

### Reference: 
- Zybook: 8.1-8.3
---

<!-- _class: activity -->

> Activity: Think-Pair-Share (2 min)

You log in to Blackboard once, then open many pages without typing your password again.

1. How could the server know it is still you on every request?
2. Should the server store your actual password? What could it store instead?
3. A weather widget on the page shows today's forecast. Who produced that data?

<!--
Answers:
1. (Model answer) After login, the server gives the browser something that proves you logged in (a token). The browser sends it with every request, and the server checks it.
2. (Model answer) No. If the database is stolen, every password is exposed. The server stores a password hash instead.
3. (Model answer) Probably another organization: a third-party web API (e.g., a weather service).
Tip: write "token", "hash", and "third-party API" on the board; they are today's three sections.
-->

---

# 8.1 Third-Party Web APIs

<!-- Timing: ~6 min for 8.1 (including activities), plus 2 min for the warm-up -->

---

# Third-Party Web APIs

> A **third-party web API** is a web API hosted by another person or organization that any web client may use

- Why: weather data, maps, and more, without building them
- Usually needs an **API key** that identifies who is using it

```
http://api.openweathermap.org/data/2.5/weather?zip=90210&units=imperial&appid=APIKEY
```

<!--
Book examples (Table 8.1.1): Google Maps Platform APIs, OpenWeatherMap API, NASA Image and Video Library API (key required); Pokémon API, Trivia API (no key).
API keys help third parties track usage and may limit the number of requests in a fixed time period.
OpenWeatherMap Weather API: GET requests, JSON by default. Query string parameters: zip (five-digit US ZIP code), units (standard, metric, or imperial), appid (the developer's API key, sent in all requests).
Live: open the URL in the browser with the literal APIKEY to show the "invalid API key" error, then (if you have a key) the real JSON.
-->

---

# Calling a Third-Party API with fetch()

> The web server sends the request with **fetch()** and gets **JSON** back

```js
app.get("/weather", function(req, res) {
  const zip = 90210;
  const params = new URLSearchParams({
    zip: zip, units: "imperial", appid: "APIKEY"});
  fetch("http://api.openweathermap.org/data/2.5/weather?" + params)
    .then(response => response.json())       // JSON → JavaScript objects
    .then(data => res.render("weather", { data: data, zip: zip }))
    .catch(error => console.log(error))
});
```

- `URLSearchParams` builds the query string; `fetch()` needs **Node 18** or above

<!--
Book code (Figure in 8.1): the locals object { data: data, zip: zip } is passed to res.render("weather", locals); weather.pug shows data.main.temp, data.weather[0].description, and data.main.humidity. Pug isn't the point today; the lab returns JSON with res.json().
fetch() returns a Promise; the first then() runs after the response arrives, the second right after the first.
Note for the lab: the lab's routes use async/await instead of then() (students saw this in 5.17 and 7.5):
  app.get("/weather", async function(req, res) { ... const response = await fetch(url + params); if (response.ok) { const data = await response.json(); ... } });
await waits for the response like then(); response.ok is true for a 2xx status code. Mention it verbally; it is not the book's 8.1 code.
-->

---

<!-- _class: activity -->

> Activity: Predict

<div class="two-column-slide">

<div class="column-left">

```js
const params = new URLSearchParams({
  zip: 10001, units: "metric", appid: "KEY"});
fetch("http://api.openweathermap.org/data/2.5/weather?"
  + params)
  .then(response => response.json())
  .then(data => {
    console.log(data.main.temp);
  });
```

Part of the JSON response:
```json
{ "main": { "temp": 21.5 },
  "wind": { "speed": 4.1 } }
```

</div>

<div class="column-right">

1. When does the first then() run?
2. When does the second then() run?
3. Wind speed: data.main.temp, data.wind.speed, or data.main.speed?
4. Celsius: standard, metric, or imperial?
5. What query string does params create?

</div>

</div>

<!--
Answers:
1. After the API response is received.
2. Immediately after the first then() arrow function completes.
3. data.wind.speed
4. metric
5. zip=10001&units=metric&appid=KEY
Tip: these are zyBooks 8.1.2 and 8.1.4.
-->


---

# 8.2 Token-Based User Authentication

<!-- Timing: ~11 min for 8.2 (including activities) -->

---

# Token-Based Authentication

> **Token-based authentication:** the client uses a **signed token** to "prove" to the server that it has successfully authenticated

- Why: the user logs in **once**, not on every request

```
1. POST /api/auth   username + password  → server sends a token
2. Client stores the token
3. GET /api/status  X-Auth: token        → server validates it, sends data
```

<!--
User authentication = verifying that a user is who the user claims to be. Username + password is the most common form (not foolproof; some sites add security questions or images).
Signed token = a string produced with a secret key that uniquely identifies the entity that created it.
Book animation (8.2.1): bsmith logs in, then the web app requests GET api/calendar with the token and gets bsmith's calendar.
Browser side (8.2, mention only): the front end saves the token with localStorage.setItem("token", ...) and sends it with fetch(..., { headers: { "X-Auth": token } }). The lab is server-side and is tested with Postman instead.
-->

---

# JSON Web Tokens (JWT)

> A **JWT** is a string with three parts, **header.payload.signature**, signed with a **secret key** known only by the server

- Why: if the client changes the payload, the signature no longer matches

```
header     eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9          {"typ":"JWT","alg":"HS256"}
payload    eyJ1c2VybmFtZSI6ImJvYiJ9                      {"username":"bob"}
signature  Mm0fNOZMBFOrFu99NlnHdz3jkp5IE_BQCNOz4sh1epQ   secret key "supersecret"
```

<!--
JWT is pronounced "jot". The header and payload are JSON, base64 encoded (64 printable characters). The signature is HMAC SHA256 over the encoded header + encoded payload + the secret key.
Validating: the server builds a new signature from the received header and payload with its secret key; if the payload wasn't modified, the new signature is identical to the JWT's signature.
-->

---

# jwt-simple: encode() and decode()

> The **jwt-simple** module creates and validates JWTs: `npm install jwt-simple`

```js
const jwt = require("jwt-simple");
const secret = "supersecret";

// Create a JWT (after a successful login)
const token = jwt.encode({ username: "bsmith" }, secret);

// Decode a JWT (on later requests)
const decoded = jwt.decode(token, secret);
console.log(decoded.username);   // bsmith
```

- A changed or fake token makes `jwt.decode()` fail

<!--
Book Figure 8.2.1 uses const payload = { username: "bsmith" }; jwt.encode(payload, secret).
Good practice (book): store the secret key in a configuration file and use a long randomized string.
Live: run this file with node and show the three parts of the token (two periods).
-->

---

# The X-Auth Header

> The client sends the token in the **X-Auth** header; the server validates it

- Login route: correct password → `jwt.encode()` → token; else **401**

```js
router.get("/status", function(req, res) {
  const token = req.headers["x-auth"];
  try {
    const decoded = jwt.decode(token, secret);
    res.json({status: "Enjoying a beautiful day!"});
  }
  catch (ex) {
    res.status(401).json({ error: "Invalid JWT" });
  }
});
```

<!--
Book login route (Figure 8.2.2):
  router.post("/auth", function(req, res) {
    if (req.body.username === "bsmith" && req.body.password === "pass") {
      const token = jwt.encode({username: "bsmith"}, secret);
      res.json({ token: token });
    }
    else { res.status(401).json({ error: "Bad username/password" }); }
  });
The status route above is simplified from Figure 8.2.2. The book's full version also:
- sets up const router = express.Router(); router.use(express.urlencoded({ extended: false })); app.use("/api", router);
- checks if (!req.headers["x-auth"]) first → 401 { error: "Missing X-Auth header" }
- returns "Enjoying a beautiful day!" for bsmith and "Working hard!" for any other username.
Live: POST username=bsmith&password=pass to /api/auth, copy the token, then GET /api/status with and without the X-Auth header.
-->

---

<!-- _class: activity -->

> Activity: What happens if... (status code + message)

```
POST /api/auth    not bsmith / pass        → 401 { error: "Bad username/password" }
GET  /api/status  no X-Auth header         → 401 { error: "Missing X-Auth header" }
GET  /api/status  jwt.decode(X-Auth) fails → 401 { error: "Invalid JWT" }
Success: /api/auth → { token: ... }, /api/status → { status: ... }
```

1. POST /api/auth with username=bmsith&password=opensesame
2. GET /api/status with no X-Auth header
3. GET /api/status with X-Auth: bsmith
4. One character of a valid token is changed, then GET /api/status

<!--
Answers:
1. 401 { "error": "Bad username/password" }
2. 401 { "error": "Missing X-Auth header" }
3. 401 { "error": "Invalid JWT" }: "bsmith" is not a valid JWT, so jwt.decode() fails and the catch runs.
4. 401 { "error": "Invalid JWT" }: the new signature no longer matches.
Follow-up (ask aloud): a client learns the server's secret key. What can it do? Create JWTs with any payload that the server accepts as valid: the secret must stay on the server.
Tip: zyBooks 8.2.4, 8.2.5, and 8.2.6.
-->


---

# 8.3 Password Hashing

<!-- Timing: ~12 min for 8.3 (including activities and the exit ticket) -->

---

# Password Hashing

> A **cryptographic hash function** converts text of any length into a fixed-length **hash**; the hash can't be directly converted back

- Why: **never store passwords**; store hashes, so a stolen database doesn't reveal them

```
Register:  opensesame → hash → BC029G8A38   stored in the database
Login:     OpenSesame → hash → 75EE39FA90   ≠ stored → denied
Login:     opensesame → hash → BC029G8A38   = stored → correct password
```

<!--
Hash functions in the book: MD5, SHA-1, bcrypt, PBKDF2. The output is the hash digest ("hash"); changing one character of the input completely changes the hash (try an online MD5 generator: "password" → 5f4dcc3b5aa765d61d8327deb882cf99).
The book's pgreen animation (8.3.2) is the example above.
A site that stores only hashes can't recover a lost password.
-->

---

# Salt

> A **salt** is a random string combined with a password so two identical passwords produce **different hashes**

- Why: cracking salted hashes is much harder

```
opensesame + salt 33M.4Zn7R7k3jHOISHxCe. → yUqI4vl9mv4/oeiLuhHDQZcfySVg6wC
opensesame + salt ByrTcHizkol25k1WOnlV2e → gFI3DdRzo9.xrjal/IyiaKd8X5diFpi
```

<!--
Password cracking = recovering passwords from data, like a compromised website's database.
Dictionary attack: hash many likely passwords (e.g., dictionary words) and compare them with the stolen hashes; attackers precompute dictionary tables. With salt, the attacker needs a table for each salt value.
Strong passwords (book): no dictionary words, upper/lowercase letters + digits (+ punctuation), at least 10 characters, never used before, no popular patterns (initial capital, 2-4 digits or ! at the end).
2012 LinkedIn breach: 6.5 million SHA1 hashes without salt; more than 60% of the unique passwords were cracked.
The salts and digests above come from the book's bcrypt hashes of "opensesame" (next slide).
-->

---

# bcryptjs: hashSync() and compareSync()

> **bcryptjs** (`npm install bcryptjs`) hashes passwords with a random salt

```js
const bcrypt = require("bcryptjs");

// Register: store the hash, not the password
const hash = bcrypt.hashSync("opensesame", 10);   // 10 = cost factor

// Login: compare the submitted password with the stored hash
if (bcrypt.compareSync("opensesame", hash)) {
  console.log("Same!");
}
```

- Same password → a different hash each time, so don't compare hashes with `===`

<!--
hashSync() returns a 60-character hash: $2a$10$33M.4Zn7R7k3jHOISHxCe.yUqI4vl9mv4/oeiLuhHDQZcfySVg6wC → "2a" = bcrypt, "10" = cost factor, 22-character salt, 31-character hash digest. The salt is stored inside the hash.
A larger cost factor → hashSync() takes more time. Book: MD5 and SHA-1 have known weaknesses; bcrypt, scrypt, and PBKDF2 purposely execute slowly, making password cracking significantly more difficult.
compareSync(password, hash) returns true if the password is the one used to create the hash, false otherwise.
Putting it together (8.3 "Using a database"): POST /api/user → hashSync() → save username + hash + status; POST /api/auth → compareSync() → true: jwt.encode() → JWT, false: 401; GET /api/status → X-Auth → jwt.decode().
Live: hash "opensesame" three times in a loop to show three different hashes; then change the compareSync() argument to "OpenSesame" → no output.
-->

---

<!-- _class: activity -->

> Activity: Predict

```js
const hash = bcrypt.hashSync("qwerty", 10);
if (bcrypt.compareSync("Qwerty", hash)) {
  console.log("Same!");
}
else {
  console.log("Not the same");
}
```

1. What does the code output?
2. What if hashSync("qwerty", 10) runs twice: are the two hashes equal?
3. What if the cost factor changes from 10 to 12: does hashSync() take less or more time?
4. Can a website that stores only password hashes recover a user's lost password?

<!--
Answers:
1. Not the same: "Qwerty" and "qwerty" are different passwords.
2. No: each call uses a new random salt.
3. More time.
4. No: the hash can't be converted back into the password.
Tip: zyBooks 8.3.3 and 8.3.5.
-->

---

<!-- _class: activity -->

> Activity: Exit ticket: find the 4 bugs

users is an object: username → saved password data.

```js
router.post("/user", function(req, res) {
  users[req.body.username] = req.body.password;
  res.json({ message: "User added" });
});
router.post("/auth", function(req, res) {
  const hash = bcrypt.hashSync(req.body.password, 10);
  if (hash === users[req.body.username]) {
    res.json({ token: jwt.encode({ username: req.body.username }) });
  } else { res.status(200).json({ error: "Bad username/password" }); }
});
```

<!--
Answers:
1. /user stores the plain-text password → store bcrypt.hashSync(req.body.password, 10) instead.
2. /auth compares two hashes with === → a new salt makes them always different; use bcrypt.compareSync(req.body.password, users[req.body.username]).
3. jwt.encode() is missing the secret key → jwt.encode({ username: req.body.username }, secret).
4. A failed login returns 200 → it should be 401 (unauthorized).
Tip: bugs 1 and 2 are the most common lab mistakes (the lab uses the async bcrypt.hash()/bcrypt.compare(), but the idea is the same).
-->

---

# Key Takeaways

- A **third-party web API** is called from the server with `fetch()`; usually needs an **API key**
- **Token-based auth:** log in once, then send a **signed token** with each request
- **JWT** = header.payload.signature, signed with the server's **secret key**
- jwt-simple: `jwt.encode()` / `jwt.decode()`; token in the **X-Auth** header
- **Never store passwords:** store hashes; **salt** makes equal passwords hash differently
- bcryptjs: `hashSync()` to register, `compareSync()` to log in

---

<!-- _class: demo -->

>30m
# Demo
8.1 Third-Party APIs and Authentication

**Build a secure weather API with:**
- Password hashing
- Token-based authentication
- A third-party weather API

<!--
Setup: npm install; node server.js → http://localhost:3000/ shows "Server is running". Test with Postman or Thunder Client (VS Code extensions), Body → raw → JSON.
Tasks (server.js TODOs): 1) POST /register: hash the password, store { email, passwordHash } in the in-memory users array, 201. 2) POST /login: compare the password, return a JWT. 3) GET /weather?city=Riyadh: require the token, then fetch the weather and return JSON.
Not in zyBooks ch8 (the TODO comments in server.js give the exact code):
- jsonwebtoken: jwt.sign(payload, secret, { expiresIn: "1h" }) and jwt.verify(token, secret) (zyBooks uses jwt-simple's jwt.encode()/jwt.decode(); same idea, plus an expiry time).
- Authorization: Bearer <token> header and auth.split(" ")[1] (zyBooks uses the X-Auth header). One space after "Bearer", no quotes.
- await bcrypt.hash() / await bcrypt.compare(): the async versions of hashSync()/compareSync(); same bcryptjs package and cost factor 10.
- wttr.in weather API with encodeURIComponent(city) (zyBooks uses OpenWeatherMap with URLSearchParams). No API key needed. The README says "GoWeather", but server.js uses wttr.in; data.temperature/description/wind may come back undefined, while raw shows the full response.
- Arrow-function route handlers, const { email, password } = req.body || {}, and users.find(...): plain JavaScript, given verbatim in the TODOs.
- express.json() for JSON request bodies (covered in zyBooks 7.3); cors is in package.json (zyBooks 7.4) but not used by server.js; dotenv / .env is only mentioned in a comment.
- The lab returns 400 for "User not found" / "Wrong password" (zyBooks returns 401); follow the lab so the grader passes.
-->

---

# Next Class

- Course review
- Final project work
