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
# MongoDB & Mongoose

---

# In today's lecture:
- MongoDB: documents, collections, and the MongoDB Shell
- CRUD operations in the shell
- Mongoose: schemas, models, and CRUD in Node.js

### Reference: 
- Zybook: 7.1, 7.2
---

<!-- _class: activity -->

> Activity: Think-Pair-Share (2 min)

Recall 6.1: a new product with an extra color field is added to both databases.

```sql
INSERT INTO Product VALUES (999, 315.99, 'Smart watch', 'blue');
```
```js
db.products.insertOne({ _id: 999, price: 315.99, title: "Smart watch", color: "blue" })
```

1. A relational database stores data in ____; a document database stores documents in ____ format.
2. Why does the SQL statement fail while the MongoDB command works?
3. What could a table, a row, and a column be called in MongoDB?

<!--
Answers:
1. Tables (relations); JSON format.
2. The product table has no color column. The MongoDB document simply stores the extra field.
3. Model answer: table → collection, row → document, column → field.
Tip: keep the three words (collection, document, field) on the board for the next slides.
-->

---
# 7.2 MongoDB

<!-- Timing: ~14 min for 7.2 (including activities) -->

---

# What is MongoDB?

> **MongoDB** stores data as **documents** (field/value pairs, like JSON), grouped into **collections**

- **Why:** Node.js works seamlessly with MongoDB: JSON data, JavaScript queries
- **Field/value pair:** `gpa: 3.1` → field `gpa`, value `3.1`

```
mydb database
  → students collection
    → { name: "Sue", gpa: 3.1, interests: ["biking", "reading"] }
    → { name: "Larry", gpa: 2.5, interests: ["RPGs", "chess"] }
    → { name: "Anne", gpa: 4.0, interests: ["coding", "Pilates"] }
```

<!--
MongoDB is the most popular NoSQL database used by Node.js developers.
Extra details (zyBooks 7.2):
- Documents are stored internally as BSON (Binary JSON): JSON + extra type information (string, integer, double, date, boolean, null, ...). A BSON document may not exceed 16 MB.
- Documents may contain nested documents, e.g. address: { city: "Dallas", state: "TX" }.
- All documents in a collection; a database holds collections.
-->

---

# MongoDB Shell (mongosh)

> **MongoDB Shell** is a command-line interface for MongoDB; the `mongosh` command starts it

- **Why:** create, query, and delete documents by typing commands

```
$ mongosh
test> use mydb            // creates or selects the "mydb" database
switched to db mydb
mydb> show dbs            // lists all databases
mydb> show collections    // lists all collections in mydb
mydb> exit                // quits the shell
```

<!--
Live: run mongosh, use mydb, show dbs, show collections. use mydb creates mydb because it does not exist.
Extra details (zyBooks 7.2):
- mongosh connects to MongoDB running on the local computer (mongodb://127.0.0.1:27017).
- help → summary of shell commands; db.autos.help() → summary of collection methods.
- Install MongoDB Community Edition and MongoDB Shell from the MongoDB website; the installer includes MongoDB Compass, a GUI.
-->

---

<!-- _class: activity -->

> Activity: Classify, then name the command

```
test> use dealer
dealer> db.autos.insertOne({ _id: 200, make: "Ford", model: "Mustang" })
```

Database, collection, document, field, or value?

1. `dealer`
2. `autos`
3. `{ _id: 200, make: "Ford", model: "Mustang" }`
4. `make`
5. `"Ford"`

<!-- 6. Which command lists all databases? Which lists the collections in dealer? Choose from: `show dbs`, `show collections`, `use dealer` -->

<!--
Answers:
1. Database
2. Collection
3. Document
4. Field
5. Value
6. show dbs; show collections
Tip: ask what db.autos.help() shows (a summary of all collection methods).
-->

---

# Inserting Documents

> `insertOne()` inserts a single document into a collection

- **Why:** this is how data gets into MongoDB (the C in CRUD)
- Every document gets a unique `_id`, the **primary key**

```
mydb> db.students.insertOne({ name: "Sue", gpa: 3.1 })
{ acknowledged: true, insertedId: ObjectId("62794229fc4ebd4933877a9d") }
```

<!--
Live: insert Sue, then db.students.find() to show the _id.
Extra details (zyBooks 7.2):
- insertMany(array) inserts multiple documents: db.students.insertMany([{ name: "Maria", gpa: 4.0 }, { name: "Xiu", gpa: 3.8 }, { name: "Braden", gpa: 2.5 }])
- _id is always the first field. It may be assigned (e.g., _id: 123) or auto-incrementing; otherwise MongoDB assigns an ObjectId (a 12-byte BSON type shown as a hexadecimal number).
-->

---

# Finding Documents

> `find()` returns the documents that match a query; `findOne()` returns only the first

- **Why:** queries read just the data you need
- **Query operators** compare values: `$gt` means greater than

```js
db.students.find()                            // all students
db.students.find({ name: "Sue" })             // students named Sue
db.students.find({ gpa: { $gt: 3.5 } })       // students with gpa > 3.5
db.students.findOne({ gpa: { $gt: 3.5 } })    // only the first match
```

<!--
Live: insert Maria (4.0), Xiu (3.8), Braden (2.5), then run the queries.
Extra details (zyBooks 7.2, Table 7.2.1):
- $eq / $ne (= / ≠), $gt / $gte (> / ≥), $lt / $lte (< / ≤), $in / $nin (in / not in an array)
- $and / $or: { $or: [{ gpa: { $gte: 3.9 } }, { gpa: { $lte: 3.0 } }] }
- findOne() returns null when nothing matches.
-->

---

# Updating & Deleting Documents

> `updateOne()` changes the first matching document; `deleteOne()` removes it

- **Why:** keep data current and remove what is no longer needed
- `updateMany()` / `deleteMany()` → all matching documents

```
mydb> db.students.updateOne({ name: 'Sue' }, { $set: { gpa: 3.3 } })
{ acknowledged: true, insertedId: null, matchedCount: 1, modifiedCount: 1, upsertedCount: 0 }
mydb> db.students.deleteOne({ gpa: { $lt: 3.5 } })
{ acknowledged: true, deletedCount: 1 }
```

<!--
Live: updateOne Sue, find() to confirm, then deleteOne.
Extra details (zyBooks 7.2):
- updateOne/updateMany take a query ({} matches all documents) and an update operator.
- Update operators: $set (sets a value), $inc (increments, e.g. { $inc: { gpa: 0.1 } }), $unset (removes fields), $rename (renames a field), $currentDate (sets the current date/time).
- matchedCount / modifiedCount / deletedCount report how many documents matched, changed, or were deleted.
-->

---

<!-- _class: activity -->

> Activity: Predict: which documents are returned (1–3)? What changes (4–5)?

| _id | make | year | price |
|-----|------|------|-------|
| 100 | Ford | 2014 | 13500 |
| 200 | Honda | 2013 | 16900 |
| 300 | Dodge | 2012 | 10800 |
| 400 | Toyota | 2013 | 13400 |

Key: `$gt` >, `$gte` ≥, `$lt` <, `$set` sets a field

```js
db.autos.find({ year: { $gte: 2013 } })                                   // 1.
db.autos.findOne({ year: { $gte: 2013 } })                                // 2.
db.autos.find({ price: { $lt: 13500 } })                                  // 3.
db.autos.updateOne({ price: { $gt: 13000 } }, { $set: { sold: true } })   // 4.
db.autos.deleteOne({ year: 2013 })                                        // 5.
```

<!--
Answers:
1. _id 100, 200, 400
2. _id 100 (only the first match)
3. _id 300, 400
4. Only auto 100 (the first match) gets a new field sold: true.
5. Auto 200 is deleted (the first auto with year 2013) → deletedCount: 1
Tip: each command runs on the original collection. Ask what updateMany would do in 4 (autos 100, 200, and 400 get sold: true).
-->

---
# 7.1 Mongoose

<!-- Timing: ~17 min for 7.1 (including activities and the exit ticket) -->

---

# What is Mongoose?

> The **mongoose** module adds **structured schemas** to MongoDB collections in Node.js

- **Why:** documents follow a defined structure, and some operations get simpler
- `connect()` must run before any database operation

```js
// npm install mongoose
const mongoose = require("mongoose");
mongoose.connect("mongodb://localhost/mydb");   // creates mydb if it doesn't exist
```

<!--
Extra details (zyBooks 7.1):
- Mongoose provides object data mapping (ODM): converting data from a database into a JavaScript object.
- The mongodb module can also be used; it supports many of the same functions as the shell.
-->

---

# Schemas & Models

> A **schema** defines the structure of documents; a **model** is a constructor compiled from a schema

- **Why:** every student needs a `name`; `gpa` must be 0 to 4
- Model `"Student"` → collection **"students"** (the plural)

```js
const studentSchema = new mongoose.Schema({
  name: { type: String, required: true },
  gpa: { type: Number, min: 0, max: 4 },
  birthDate: { type: Date, default: Date.now }
});
const Student = mongoose.model("Student", studentSchema);
```

<!--
Extra details (zyBooks 7.1):
- Data types: String, Number, Date, Buffer (binary), Boolean, Mixed (any), ObjectId, Array (e.g., [String]).
- required: true → saving without the field fails; min/max → allowed range; default → value used when the field is missing.
- Good practice: capitalize model names and model variables ("Card", not "card").
-->

---

# Saving Documents

> `save()` stores a model instance (a **document**) in the database

- **Why:** `new Student(...)` alone does not touch the database
- `await` waits for the save to finish; the document then has an `_id`

```js
app.get("/create", async function(req, res) {
  const stu = new Student({ name: "Sue Black", gpa: 3.1 });
  await stu.save();
  res.send(`Saved ${stu.name}.`);
});
```

<!--
Live: node server.js, visit http://localhost:8080/create, then check the students collection in mongosh (note the __v field = versionKey).
Extra details (zyBooks 7.1):
- Student.create() also saves one document or an array of documents.
- Full program: require express and mongoose, connect, define the schema and model, create the app, the route above, app.listen(8080).
-->

---

<!-- _class: activity -->

> Activity: What happens if... (each change on its own)

<div class="two-column-slide">

<div class="column-left">

```js
mongoose.connect("mongodb://localhost/mydb");

const studentSchema = new mongoose.Schema({
  name: { type: String, required: true },
  birthDate: { type: Date, default: Date.now }
});
// Model "Student" → collection "students"
const Student = mongoose.model("Student",
  studentSchema);

app.get("/create", async function(req, res) {
  const stu = new Student({ name: "Sue Black" });
  await stu.save();
  res.send(`Saved ${stu.name}.`);
});
```

</div>

<div class="column-right">

1. A student is saved with no `birthDate`?
2. A student is saved with no `name`?
3. `mongoose.model("Dog", dogSchema)`: which collection?
4. The URL ends in `/students` instead of `/mydb`?
5. `await` is removed before `stu.save()`?

</div>

</div>

<!--
Answers:
1. birthDate is the current date and time (default: Date.now).
2. An error occurs, and no student is saved (name is required).
3. The "dogs" collection (the plural of the model name).
4. Mongoose connects to the "students" database (created if it doesn't exist).
5. The route doesn't wait for the save to complete before sending the response.
Tip: _id is assigned when save() is called, not when new Student(...) runs.
Follow-up (ask aloud): True or False, Mongoose is the only way a Node.js app can use MongoDB? False: the mongodb module can also be used.
-->

---

# CRUD with Mongoose

> Model methods work like the shell's `find()`, `findOne()`, `updateOne()`, and `deleteOne()`

- **Why:** same queries and operators, now inside Node.js (use `await`)

```js
const students = await Student.find({ gpa: { $gte: 3 } });
const stu = await Student.findOne({ name: "Sue Black" });

const result = await Student.updateOne({ name: "Sue Black" }, { $set: { gpa: 3.9 } });
console.log("Docs updated: " + result.modifiedCount);

const result2 = await Student.deleteOne({ name: "Sue Black" });
console.log("Docs deleted: " + result2.deletedCount);
```

<!--
Live: add these to an async function and run them one at a time.
Extra details (zyBooks 7.1):
- findById("66901e8c09a55e28d1acc296") finds by _id; findOne/findById return null when nothing matches.
- updateMany() / deleteMany() change or delete all matching documents.
- save() can also update: find a document, change it (stu.gpa += 0.1), then await stu.save().
- Find methods return a Query object; methods can be chained: .where("interests").in(["fishing", "biking"]).sort({ "birthDate": "desc" }).limit(2).exec()
-->

---

<!-- _class: activity -->

> Activity: Predict the result (each line on its own)

| name | Sue | Mara | Dana | Li |
|------|-----|------|------|----|
| gpa | 3.1 | 2.6 | 3.3 | 4.0 |

```js
await Student.find({ gpa: { $gte: 3.2 } });                         // 1. which students?
await Student.findOne({ gpa: { $lt: 3.5 } });                       // 2. which student?
await Student.updateOne({ gpa: { $gt: 3 } }, { $set: { gpa: 4 } }); // 3. who changes?
await Student.deleteOne({ name: "Greg" });                          // 4. deletedCount?
```

Key: `$gt` >, `$gte` ≥, `$lt` <, `$set` sets a field

<!--
Answers:
1. Dana and Li
2. Sue (the first match)
3. Sue (the first student with gpa > 3) → gpa 4, modifiedCount 1
4. 0: no student is named Greg, so nothing is deleted.
-->

---

<!-- _class: activity -->

> Activity: Exit ticket - find the 5 bugs

```js
const mongoose = require("mongoose");
mongoose.connect("http://localhost/mydb");

const studentSchema = new mongoose.Schema({
  name: { type: String, required: true },
  gpa: { type: Number, min: 0, max: 4 }
});
const Student = mongoose.model("Student", studentSchema);

async function addStudent() {
  const stu = new Student({ gpa: 3.5 });
  stu.save();
  const honors = await Student.find({ gpa: { gte: 3.5 } });
  await Student.deleteOne(123);
}
```

<!--
Answers:
1. The URL must start with mongodb:// → mongodb://localhost/mydb
2. name is required → the save fails; add a name.
3. save() is missing await → await stu.save();
4. gte is missing the $ → { gpa: { $gte: 3.5 } }
5. deleteOne needs a query → Student.deleteOne({ _id: 123 })
Tip: a wrong connection string and a missing await are the most common lab mistakes. Follow-up: put the steps in order → require, connect, schema, model, new Student(...), save().
-->

---

# Key Takeaways

- MongoDB stores **documents** (field/value pairs) in **collections** inside databases
- **mongosh:** `use mydb`, `show dbs`, `show collections`
- **Shell CRUD:** `insertOne()`, `find()`, `updateOne()` with `$set`, `deleteOne()`
- **Query operators** like `$gt` and `$lt` filter documents
- **Mongoose:** `connect()` → schema → model → document → `save()`
- **Mongoose CRUD:** the same methods, called on the model with `await`

<!--
Mongoose uses the same CRUD method names as the shell (find, findOne, updateOne, updateMany, deleteOne, deleteMany), plus save(), Model.create(), and findById().
-->

---

<!-- _class: demo -->

>30m
# Demo
7.1 MongoDB

**MongoDB & Mongoose hands-on:**
- MongoDB and mongosh setup
- CRUD operations in mongosh
- Mongoose connection, schema, and CRUD

<!--
Setup: create the cluster on MongoDB Atlas (server.js MongoDB Cloud TODO-1 to TODO-4), connect with mongosh, then cd 7-1-mongodb; npm install; node server.js.
Tasks: mongosh TODO-5 to TODO-9 (use labDB, insert, find, update, delete); Mongoose TODO-1 to TODO-6 in server.js (connect, schema/model, create, read, update, delete). Save screenshots in Mongo-Screen-Shots.
Not in zyBooks ch7 (the lab's server.js TODO hints and README explain them):
- MongoDB Atlas: sign-up, free cluster, database user, IP access list 0.0.0.0/0 (zyBooks runs MongoDB on the local computer)
- Installing mongosh from Atlas and connecting with a mongodb+srv:// connection string with username, password, and database name (zyBooks uses mongodb://localhost/mydb)
- import mongoose from "mongoose" with "type": "module" (zyBooks 7.1 uses require; ES modules were covered in 6.3)
- mongoose.connect(...).then(...).catch(...) (promise then/catch; zyBooks uses await)
- Student.insertMany([...]) in Mongoose (zyBooks uses Student.create() for an array)
- db.createCollection("students") (only appears in the zyBooks Try 7.2.1 code, not explained) and .pretty() (not in zyBooks)
-->

---

# Next Class

- RESTful web APIs (7.3)
- Using RESTful web APIs with Fetch (7.5)
