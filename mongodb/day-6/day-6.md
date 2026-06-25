$all
-----
Used with arrays.
Returns documents where an array contains all specified values.

Example:
db.students.find({
   skills:{
      $all:["Java","MongoDB"]
   }
})

Meaning:
Student must have BOTH Java and MongoDB.


$elemMatch
----------
Used with arrays of documents.
Ensures multiple conditions match the same array element.

Example:
db.students.find({
   exams:{
      $elemMatch:{
         subject:"Math",
         marks:{
            $gt:80
         }
      }
   }
})

Meaning:
Find students whose Math marks are greater than 80.