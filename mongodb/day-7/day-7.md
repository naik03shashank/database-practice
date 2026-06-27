# MongoDB Update Operators

Update operators are used with:

```javascript
updateOne()
updateMany()
findOneAndUpdate()
```

to modify existing documents.

---

## `$set`

Adds or updates a field.

### Example

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $set:{
         age:23
      }
   }
)
```

Before:

```javascript
{
   name:"Shashank",
   age:22
}
```

After:

```javascript
{
   name:"Shashank",
   age:23
}
```

---

## `$unset`

Removes a field.

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $unset:{
         age:""
      }
   }
)
```

Result:

```javascript
{
   name:"Shashank"
}
```

---

## `$inc`

Increments a numeric value.

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $inc:{
         marks:5
      }
   }
)
```

Before:

```javascript
marks:80
```

After:

```javascript
marks:85
```

---

## `$mul`

Multiplies a numeric value.

```javascript
db.products.updateOne(
   { name:"Laptop" },
   {
      $mul:{
         price:2
      }
   }
)
```

Before:

```javascript
price:50000
```

After:

```javascript
price:100000
```

---

## `$rename`

Renames a field.

```javascript
db.students.updateOne(
   {},
   {
      $rename:{
         marks:"score"
      }
   }
)
```

Before:

```javascript
{
   marks:80
}
```

After:

```javascript
{
   score:80
}
```

---

## `$push`

Adds an element to an array.

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $push:{
         skills:"MongoDB"
      }
   }
)
```

Before:

```javascript
skills:["Java"]
```

After:

```javascript
skills:["Java","MongoDB"]
```

---

## `$pull`

Removes an element from an array.

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $pull:{
         skills:"Java"
      }
   }
)
```

Before:

```javascript
skills:["Java","MongoDB"]
```

After:

```javascript
skills:["MongoDB"]
```

---

## `$addToSet`

Adds a value only if it does not already exist.

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $addToSet:{
         skills:"MongoDB"
      }
   }
)
```

Before:

```javascript
skills:["Java","MongoDB"]
```

After:

```javascript
skills:["Java","MongoDB"]
```

No duplicate is added.

---

## Difference Between `$push` and `$addToSet`

### `$push`

```javascript
db.students.updateOne(
   {},
   {
      $push:{
         skills:"Java"
      }
   }
)
```

Result:

```javascript
["Java","Java"]
```

Duplicates allowed.

### `$addToSet`

```javascript
db.students.updateOne(
   {},
   {
      $addToSet:{
         skills:"Java"
      }
   }
)
```

Result:

```javascript
["Java"]
```

Duplicates prevented.

---

## Common Usage

### Update One Document

```javascript
db.students.updateOne(
   { name:"Shashank" },
   {
      $set:{
         age:23
      }
   }
)
```

### Update Multiple Documents

```javascript
db.students.updateMany(
   { age:{ $lt:18 } },
   {
      $set:{
         status:"Minor"
      }
   }
)
```

---

# Quick Revision

| Operator    | Purpose                   |
| ----------- | ------------------------- |
| `$set`      | Add or update field       |
| `$unset`    | Remove field              |
| `$inc`      | Increment value           |
| `$mul`      | Multiply value            |
| `$rename`   | Rename field              |
| `$push`     | Add to array              |
| `$pull`     | Remove from array         |
| `$addToSet` | Add unique value to array |
