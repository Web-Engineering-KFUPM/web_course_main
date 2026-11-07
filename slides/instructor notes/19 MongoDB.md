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

<!-- Timing: ~16 min for 7.2 (including activities) -->

---

# What is MongoDB?

> **MongoDB** is the most popular **NoSQL** database used by Node.js developers

- **Document** → a single data object made of **field/value pairs** (like JSON)
- **Collection** → a group of related documents
- Documents are stored internally as **BSON** (Binary JSON)
  - JSON + extra type information: string, integer, double, date, boolean, null, ...
  - A BSON document may not exceed **16 MB**

---

# MongoDB Structure

<div class="two-column-slide">

<div class="column-left">

## A document
```js
{
  name: "Sue",      // string
  gpa: 3.1,         // double
  interests: ["biking", "reading"],
  address: {        // nested
    city: "Dallas",
    state: "TX"
  }
}
```

</div>

<div class="column-right">

## A collection
```js
// students collection
{ name: "Sue", gpa: 3.1, ... }
{ name: "Larry", gpa: 2.5, ... }
{ name: "Anne", gpa: 4.0, ... }
```

```
mydb database
  → students collection
    → documents
```

</div>

</div>

---

# MongoDB Shell (mongosh)

- **MongoDB Shell** → a command-line interface; the `mongosh` command starts it
- The MongoDB installer also includes **MongoDB Compass**, a GUI for MongoDB

```
$ mongosh
Connecting to: mongodb://127.0.0.1:27017/...
test> use mydb                // creates or selects the "mydb" database
switched to db mydb
mydb> db.students.insertOne({ _id: 123, name: "Sue", gpa: 3.1 })
{ acknowledged: true, insertedId: 123 }
mydb> db.students.find()
[ { "_id" : 123, "name" : "Sue", "gpa" : 3.1 } ]
mydb> show dbs                // lists all databases
mydb> show collections        // lists all collections in the current database
mydb> help                    // summary of all shell commands
mydb> exit                    // quits the MongoDB Shell
```

<!--
Live: run mongosh, then use mydb, insert Sue, find(), show dbs, and show collections. Point out that use mydb creates mydb because it does not exist.
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

- `insertOne()` → **one** document; `insertMany()` → **multiple** documents
- `_id` → the **primary key**: uniquely identifies each document; always the first field
- No `_id` given → MongoDB assigns an **ObjectId** (12-byte BSON type, shown in hex)

```
mydb> db.students.insertOne({ name: "Sue", gpa: 3.1 })
{ acknowledged: true, insertedId: ObjectId("62794229fc4ebd4933877a9d") }
mydb> students = [ { name: "Maria", gpa: 4.0 }, { name: "Xiu", gpa: 3.8 },
... { name: "Braden", gpa: 2.5 } ]
mydb> db.students.insertMany(students)
{ acknowledged: true,
  insertedIds: { '0': ObjectId("627942f6fc4ebd4933877a9e"),
                 '1': ObjectId("627942f6fc4ebd4933877a9f"),
                 '2': ObjectId("627942f6fc4ebd4933877aa0") } }
```

---

# Finding Documents & Query Operators

- `find()` → returns **all** documents, or those that match an optional query
- `findOne()` → returns only the **first** matching document (`null` if none)

```js
db.students.find({ name: 'Sue' })                     // field: value → equal to the value
db.students.find({ name: { $ne: "Sue" } })            // $eq / $ne    → = or ≠ the value
db.students.find({ gpa: { $gt: 3.5 } })               // $gt / $gte   → > or ≥ the value
db.students.findOne({ gpa: { $lte: 3.0 } })           // $lt / $lte   → < or ≤ the value
db.students.find({ name: { $in: ["Sue", "Susie"] } }) // $in / $nin   → in or not in an array

// $and / $or → matches both / either clause: gpa >= 3.9 or gpa <= 3.0
db.students.find({ $or: [{ gpa: { $gte: 3.9 } }, { gpa: { $lte: 3.0 } }] })
```

<!--
Live: run db.students.find({ gpa: { $gte: 3.0 } }) (Sue, Maria, Xiu) and the $or example in mongosh.
-->

---

# Updating Documents

- `updateOne()` / `updateMany()` → modify **one** / **multiple** documents
- Parameters: a **query** (`{}` matches **all**) and an **update operator**

```
mydb> db.students.updateOne({ name: 'Sue' }, { $set: { gpa: 3.3 } })
{ acknowledged: true, insertedId: null, matchedCount: 1, modifiedCount: 1, upsertedCount: 0 }
```

```js
{ $set: { gpa: 4.0 } }                   // $set → sets a field's value
{ $inc: { gpa: 0.1 } }                   // $inc → increments a field's value by the amount
{ $unset: { gpa: "", birthDate: "" } }   // $unset → removes fields
{ $rename: { name: 'firstName' } }       // $rename → renames a field
{ $currentDate: { birthDate: true } }    // $currentDate → sets the current date/time
```

---

# Deleting Documents

- `deleteOne()` / `deleteMany()` → delete **one** / **multiple** matching documents
- Returns `deletedCount` → how many documents were deleted

```
mydb> db.students.deleteOne({ gpa: { $lt: 3.5 } })
{ acknowledged: true, deletedCount: 1 }

mydb> db.students.deleteMany({ gpa: { $gt: 3.5 } })
{ acknowledged: true, deletedCount: 2 }

mydb> db.students.find()
[ { _id: ObjectId("627942f6fc4ebd4933877aa0"), name: 'Braden', gpa: 2.5 } ]
```

<!--
Live: deleteOne removed Sue (the first student with GPA < 3.5); deleteMany removed Maria and Xiu.
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

Key: `$gt` >, `$gte` ≥, `$lt` <, `$ne` ≠, `$or` either condition, `$set` sets a field

```js
db.autos.find({ year: { $gte: 2013 } })                                   // 1.
db.autos.findOne({ year: { $gte: 2013 } })                                // 2.
db.autos.find({ $or: [ { make: "Honda" }, { year: { $ne: 2013 } } ] })    // 3.
db.autos.updateOne({ price: { $gt: 13000 } }, { $set: { sold: true } })   // 4.
db.autos.deleteMany({ price: { $lt: 13500 } })                            // 5.
```

<!--
Answers:
1. _id 100, 200, 400
2. _id 100 (only the first match)
3. _id 100, 200, 300
4. Only auto 100 (the first match) gets a new field sold: true.
5. Autos 300 and 400 are deleted → deletedCount: 2
Tip: each command runs on the original collection. Ask what updateMany would do in 4 (autos 100, 200, and 400 get sold: true).
-->

---
# 7.1 Mongoose

<!-- Timing: ~18 min for 7.1 (including activities and the exit ticket) -->

---

# What is Mongoose?

> The **mongoose** module provides **object data mapping (ODM)** and structured schemas to MongoDB collections

- **ODM** → converts data from a database into a **JavaScript object**
- The `mongodb` module also works, with many of the same functions as the shell
- Many developers prefer Mongoose → it **simplifies** some MongoDB operations

```bash
npm install mongoose
```

```js
const mongoose = require("mongoose");
```

---

# Mongoose Schemas

> A **schema** defines the structure of documents within a MongoDB collection

```js
const studentSchema = new mongoose.Schema({
  name: { type: String, required: true },
  gpa: { type: Number, min: 0, max: 4 },
  birthDate: { type: Date, default: Date.now },
  interests: [ String ]
});
```

**Data types:** `String`, `Number`, `Date`, `Buffer` (binary), `Boolean`, `Mixed` (any), `ObjectId`, `Array` (e.g., `[Number]`)

---

# Mongoose Models

> A **model** is a constructor compiled from a schema

```js
// Create a "Student" model from the studentSchema schema
const Student = mongoose.model("Student", studentSchema);

// Create a student document from the Student model
const stu = new Student({
  name: "Sue Black",
  gpa: 3.1,
  birthDate: new Date(2006, 11, 2),
  interests: ["biking", "reading"]
});
```

- Model name `"Student"` → collection **"students"** (the plural)
- Good practice: capitalize model names and variables (`Card`, not `card`)

---

# Connecting & Saving Documents

```js
const express = require("express");
const mongoose = require("mongoose");
mongoose.connect("mongodb://localhost/mydb");
// ... studentSchema and Student model ...
const app = express();
app.get("/create", async function(req, res) {
  const stu = new Student({ name: "Sue Black", gpa: 3.1 });
  await stu.save();
  res.send(`Saved ${stu.name}.`);
});
app.listen(8080);
```

- `connect()` → connects **before** any operations; creates `mydb` if needed
- `await stu.save()` → saves the document and assigns its `_id`
- `Student.create()` → also saves one document or an array of documents

<!--
Live: node server.js, visit http://localhost:8080/create, then check the students collection in mongosh (note the __v field = versionKey).
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

# Finding Documents with Mongoose

| Method | Finds |
|--------|-------|
| `Model.find()` | All documents that match the conditions |
| `Model.findOne()` | The first document that matches |
| `Model.findById()` | The document with the given id |

```js
// Find all students with gpa >= 3
const students = await Student.find({ gpa: { $gte: 3 } });

// Find the student with this ObjectId
const stu = await Student.findById("66901e8c09a55e28d1acc296");
if (stu === null) {
  console.log("No student found");
}
```

---

# Chaining Query Methods

All find methods return a **Query** object → chain methods for a readable query

```js
async function findStudents() {
  const students = await Student.find({ gpa: { $gte: 3 } })
    .where("interests").in(["fishing", "biking"])
    .sort({ "birthDate": "desc" })
    .limit(2)
    .exec();
  students.forEach(function(stu) {
    console.log(stu.name);
  });
}
```

- `where()` → filter on a path; `sort()` → set the sort order
- `limit()` → limit the number of documents; `exec()` → called **last** to run the query

---

<!-- _class: activity -->

> Activity: Predict the output of findStudents()

```js
Student.find({ gpa: { $gte: 3 } }).where("interests").in(["fishing", "biking"])
  .sort({ "birthDate": "desc" }).limit(2).exec();   // then prints each stu.name
```

<div class="two-column-slide">

<div class="column-left">

| name | gpa | birthDate | interests |
|------|-----|-----------|-----------|
| Sue | 3.1 | 2006-11-2 | biking, reading |
| Mara | 2.6 | 2002-5-6 | dancing, coding |
| Dana | 3.3 | 2008-1-15 | gardening, biking |
| Li | 4.0 | 2001-2-6 | rock climbing |
| Greg | 3.2 | 1998-6-30 | fishing, tennis |

</div>

<div class="column-right">

1. What is printed?
2. What if `.limit(2)` becomes `.limit(3)`?
3. What if `"desc"` becomes `"asc"`?
4. What if the `.where(...)` line is removed?

</div>

</div>

<!--
Answers:
1. Dana, Sue (gpa ≥ 3 → Sue, Dana, Li, Greg; fishing or biking → Sue, Dana, Greg; newest birthDate first; first 2)
2. Dana, Sue, Greg
3. Greg, Sue (oldest first)
4. Dana, Sue (Li is third: born 2001)
-->

---

# Update & Delete Methods

<div class="two-column-slide">

<div class="column-left">

## Update
```js
// Change Sue's birthDate to 2008-12-02
const result = await Student.updateOne(
  { name: "Sue Black" },
  { birthDate: new Date(2008, 11, 2) });

// Add 0.5 to all GPAs <= 3.5
const result = await Student.updateMany(
  { gpa: { $lte: 3.5 } },
  { $inc: { gpa: 0.5 } });

// save() also updates a found document
stu.gpa += 0.1;
await stu.save();
```

</div>

<div class="column-right">

## Delete
```js
// Delete student with given id
const result = await Student.deleteOne(
  { _id: "668fe18cda9cd0d66eee9a76" });

// Delete all students with GPA < 3
const result = await Student.deleteMany(
  { gpa: { $lt: 3 } });
console.log("Docs deleted: " +
  result.deletedCount);
```

</div>

</div>

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

- MongoDB stores **documents** (field/value pairs, saved as BSON) in **collections**
- **mongosh:** `use`, `show dbs`, `show collections`, `db.collection.method()`
- **CRUD:** `insertOne/Many`, `find/findOne`, `updateOne/Many`, `deleteOne/Many`
- **Query operators** (`$gt`, `$in`, `$or`) filter; **update operators** (`$set`, `$inc`) modify
- **Mongoose:** schema → model → document → `save()` or `Model.create()`
- Chain Mongoose **Query** methods: `where()`, `sort()`, `limit()`, `exec()`

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
