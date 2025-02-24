# MongoDB Study Guide

![License](https://img.shields.io/badge/license-MIT-blue.svg) <!-- Replace with your license -->
![MongoDB](https://img.shields.io/badge/MongoDB-4.4-green.svg) <!-- Replace with your MongoDB version -->

A comprehensive guide to learning MongoDB, covering basics, commands, examples, and practice exercises.

---

## Table of Contents
1. [MongoDB Basics](#mongodb-basics)
2. [MongoDB Installation](#mongodb-installation)
3. [MongoDB Commands and Examples](#mongodb-commands-and-examples)
   - [Database Commands](#database-commands)
   - [Collection Commands](#collection-commands)
   - [Document Commands](#document-commands)
   - [Query Operators](#query-operators)
   - [Aggregation Pipeline](#aggregation-pipeline)
   - [Indexing](#indexing)
4. [Practice Exercises](#practice-exercises)
5. [Resources](#resources)

---

## MongoDB Basics

### What is MongoDB?
MongoDB is a **document-oriented database**.
- Data is stored in **collections** (similar to tables in SQL) and **documents** (similar to rows in SQL).
- Documents are stored in **BSON** format, which is a binary representation of JSON.

### Key Concepts
- **Database**: A container for collections.
- **Collection**: A group of MongoDB documents.
- **Document**: A set of key-value pairs (stored in BSON format).
- **Field**: A key-value pair in a document.
- **Index**: Improves query performance.
- **Schema-less**: Unlike SQL, MongoDB does not enforce a fixed schema.

---

## MongoDB Installation

### Steps to Install MongoDB
1. Download MongoDB from the [official website](https://www.mongodb.com/try/download/community).
2. Install it on your system.
3. Start the MongoDB server:
   ```bash
   mongod
Connect to the server using the MongoDB shell:

bash
Copy
mongo
MongoDB Commands and Examples
a. Database Commands
Show Databases:

bash
Copy
show dbs
Example:

bash
Copy
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
Switch/Create Database:

bash
Copy
use <database_name>
Example:

bash
Copy
> use mydb
switched to db mydb
Drop Database:

bash
Copy
db.dropDatabase()
Example:

bash
Copy
> use mydb
> db.dropDatabase()
{ "dropped" : "mydb", "ok" : 1 }
b. Collection Commands
Create Collection:

bash
Copy
db.createCollection("<collection_name>")
Example:

bash
Copy
> db.createCollection("users")
{ "ok" : 1 }
Show Collections:

bash
Copy
show collections
Example:

bash
Copy
> show collections
users
Drop Collection:

bash
Copy
db.<collection_name>.drop()
Example:

bash
Copy
> db.users.drop()
true
c. Document Commands
Insert Document:

bash
Copy
db.<collection_name>.insert(<document>)
Example:

bash
Copy
> db.users.insert({ name: "John", age: 30, city: "New York" })
WriteResult({ "nInserted" : 1 })
Insert Multiple Documents:

bash
Copy
db.<collection_name>.insertMany([<document1>, <document2>])
Example:

bash
Copy
> db.users.insertMany([
    { name: "Alice", age: 25, city: "London" },
    { name: "Bob", age: 35, city: "Paris" }
  ])
Find Documents:

bash
Copy
db.<collection_name>.find(<query>)
Example:

bash
Copy
> db.users.find({ age: { $gt: 30 } })
{ "_id" : ObjectId("..."), "name" : "Bob", "age" : 35, "city" : "Paris" }
Update Document:

bash
Copy
db.<collection_name>.update(<query>, <update>)
Example:

bash
Copy
> db.users.update({ name: "John" }, { $set: { age: 31 } })
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
Delete Document:

bash
Copy
db.<collection_name>.remove(<query>)
Example:

bash
Copy
> db.users.remove({ name: "John" })
WriteResult({ "nRemoved" : 1 })
d. Query Operators
MongoDB provides various query operators for filtering data.

Comparison Operators:

$eq: Equal to

$ne: Not equal to

$gt: Greater than

$lt: Less than

$gte: Greater than or equal to

$lte: Less than or equal to

Example:

bash
Copy
> db.users.find({ age: { $gt: 30 } })
Logical Operators:

$and: Logical AND

$or: Logical OR

$not: Logical NOT

$nor: Logical NOR

Example:

bash
Copy
> db.users.find({ $or: [{ age: 25 }, { city: "Paris" }] })
Array Operators:

$in: Matches any value in an array

$nin: Matches none of the values in an array

$all: Matches all values in an array

Example:

bash
Copy
> db.users.find({ city: { $in: ["London", "Paris"] } })
e. Aggregation Pipeline
Aggregation operations process data and return computed results.

Aggregation Pipeline:

bash
Copy
db.<collection_name>.aggregate([<stage1>, <stage2>, ...])
Example:

bash
Copy
> db.users.aggregate([
    { $match: { age: { $gt: 30 } } },
    { $group: { _id: "$city", total: { $sum: 1 } } }
  ])
f. Indexing
Indexes improve query performance.

Create Index:

bash
Copy
db.<collection_name>.createIndex({ <field>: 1 })
Example:

bash
Copy
> db.users.createIndex({ name: 1 })
Show Indexes:

bash
Copy
db.<collection_name>.getIndexes()
Example:

bash
Copy
> db.users.getIndexes()
Drop Index:

bash
Copy
db.<collection_name>.dropIndex({ <field>: 1 })
Example:

bash
Copy
> db.users.dropIndex({ name: 1 })
Practice Exercises
Create a database called school and a collection called students.

bash
Copy
> use school
> db.createCollection("students")
Insert 5 student documents with fields like name, age, and grade.

bash
Copy
> db.students.insertMany([
    { name: "Alice", age: 20, grade: "A" },
    { name: "Bob", age: 22, grade: "B" },
    { name: "Charlie", age: 19, grade: "C" },
    { name: "David", age: 21, grade: "A" },
    { name: "Eve", age: 23, grade: "B" }
  ])
Find all students who are older than 20.

bash
Copy
> db.students.find({ age: { $gt: 20 } })
Update the grade of a student.

bash
Copy
> db.students.update({ name: "Alice" }, { $set: { grade: "A+" } })
Delete a student by name.

bash
Copy
> db.students.remove({ name: "Eve" })
Create an index on the name field.

bash
Copy
> db.students.createIndex({ name: 1 })
