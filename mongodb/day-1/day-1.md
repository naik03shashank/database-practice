# MongoDB Basics

## Connect to MongoDB

```bash
mongosh
```

---

## Show Existing Databases

```javascript
show dbs
```

---

## Create / Switch Database

```javascript
use college
```

Output:

```text
switched to db college
```

---

## Insert One Document

```javascript
db.students.insertOne({
    name: "Shashank",
    age: 22,
    branch: "AI"
})
```

---

## View All Documents

```javascript
db.students.find()
```

Pretty Output:

```javascript
db.students.find().pretty()
```

---

## Insert Multiple Documents

```javascript
db.students.insertMany([
    {
        name: "Rahul",
        age: 21,
        branch: "CSE"
    },
    {
        name: "Priya",
        age: 22,
        branch: "ECE"
    },
    {
        name: "Amit",
        age: 23,
        branch: "AI"
    }
])
```

---

## Find One Document

```javascript
db.students.findOne()
```

---

## Find Documents with Condition

```javascript
db.students.find({
    age: 22
})
```

---

## Find AI Students

```javascript
db.students.find({
    branch: "AI"
})
```

---

## Find Students Older Than 21

```javascript
db.students.find({
    age: {
        $gt: 21
    }
})
```

---

## Find Students Younger Than 23

```javascript
db.students.find({
    age: {
        $lt: 23
    }
})
```

---

## Find Students Age >= 22

```javascript
db.students.find({
    age: {
        $gte: 22
    }
})
```

---

## Update One Document

```javascript
db.students.updateOne(
    {
        name: "Rahul"
    },
    {
        $set: {
            age: 25
        }
    }
)
```

---

## Update Multiple Documents

```javascript
db.students.updateMany(
    {},
    {
        $set: {
            status: "active"
        }
    }
)
```

---

## Delete One Document

```javascript
db.students.deleteOne({
    name: "Rahul"
})
```

---

## Delete Multiple Documents

```javascript
db.students.deleteMany({
    branch: "ECE"
})
```

---

## Count Documents

```javascript
db.students.countDocuments()
```

---

## Show Collections

```javascript
show collections
```

---

## Drop Collection

```javascript
db.students.drop()
```

---

## Drop Database

```javascript
db.dropDatabase()
```

---

# Useful MongoDB Operators

## Greater Than

```javascript
$gt
```

Example:

```javascript
db.students.find({
    age: {
        $gt: 20
    }
})
```

---

## Less Than

```javascript
$lt
```

---

## Greater Than Equal

```javascript
$gte
```

---

## Less Than Equal

```javascript
$lte
```

---

## Not Equal

```javascript
$ne
```

Example:

```javascript
db.students.find({
    branch: {
        $ne: "AI"
    }
})
```

---

## AND Condition

```javascript
db.students.find({
    age: 22,
    branch: "AI"
})
```

---

## OR Condition

```javascript
db.students.find({
    $or: [
        { branch: "AI" },
        { branch: "CSE" }
    ]
})
```

---

# MongoDB Structure

Database
│
├── Collection
│
├── Collection
│
└── Collection

Example:

college
│
└── students
│
├── Document 1
├── Document 2
└── Document 3

Document Example:

{
name: "Shashank",
age: 22,
branch: "AI"
}

```
```
