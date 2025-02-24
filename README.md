# MongoDB
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

```
mongo
```
## MongoDB Commands and Examples
### a. Database Commands
#### 1. Show Databases:
```cs
show dbs
```
Example:
```cs
> show dbs
```
```cs
admin   0.000GB
config  0.000GB
local   0.000GB
```
#### 2. Switch/Create Database:
```cs
use <database_name>
```
Example:

```cs
> use mydb
switched to db mydb
```
#### 3. Drop Database:

```cs
db.dropDatabase()
```
Example:

```cs
> use mydb
> db.dropDatabase()
{ "dropped" : "mydb", "ok" : 1 }
```
## b. Collection Commands
#### 1. Create Collection:

```cs
db.createCollection("<collection_name>")
```
Example:

```cs
> db.createCollection("users")
{ "ok" : 1 }
```
#### 2. Show Collections:

```cs
show collections
```
Example:

```cs
> show collections
users
```
#### 3. Drop Collection:

```cs
db.<collection_name>.drop()
```
Example:

```cs
> db.users.drop()
true
```
## c. Document Commands
##### 1. Insert Document:

```cs
db.<collection_name>.insert(<document>)
```
Example:

```cs
> db.users.insert({ name: "John", age: 30, city: "New York" })
WriteResult({ "nInserted" : 1 })
```
#### 2. Insert Multiple Documents:

```cs
db.<collection_name>.insertMany([<document1>, <document2>])
```
Example:

```cs
> db.users.insertMany([
    { name: "Alice", age: 25, city: "London" },
    { name: "Bob", age: 35, city: "Paris" }
  ])
```
#### 3. Find Documents:
```cs
db.<collection_name>.find(<query>)
```
Example:

```cs
> db.users.find({ age: { $gt: 30 } })
{ "_id" : ObjectId("..."), "name" : "Bob", "age" : 35, "city" : "Paris" }
```
#### 4. Update Document:

```cs
db.<collection_name>.update(<query>, <update>)
```
Example:

```cs
> db.users.update({ name: "John" }, { $set: { age: 31 } })
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```
#### 5. Delete Document:

```cs
db.<collection_name>.remove(<query>)
```
Example:

```cs
> db.users.remove({ name: "John" })
WriteResult({ "nRemoved" : 1 })
```
## d. Query Operators
MongoDB provides various query operators for filtering data.

#### Comparison Operators:

1. $eq: Equal to

2. $ne: Not equal to

3. $gt: Greater than

4. $lt: Less than

5. $gte: Greater than or equal to

6. $lte: Less than or equal to

Example:

```cs
> db.users.find({ age: { $gt: 30 } })
```
### Logical Operators:

1. $and: Logical AND

2. $or: Logical OR

3. $not: Logical NOT

4. $nor: Logical NOR

Example:
```cs
> db.users.find({ $or: [{ age: 25 }, { city: "Paris" }] })
```
### Array Operators:

1. $in: Matches any value in an array

2. $nin: Matches none of the values in an array

3. $all: Matches all values in an array

Example:

```cs
> db.users.find({ city: { $in: ["London", "Paris"] } })
```
## e. Aggregation Pipeline
Aggregation operations process data and return computed results.

Aggregation Pipeline:

```cs
db.<collection_name>.aggregate([<stage1>, <stage2>, ...])
```
Example:

```cs
> db.users.aggregate([
    { $match: { age: { $gt: 30 } } },
    { $group: { _id: "$city", total: { $sum: 1 } } }
  ])
```
## f. Indexing
Indexes improve query performance.

#### 1. Create Index:
```cs
db.<collection_name>.createIndex({ <field>: 1 })
```
Example:

```cs
> db.users.createIndex({ name: 1 })
```
#### 2. Show Indexes:

```cs
db.<collection_name>.getIndexes()
```
Example:

```cs
> db.users.getIndexes()
```
#### 3.Drop Index:

```cs
db.<collection_name>.dropIndex({ <field>: 1 })
```
Example:

```cs
> db.users.dropIndex({ name: 1 })
```
## Practice Exercises
#### 1. Create a database called school and a collection called students.

```cs
> use school
> db.createCollection("students")
```
#### 2. Insert 5 student documents with fields like name, age, and grade.

```cs
> db.students.insertMany([
    { name: "Alice", age: 20, grade: "A" },
    { name: "Bob", age: 22, grade: "B" },
    { name: "Charlie", age: 19, grade: "C" },
    { name: "David", age: 21, grade: "A" },
    { name: "Eve", age: 23, grade: "B" }
  ])
```
#### 3. Find all students who are older than 20.

```cs
> db.students.find({ age: { $gt: 20 } })
```
#### 4. Update the grade of a student.

```cs
> db.students.update({ name: "Alice" }, { $set: { grade: "A+" } })
```
#### 5. Delete a student by name.

```cs
> db.students.remove({ name: "Eve" })
```
#### 6. Create an index on the name field.

```cs
> db.students.createIndex({ name: 1 })
```
