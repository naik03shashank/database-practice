# MongoDB Delete Operations

Delete operations are used to remove documents from a collection.

MongoDB provides:

* `deleteOne()`
* `deleteMany()`

---

## deleteOne()

Deletes the first document matching the filter.

### Syntax

```javascript id="kmrn7q"
db.collection.deleteOne(filter)
```

### Example

```javascript id="8jhf0n"
db.students.deleteOne({
   name:"Shashank"
})
```

Before:

```javascript id="vhby0g"
[
   {
      name:"Shashank"
   },
   {
      name:"Rahul"
   }
]
```

After:

```javascript id="a16a78"
[
   {
      name:"Rahul"
   }
]
```

---

## deleteMany()

Deletes all documents matching the filter.

### Syntax

```javascript id="e0hf3q"
db.collection.deleteMany(filter)
```

### Example

```javascript id="a4e56g"
db.students.deleteMany({
   age:{
      $lt:18
   }
})
```

Deletes all students younger than 18.

---

## Delete Using Query Operators

### Delete students older than 60

```javascript id="17u6p4"
db.students.deleteMany({
   age:{
      $gt:60
   }
})
```

---

### Delete users from Bangalore

```javascript id="8h4tst"
db.users.deleteMany({
   city:"Bangalore"
})
```

---

## Delete Embedded Document Matches

```javascript id="0lcgkx"
db.students.deleteMany({
   "address.city":"Mumbai"
})
```

Deletes students whose city is Mumbai.

---

## Delete Array Matches

```javascript id="71s7qf"
db.students.deleteMany({
   skills:"Java"
})
```

Deletes students whose skills array contains Java.

---

## Delete All Documents

```javascript id="5bimjm"
db.students.deleteMany({})
```

Removes every document from the collection.

Collection remains, documents are deleted.

---

## Drop Collection

```javascript id="cxh5ua"
db.students.drop()
```

Deletes:

* Collection
* Documents
* Indexes

---

## Drop Database

```javascript id="upb9ml"
db.dropDatabase()
```

Deletes the entire current database.

⚠️ Use carefully.

---

## Return Value

Example:

```javascript id="yj4mym"
db.students.deleteOne({
   name:"Shashank"
})
```

Output:

```javascript id="4k0t7m"
{
   acknowledged:true,
   deletedCount:1
}
```

### Meaning

```text id="jjlwm1"
acknowledged → MongoDB accepted the operation
deletedCount → Number of documents deleted
```

---

# Quick Revision

| Method           | Purpose                        |
| ---------------- | ------------------------------ |
| `deleteOne()`    | Delete first matching document |
| `deleteMany()`   | Delete all matching documents  |
| `drop()`         | Delete collection              |
| `dropDatabase()` | Delete database                |

---

# Interview Questions

### Difference between deleteOne() and deleteMany()

```text id="8kpsdf"
deleteOne()  → Deletes first matching document
deleteMany() → Deletes all matching documents
```

### Difference between deleteMany({}) and drop()

```text id="g2tsh1"
deleteMany({})
   → Removes all documents
   → Collection remains

drop()
   → Removes entire collection
```
