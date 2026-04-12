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
# MongoDB

---

# In today's lecture:
- MongoDB
- Mongoose

### Reference: 
- Zybook: 7.1, 7.2
---
# MongoDB

---
# What is MongoDB?

**MongoDB** is a **NoSQL document database**

- Stores data as **documents** (JSON-like format)
- **Flexible schema** - documents can have different structures
- **Scalable** - handles large amounts of data
- **Fast** - optimized for performance

**Key difference**: No tables, rows, or columns like SQL databases

---
# SQL vs MongoDB

| SQL Database | MongoDB |
|--------------|---------|
| Database | Database |
| Table | Collection |
| Row | Document |
| Column | Field |
| Primary Key | _id (auto-generated) |

---
# MongoDB Structure

```
Database: labDB
  └── Collection: students
        ├── Document 1: { name: "Ali", age: 21, major: "CS" }
        ├── Document 2: { name: "Sara", age: 23, major: "SE" }
        └── Document 3: { name: "Ahmed", age: 20, major: "CS", gpa: 3.8 }
```

**Note**: Documents in the same collection can have different fields!

---
# MongoDB Cloud (Atlas)

MongoDB Atlas is the **cloud-hosted** version of MongoDB

**Benefits**:
- Free tier available
- No local installation needed
- Accessible from anywhere
- Automatic backups
- Easy to scale

**URL**: https://cloud.mongodb.com/

---
# Setting Up MongoDB Atlas

**Step 1**: Sign up and create a cluster
- Choose free plan
- Select AWS as provider
- Choose region and name the cluster

**Step 2**: Create database user
- Set username and password
- Save credentials securely

**Step 3**: Configure network access
- Add IP address: `0.0.0.0/0` (allows all IPs)

---
# MongoDB Shell (mongosh)

**mongosh** is the command-line interface for MongoDB

**Installation**:
- Download from MongoDB website
- Or use MongoDB Atlas web shell

**Purpose**:
- Connect to MongoDB
- Execute commands
- Perform CRUD operations
- Manage databases

---
# Connecting to MongoDB

**From MongoDB Atlas**:
1. Click "Connect" on your cluster
2. Choose "Shell" option
3. Copy connection string
4. Paste in terminal/command prompt

**Connection string format**:
```
mongodb+srv://username:password@cluster0.xxxxx.mongodb.net
```

---
# Working with Databases

**Create or switch to a database**:
```js
use labDB
```

**Note**: Database is created automatically when you first insert data

**View current database**:
```js
db
```

**List all databases**:
```js
show dbs
```

---
# Working with Collections

**Create a collection**:
```js
db.createCollection("students")
```

**Note**: Collection is also created automatically when you insert first document

**List collections in current database**:
```js
show collections
```

**Drop a collection**:
```js
db.students.drop()
```

---
# MongoDB Documents

**Documents** are JSON-like objects stored in collections

```js
{
  _id: ObjectId("..."),  // Auto-generated unique ID
  name: "Ali",
  age: 21,
  major: "CS"
}
```

**Key points**:
- `_id` is automatically created (unique identifier)
- Fields can be any data type
- Documents can have nested objects and arrays

---
# CRUD Operations

**CRUD** = Create, Read, Update, Delete

These are the four basic operations for managing data:

- **Create**: Insert new documents
- **Read**: Find/query documents
- **Update**: Modify existing documents
- **Delete**: Remove documents

---
# Create: Inserting Documents

**Insert one document**:
```js
db.students.insertOne({
  name: "Ali",
  age: 21,
  major: "CS"
})
```

**Insert multiple documents**:
```js
db.students.insertMany([
  { name: "Ali", age: 21, major: "CS" },
  { name: "Sara", age: 23, major: "SE" }
])
```

**Returns**: Object with `insertedId` or `insertedIds`

---
# Read: Finding Documents

**Find all documents**:
```js
db.students.find()
```

**Find with filter**:
```js
db.students.find({ major: "CS" })
```

**Find one document**:
```js
db.students.findOne({ name: "Ali" })
```


---
# Read: Query Operators

**Comparison operators**:
```js
db.students.find({ age: { $gt: 21 } })  // Greater than
db.students.find({ age: { $lt: 20 } })  // Less than
db.students.find({ age: { $gte: 21 } }) // Greater than or equal
db.students.find({ age: { $lte: 23 } }) // Less than or equal
```

**Multiple conditions**:
```js
db.students.find({ major: "CS", age: { $gt: 20 } })
```

---
# Update: Modifying Documents

**Update one document**:
```js
db.students.updateOne(
  { name: "Ali" },           // Filter
  { $set: { age: 22 } }      // Update operation
)
```

**Update multiple documents**:
```js
db.students.updateMany(
  {},                         // Filter (empty = all)
  { $inc: { age: 1 } }       // Increment age by 1
)
```

**Common operators**: `$set`, `$inc`, `$unset`, `$push`

---
# Delete: Removing Documents

**Delete one document**:
```js
db.students.deleteOne({ name: "Sara" })
```

**Delete multiple documents**:
```js
db.students.deleteMany({ age: { $lt: 20 } })
```

**Delete all documents** (keep collection):
```js
db.students.deleteMany({})
```

**Delete collection**:
```js
db.students.drop()
```

---
# Mongoose

---
# What is Mongoose?

**Mongoose** is an **Object Data Modeling (ODM)** library for MongoDB and Node.js

**Purpose**:
- Provides schema validation
- Type casting
- Query building
- Middleware hooks
- Easy connection management

**Think of it as**: A bridge between Node.js and MongoDB

---
# Why Use Mongoose?

<div class="two-column-slide">
  <div class="column-left">

**Without Mongoose** 
- Manual validation
- No schema enforcement
- More verbose code
- Manual type conversion
</div>
<div class="column-right">

**With Mongoose**:
- Schema-based validation
- Automatic type casting
- Cleaner, more readable code
- Built-in methods and helpers
</div>
</div>
---
# Installing Mongoose

**Install via npm**:
```bash
npm install mongoose
```

**Import in your code**:
```js
import mongoose from "mongoose";
```

**Or using CommonJS**:
```js
const mongoose = require("mongoose");
```

---
# Connecting to MongoDB with Mongoose

**Connection string**:
```js
mongoose.connect(
  "mongodb+srv://username:password@cluster0.xxxxx.mongodb.net"
)
```

**With options**:
```js
mongoose.connect(connectionString, {
  useNewUrlParser: true,
  useUnifiedTopology: true
})
```
---
# Connecting to MongoDB with Mongoose

**Handle connection**:
```js
mongoose.connect(connectionString)
  .then(() => console.log("Connected to MongoDB"))
  .catch(err => console.log("Connection error:", err));
```

---
# Mongoose Schemas

**Schema** defines the structure of documents

**Example**:
```js
const studentSchema = new mongoose.Schema({
  name: String,
  age: Number,
  major: String
});
```

**Schema types**:
- `String`, `Number`, `Boolean`, `Date`
- `Array`, `Object`
- `mongoose.Schema.Types.ObjectId`

---
# Mongoose Models

**Model** is a class compiled from a schema

**Create a model**:
```js
const Student = mongoose.model("Student", studentSchema);
```

**Model name**: "Student" (singular, capitalized)
**Collection name**: "students" (plural, lowercase - auto-generated)

**Use the model** to perform CRUD operations

---
# Schema with Options

**Add validation and options**:
```js
const studentSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  age: {
    type: Number,
    min: 0,
    max: 150
  },
  major: {
    type: String,
    default: "Undeclared"
  }
});
```

---
# Create: Inserting Documents

**Using Mongoose**:
```js
async function createStudents() {
  await Student.insertMany([
    { name: "Ali", age: 21, major: "CS" },
    { name: "Sara", age: 23, major: "SE" }
  ]);
  console.log("Inserted successfully");
}

createStudents();
```
---
# Create: Inserting Documents

**Or create one**:
```js
const newStudent = new Student({
  name: "Ahmed",
  age: 20,
  major: "CS"
});
await newStudent.save();
```

---
# Read: Finding Documents

**Find all**:
```js
async function readStudents() {
  const all = await Student.find();
  console.log(all);
}
```
---
# Read: Finding Documents
**Find with filter**:
```js
const csStudents = await Student.find({ major: "CS" });
```

**Find one**:
```js
const student = await Student.findOne({ name: "Ali" });
```

**Find by ID**:
```js
const student = await Student.findById(id);
```

---
# Read: Query Methods

**Chain query methods**:
```js
const results = await Student
  .find({ major: "CS" })
  .where("age").gt(20)
  .limit(10)
  .sort({ age: -1 });
```

**Common methods**:
- `.limit(n)` - limit results
- `.sort({ field: 1 })` - sort (1 = asc, -1 = desc)
- `.select("name age")` - select specific fields
- `.where()` - add conditions

---
# Update: Modifying Documents

**Update one**:
```js
async function updateStudent() {
  await Student.updateOne(
    { name: "Ali" },
    { age: 22 }
  );
  console.log("Updated successfully");
}
```
---
# Update: Modifying Documents

**Update multiple**:
```js
await Student.updateMany(
  { major: "CS" },
  { $inc: { age: 1 } }
);
```

**Find and update**:
```js
const student = await Student.findOneAndUpdate(
  { name: "Ali" },
  { age: 22 },
  { new: true }  // Return updated document
);
```

---
# Delete: Removing Documents

**Delete one**:
```js
async function deleteStudent() {
  await Student.deleteOne({ name: "Sara" });
  console.log("Deleted successfully");
}
```

**Delete multiple**:
```js
await Student.deleteMany({ age: { $lt: 20 } });
```

**Find and delete**:
```js
const student = await Student.findOneAndDelete({ name: "Ali" });
```


---
# Mongoose vs mongosh

| Feature | mongosh | Mongoose |
|---------|---------|----------|
| **Environment** | Command line | Node.js |
| **Schema** | No validation | Schema validation |
| **Type Safety** | Manual | Automatic |
| **Code Style** | MongoDB syntax | JavaScript objects |
| **Use Case** | Testing, admin | Application code |

---
# Best Practices

**Always use async/await**:
```js
async function main() {
  await mongoose.connect(connectionString);
  // ... operations
}
```

---
# Best Practices
**Handle errors**:
```js
try {
  await Student.create({...});
} catch (error) {
  console.error("Error:", error);
}
```

**Close connection** (if needed):
```js
await mongoose.connection.close();
```

---
# What's Next?

**Practice**:
- Set up MongoDB Atlas
- Try CRUD operations in mongosh
- Build a Node.js app with Mongoose

**Wednesday lecture**: RESTful APIs with Express and MongoDB

---
<!-- _class: demo -->

>30m
# Demo

7.1 mongoDB
**MongoDB & Mongoose Hands-on**

- MongoDB Atlas setup
- mongosh CRUD operations
- Mongoose connection and CRUD

