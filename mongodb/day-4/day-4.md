# MongoDB `$expr` Operator

The `$expr` operator allows us to use aggregation expressions inside a query.

It is mainly used when we need to compare:

* One field with another field
* Perform calculations while filtering documents

---

## Why `$expr`?

Normally, MongoDB compares a field with a fixed value.

### Example

```javascript
db.students.find({
    marks: {
        $gt: 40
    }
})
```

This means:

```text
marks > 40
```

Here we are comparing a field with a constant value.

---

## Using `$expr`

Suppose we have the following documents:

```javascript
{
    name: "Aryan",
    marks: 80,
    passingMarks: 40
}

{
    name: "Rahul",
    marks: 35,
    passingMarks: 40
}
```

Find students whose marks are greater than their passing marks:

```javascript
db.students.find({
    $expr: {
        $gt: ["$marks", "$passingMarks"]
    }
})
```

### Output

```javascript
{
    name: "Aryan",
    marks: 80,
    passingMarks: 40
}
```

Explanation:

```text
Aryan → 80 > 40 ✅
Rahul → 35 > 40 ❌
```

Only Aryan is returned.

---

## Common Operators Used With `$expr`

### Greater Than

```javascript
db.students.find({
    $expr: {
        $gt: ["$marks", "$passingMarks"]
    }
})
```

---

### Less Than

```javascript
db.students.find({
    $expr: {
        $lt: ["$marks", "$passingMarks"]
    }
})
```

---

### Equal To

```javascript
db.students.find({
    $expr: {
        $eq: ["$marks", "$passingMarks"]
    }
})
```

---

### Greater Than or Equal To

```javascript
db.students.find({
    $expr: {
        $gte: ["$marks", "$passingMarks"]
    }
})
```

---

### Less Than or Equal To

```javascript
db.students.find({
    $expr: {
        $lte: ["$marks", "$passingMarks"]
    }
})
```

---

## Field Comparison Pattern

```javascript
db.collection.find({
    $expr: {
        $operator: ["$field1", "$field2"]
    }
})
```

Example:

```javascript
db.products.find({
    $expr: {
        $gt: ["$price", "$cost"]
    }
})
```

This finds products where:

```text
price > cost
```

---

## Using Calculations With `$expr`

Find products where:

```text
(price - cost) > 5000
```

```javascript
db.products.find({
    $expr: {
        $gt: [
            {
                $subtract: ["$price", "$cost"]
            },
            5000
        ]
    }
})
```

---

## Interview Definition

`$expr` allows MongoDB queries to use aggregation expressions. It is commonly used to compare fields within the same document and perform calculations during filtering.
