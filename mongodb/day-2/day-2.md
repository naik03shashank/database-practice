# Day 2 - MongoDB Import and Data Management

## Terminal Commands Executed

### 1. Import Products Data
```powershell
mongoimport --db mydatabase --collection products --file "C:\vs code learning\database\mongodb\day-2\jsons\product.json" --jsonArray
```

**Output:**
```
2026-06-15T11:21:29.844+0530    connected to: mongodb://localhost/
2026-06-15T11:21:29.848+0530    100 document(s) imported successfully. 0 document(s) failed to import.
```

### 2. Connect to MongoDB
```powershell
mongosh
```

### 3. Insert Sample Collection Data
```javascript
const docs = Array.from({length: 100}, (_, i) => ({ 
  name: `User ${i+1}`, 
  age: 20 + (i % 40), 
  email: `user${i+1}@example.com` 
})); 
db.sampleCollection.insertMany(docs)
```

### 4. Verify Document Count
```javascript
db.sampleCollection.countDocuments()
// Output: 100
```

## Key Learnings

- ✅ Use full file paths when running mongoimport with subdirectories
- ✅ Quote paths that contain spaces
- ✅ `mongoimport` is a system command, not a MongoDB shell command
- ✅ Use `exit` to leave mongosh shell before running system commands

## Data Imported

- **Database:** mydatabase
- **Collection:** products
- **Documents:** 100 user records with name, age, and email
- **Collection:** sampleCollection (in test database)
- **Documents:** 100 sample records

---

## MongoDB Query Operators

### Comparison Operators

#### **$gt** - Greater Than
```javascript
// Find all users with age greater than 30
db.products.find({ age: { $gt: 30 } })
```

#### **$lt** - Less Than
```javascript
// Find all users with age less than 25
db.products.find({ age: { $lt: 25 } })
```

#### **$gte** - Greater Than or Equal
```javascript
// Find all users with age greater than or equal to 30
db.products.find({ age: { $gte: 30 } })
```

#### **$lte** - Less Than or Equal
```javascript
// Find all users with age less than or equal to 25
db.products.find({ age: { $lte: 25 } })
```

### Logical Operators

#### **$in** - Match Any Value in Array
```javascript
// Find users whose age is 20, 25, or 30
db.products.find({ age: { $in: [20, 25, 30] } })
```

#### **$or** - Logical OR
```javascript
// Find users with age < 22 OR age > 50
db.products.find({ 
  $or: [
    { age: { $lt: 22 } },
    { age: { $gt: 50 } }
  ]
})
```

#### **$and** - Logical AND
```javascript
// Find users with age between 25 and 35
db.products.find({ 
  $and: [
    { age: { $gte: 25 } },
    { age: { $lte: 35 } }
  ]
})

// OR simpler:
db.products.find({ 
  age: { $gte: 25, $lte: 35 }
})
```

### Combined Examples

```javascript
// Find users with name starting with "User 1" AND age > 25
db.products.find({
  $and: [
    { name: /^User 1/ },
    { age: { $gt: 25 } }
  ]
})

// Find users with age in [20, 30, 40] OR email contains "user"
db.products.find({
  $or: [
    { age: { $in: [20, 30, 40] } },
    { email: /user/ }
  ]
})
```

### Quick Reference

| Operator | Meaning | Example |
|----------|---------|---------|
| `$gt` | Greater than | `{ age: { $gt: 30 } }` |
| `$lt` | Less than | `{ age: { $lt: 25 } }` |
| `$gte` | Greater than or equal | `{ age: { $gte: 30 } }` |
| `$lte` | Less than or equal | `{ age: { $lte: 25 } }` |
| `$in` | Match any in array | `{ age: { $in: [20, 25] } }` |
| `$or` | Logical OR | `{ $or: [...] }` |
| `$and` | Logical AND | `{ $and: [...] }` |
