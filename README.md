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
```
show dbs
```
Example:
```
> show dbs
```
admin   0.000GB
config  0.000GB
local   0.000GB
#### 2. Switch/Create Database:
```
use <database_name>
```
Example:

```
> use mydb
switched to db mydb
```
#### 3. Drop Database:

```
db.dropDatabase()
```
Example:

```
> use mydb
> db.dropDatabase()
{ "dropped" : "mydb", "ok" : 1 }
```
## b. Collection Commands
#### 1. Create Collection:

```
db.createCollection("<collection_name>")
```
Example:

```
> db.createCollection("users")
{ "ok" : 1 }
```
#### 2. Show Collections:

```
show collections
```
Example:

```
> show collections
users
```
#### 3. Drop Collection:

```
db.<collection_name>.drop()
```
Example:

```
> db.users.drop()
true
```
## c. Document Commands
##### 1. Insert Document:

```
db.<collection_name>.insert(<document>)
```
Example:

```
> db.users.insert({ name: "John", age: 30, city: "New York" })
WriteResult({ "nInserted" : 1 })
```
#### 2. Insert Multiple Documents:

```
db.<collection_name>.insertMany([<document1>, <document2>])
```
Example:

```
> db.users.insertMany([
    { name: "Alice", age: 25, city: "London" },
    { name: "Bob", age: 35, city: "Paris" }
  ])
```
#### 3. Find Documents:
```
db.<collection_name>.find(<query>)
```
Example:

```
> db.users.find({ age: { $gt: 30 } })
{ "_id" : ObjectId("..."), "name" : "Bob", "age" : 35, "city" : "Paris" }
```
#### 4. Update Document:

```
db.<collection_name>.update(<query>, <update>)
```
Example:

```
> db.users.update({ name: "John" }, { $set: { age: 31 } })
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```
#### 5. Delete Document:

```
db.<collection_name>.remove(<query>)
```
Example:

```
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

```
> db.users.find({ age: { $gt: 30 } })
```
### Logical Operators:

1. $and: Logical AND

2. $or: Logical OR

3. $not: Logical NOT

4. $nor: Logical NOR

Example:
```
> db.users.find({ $or: [{ age: 25 }, { city: "Paris" }] })
```
### Array Operators:

1. $in: Matches any value in an array

2. $nin: Matches none of the values in an array

3. $all: Matches all values in an array

Example:

```
> db.users.find({ city: { $in: ["London", "Paris"] } })
```
## e. Aggregation Pipeline
Aggregation operations process data and return computed results.

Aggregation Pipeline:

```
db.<collection_name>.aggregate([<stage1>, <stage2>, ...])
```
Example:

```
> db.users.aggregate([
    { $match: { age: { $gt: 30 } } },
    { $group: { _id: "$city", total: { $sum: 1 } } }
  ])
```
## f. Indexing
Indexes improve query performance.

#### 1. Create Index:
```
db.<collection_name>.createIndex({ <field>: 1 })
```
Example:

```
> db.users.createIndex({ name: 1 })
```
#### 2. Show Indexes:

```
db.<collection_name>.getIndexes()
```
Example:

```
> db.users.getIndexes()
```
#### 3.Drop Index:

```
db.<collection_name>.dropIndex({ <field>: 1 })
```
Example:

```
> db.users.dropIndex({ name: 1 })
```
## Practice Exercises
#### 1. Create a database called school and a collection called students.

```
> use school
> db.createCollection("students")
```
#### 2. Insert 5 student documents with fields like name, age, and grade.

```
> db.students.insertMany([
    { name: "Alice", age: 20, grade: "A" },
    { name: "Bob", age: 22, grade: "B" },
    { name: "Charlie", age: 19, grade: "C" },
    { name: "David", age: 21, grade: "A" },
    { name: "Eve", age: 23, grade: "B" }
  ])
```
#### 3. Find all students who are older than 20.

```
> db.students.find({ age: { $gt: 20 } })
```
#### 4. Update the grade of a student.

```
> db.students.update({ name: "Alice" }, { $set: { grade: "A+" } })
```
#### 5. Delete a student by name.

```
> db.students.remove({ name: "Eve" })
```
#### 6. Create an index on the name field.

```
> db.students.createIndex({ name: 1 })
```
