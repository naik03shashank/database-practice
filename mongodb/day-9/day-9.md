# MongoDB Aggregation Framework

Aggregation is used to process documents and generate computed results.

Unlike `find()`, which simply retrieves documents, aggregation allows us to:

* Filter data
* Group data
* Calculate totals
* Calculate averages
* Count documents
* Sort results
* Reshape output

---

# Aggregation Pipeline

Aggregation works using a pipeline.

Each stage processes documents and passes the result to the next stage.

```text
Documents
   ↓
$match
   ↓
$group
   ↓
$project
   ↓
$sort
   ↓
Result
```

### Syntax

```javascript
db.collection.aggregate([
   { stage1 },
   { stage2 },
   { stage3 }
])
```

---

# Sample Collection

```javascript
[
   {
      product:"Laptop",
      category:"Electronics",
      price:50000
   },
   {
      product:"Phone",
      category:"Electronics",
      price:30000
   },
   {
      product:"Book",
      category:"Education",
      price:500
   }
]
```

---

# $match

Filters documents.

Works similarly to `find()`.

### Example

```javascript
db.products.aggregate([
{
   $match:{
      category:"Electronics"
   }
}
])
```

### Output

Returns only electronics products.

---

# $group

Groups documents based on a field.

### Example

```javascript
db.products.aggregate([
{
   $group:{
      _id:"$category"
   }
}
])
```

### Output

Groups all products by category.

---

# $sum

Calculates totals.

### Example

```javascript
db.products.aggregate([
{
   $group:{
      _id:"$category",
      totalRevenue:{
         $sum:"$price"
      }
   }
}
])
```

### Output

```javascript
[
   {
      _id:"Electronics",
      totalRevenue:80000
   }
]
```

---

# $avg

Calculates average values.

### Example

```javascript
db.products.aggregate([
{
   $group:{
      _id:"$category",
      averagePrice:{
         $avg:"$price"
      }
   }
}
])
```

### Output

Returns the average product price per category.

---

# $count

Counts documents.

### Example

```javascript
db.products.aggregate([
{
   $count:"totalProducts"
}
])
```

### Output

```javascript
[
   {
      totalProducts:3
   }
]
```

---

# $project

Used to select, remove, rename, or create fields.

### Example

```javascript
db.products.aggregate([
{
   $project:{
      _id:0,
      product:1,
      price:1
   }
}
])
```

### Output

```javascript
{
   product:"Laptop",
   price:50000
}
```

---

# $sort

Sorts documents.

### Ascending Order

```javascript
db.products.aggregate([
{
   $sort:{
      price:1
   }
}
])
```

### Descending Order

```javascript
db.products.aggregate([
{
   $sort:{
      price:-1
   }
}
])
```

---

# Complete Pipeline Example

Find electronics products and calculate total revenue.

```javascript
db.products.aggregate([
{
   $match:{
      category:"Electronics"
   }
},
{
   $group:{
      _id:"$category",
      totalRevenue:{
         $sum:"$price"
      }
   }
}
])
```

### Pipeline Flow

```text
All Products
   ↓
$match
(Electronics Only)
   ↓
$group
(Group by Category)
   ↓
$sum
(Calculate Revenue)
   ↓
Result
```

---

# Another Example

Find average marks of students older than 18.

```javascript
db.students.aggregate([
{
   $match:{
      age:{
         $gt:18
      }
   }
},
{
   $group:{
      _id:null,
      avgMarks:{
         $avg:"$marks"
      }
   }
}
])
```

---

# Difference Between find() and aggregate()

| find()              | aggregate()                |
| ------------------- | -------------------------- |
| Retrieves documents | Processes documents        |
| Simple filtering    | Advanced analytics         |
| Fast queries        | Computations and reporting |

---

# Quick Revision

| Operator   | Purpose                 |
| ---------- | ----------------------- |
| `$match`   | Filter documents        |
| `$group`   | Group documents         |
| `$sum`     | Calculate total         |
| `$avg`     | Calculate average       |
| `$count`   | Count documents         |
| `$project` | Select or modify fields |
| `$sort`    | Sort documents          |

---

# Interview Definition

Aggregation is a MongoDB framework used to process documents through multiple pipeline stages. Each stage transforms the data and passes the result to the next stage, enabling filtering, grouping, sorting, counting, and analytical computations.
