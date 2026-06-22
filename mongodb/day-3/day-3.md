# MongoDB Aggregation Framework

Aggregation is used to process documents and generate computed results. It works like a pipeline where documents pass through multiple stages, and each stage transforms the data.

```text
Documents
   ↓
$match
   ↓
$group
   ↓
$sort
   ↓
Result
```

---

## 1. $match

The `$match` stage filters documents based on a condition. It works similarly to the `find()` method.

### Example

```javascript
db.students.aggregate([
{
    $match: {
        age: { $gt: 20 }
    }
}
]);
```

### Output

Returns only students whose age is greater than 20.

---

## 2. $group

The `$group` stage groups documents by a specified field and performs calculations on each group.

### Example

```javascript
db.sales.aggregate([
{
    $group: {
        _id: "$product"
    }
}
]);
```

### Output

Groups all documents having the same product name together.

---

## 3. $sum

The `$sum` operator is commonly used inside `$group` to calculate totals.

### Example

```javascript
db.sales.aggregate([
{
    $group: {
        _id: "$product",
        totalSales: {
            $sum: "$amount"
        }
    }
}
]);
```

### Output

Calculates the total sales amount for each product.

---

## 4. $avg

The `$avg` operator calculates the average value of a field.

### Example

```javascript
db.students.aggregate([
{
    $group: {
        _id: null,
        averageAge: {
            $avg: "$age"
        }
    }
}
]);
```

### Output

Returns the average age of all students.

---

## 5. $count

The `$count` stage counts the number of documents that pass through the pipeline.

### Example

```javascript
db.students.aggregate([
{
    $count: "totalStudents"
}
]);
```

### Output

```javascript
[
    {
        totalStudents: 50
    }
]
```

---

## 6. $project

The `$project` stage selects, removes, or modifies fields in the output documents.

### Example

```javascript
db.students.aggregate([
{
    $project: {
        name: 1,
        age: 1,
        _id: 0
    }
}
]);
```

### Output

Returns only the `name` and `age` fields while hiding `_id`.

---

## 7. $sort

The `$sort` stage sorts documents in ascending or descending order.

### Ascending Order

```javascript
db.students.aggregate([
{
    $sort: {
        age: 1
    }
}
]);
```

### Descending Order

```javascript
db.students.aggregate([
{
    $sort: {
        age: -1
    }
}
]);
```

### Output

Sorts students by age.

---

## Example Aggregation Pipeline

```javascript
db.sales.aggregate([
{
    $match: {
        amount: { $gt: 1000 }
    }
},
{
    $group: {
        _id: "$product",
        totalRevenue: {
            $sum: "$amount"
        }
    }
},
{
    $sort: {
        totalRevenue: -1
    }
}
]);
```

### Pipeline Explanation

1. `$match` filters sales greater than 1000.
2. `$group` groups sales by product.
3. `$sum` calculates total revenue per product.
4. `$sort` orders products by revenue in descending order.

This is a common real-world aggregation pattern used in analytics and reporting systems.
