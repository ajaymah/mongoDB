# mongoDB
### 1. What is mongoDb ###
mongoDb is a **NoSQL**  (**non-relational**) database, it store data in a type of JSON formate called **BSON(binary json)**
A Database is a collection of data that can easily access.
### 2. diffrence between SQL Databse and NoSQL Database ###
**SQL (Structured Quary Language) Database** : Oracle, MySQL, PostgreSQL  
Data store table formate with relational database
**Relational Database**
A **Relational Database stores data in tables (relations)** with rows and columns, and tables can be connected using keys.  
**NoSQL database**: MongoDB, Radis 
Data store Json Formate like **Bson**  
BSON TYPE = String, Double, 32-bit integer, 64-bit integer, Boolean, Array, Object, Null, regular expression, timestamp, date, objectId,

we can store multiple collection in a single database  
```javascript
Database name - School
DB         |     Collection     |   Document
School     >     Student        > Doc 1
                                  Doc 2
           >     Library        > Doc 1
                                  Doc 2                    
```
**Benefits of MongoDB Database**  
1- **Flexible scema design** - we can easily add new field or delete field.   
2- **Horizontal scalability through sharding**  - we can easily scale overfloew data store other server.     
3- **Hight performance read and write operations.** - due to bason like binary formate computer language 0,1

**MongoDB install -**   
Requirements -   
Window 10/11(64 bit)   
MongoDB Comunity server  
MongoDB shell(mongosh)  

### Create Dadabase & Collection ###
```javascript
// Create dadabse //
use databse_name
Example-   use school

// Create collection //
db.createCollection("collection_name")
example: db.createCollection("students")

// Rename collection
db.old_name.renameCollection("new Name")
example: db.students.renameCollection("student") // remove "S"

// Delete collection
db.library.drop()
example: school> db.library.drop()

// remove Database //
db.dropDatabase()
Example: school> dropDatabase()
responce : {ok:1, dropped:"school"}

// Database shift //
use admin(other database name like admin)
```
```javascript
//Run mongo DB
window R > CMD > mongosh
CTRL + L // use for clear cmd //
show dbs // dispaly all database //
show collections // dispaly collection //
show collections // display all collection in side DB
DB // show database
db.help() // help cmd //
db.collection_name.help()
```
**Add documents inside collection**  
```javascript
insert
insertOne() // single
insertMany() // multiple document insert //
db.collection_name.inserOne()
db.collection_name.insertmany([
{field1:"val", field2:"val"}, {field1:"val", field2:"val"}
]}

// show collection  all data //
db.database_name.find() 
```
**Mongo DB Date**  
```javascript
{dob:ISO("2026-10-18T28:30:00Z")} // T for Time, Z for UTC(universal time) //
{dob:ISO("2026-11-18T18:30:00+02:00")} // CENTAL European time //
{dob:ISO("2026-11-18T18:30:00")} 
```
**MongoDB Integer Data Type**  
```javascript
**32-bit Integer** - uses 32 bits(4 bytes) of memoryto store the integer value.
**64-bit integer** - uses 642 bits(8 bytes) of memoryto store the integer value.
```
**MongoDB JSON Schema validation**  
```javascript
db.createCollection('collection_name',{
   title:"student obj validation"
   required:["name","age"]
   validator: {
      $jsonSchema:{
        name:{
            bsonType:"string",
            description:"Name must be a string and a required"
        },
         age:{
            bsonType:"int",
            minimun:5,
            description:"age must be a integer and min of 5"
        },
        course:{
            bsonType:"string",
            enum:["BCA","MCA"],
            description:"Course must be one of the following values: BCA, MCA"
        }
      }
  }
})
```
**Modify an existing collection`s Schema:**   
```java
db.runcommand({
  collMod: "students"
  validator:{
    $jsonSchema:{
      require:["name","age"],
      properties:{
        name:{
           bsonType:"string",
           description:"Name must be a string and a required"
        }
      }
    }
  }
})
```
**MongoDB Update commands**  
```javascript
// only update one document //
db.collection_name.updateOne(
  {field:"val"},  //filter that field as per field name and value
  { $set:{updated_field:"new_Val"}}  // update
)

// many update one document //
db.collection_name.updateMany(
  {field:"val"},  //filter that field as per field name and value
  { $set:{updated_field:"new_Val"}}  // update
)

db.collection_name.updateMany(
  {},  //filter that field as per field name and value
  { $rename:{"skills":"coding_skills"}}  // rename key
)

db.collection_name.updateMany(
  {},  //filter that field as per field name and value
  { $currentdatee:{"lastModified":true}}  // if key is not available created lastModified key with val //
)

```
**MongoDB Update Oprators**   
```javascript 
$unset: Remove the field from the document  
$rename : Rename the field
$inc: increment the field value
$mul: Multiplies the field value
$currentdate: Set the field value to the current date
$push: Add an element to an Array // {skills:["html","css"]}
$pop: Removes the first or last elementsof an array
$pull: Remove all elements from an array
$addToSet: add distinct elements to an array(cant add diplicat value)
```
**MongoDB Delete commands**:  
```javascript
db.collection_name.deleteOne({field1:"val"})
db.collection_name.deleteMany({field1:"val"})
db.collection_name.deleteOne({})

```
**MongoDB Find commands**:  
```javascript
db.collection_name.find({"field1": "val"})
db.collection_name.findOne({"field1": "val"})
db.collection_name.find()
```

**MongoDB Find with Projection**:   
```javascript
db.collection_name.find(
  {"field": "val"},
  {field1:1, field2:1: field3:0} // 1 will showing, o will not displaying
   {field1:1, field2:1:} // 0 not require
)

db.collection_name.find({"field": "val"}).projection(name:1, class:1, id:0)
db.collection_name.find().limit(3).skip(3) // 4,5,6 will displaying, pagination uses
```
**mongoDB Sort:**  
```javascript
db.collection_name.find().sort({field:1})
// ascending order: 1
// descending order:-1
```
**MongoDB compariosn operator**: 
```javascript
$eq : value are equal {"age":{$eq:20}}
$ne : value are not equal {"age":{$ne:20}}
$gt : value is greater than another value {"age":{$gt:20}}
$gte : value is greater than or equal to another value {"age":{$eq:20}}
$lt : value is less then another value {"age":{$lt:20}}
$lte : value is less then or equal to  another value {"age":{$lte:20}}
$in : value matchecd with in array {"age":{$in:[20,22,24}}
$nin : value is not matched within an array {"age":{$nint:[20,24}}

```
**MongoDB logical Operators**:    
```javascript
{"age":{$lt:20}}
{"city":"Noda"}
$and: {$and:[condition1, condition2]}  both query matched
$ord: {$and:[condition1, condition2]}  either query matched
$nor: {$and:[condition1, condition2]} both query fail
$not: {$and:[condition1]} query does not matched
```

**MongoDb element query operator**:  
```javascript
db.collection_name.find({field:"val"})
$exists
{field:{$exists:<boolean>}} // true or false pass
$type
{field:{$type:<type>}} // int, string
```

**MongoDB Evaluation Query operation**:  
```javascript
$regex: Matches string field to a pattern
{field:{$regex:/pattern/<options>}}   // "^S","an$"
$expr: allows field comparisons with documents
{$expr:{<expression>}}
$mod : Matches numbers based on remainder
{field:{$mod:[divisor, remainder]}} // {age:{$mod:[2,0}}

Example:
db.student.find({name:{$regex:"khan"}}) // case insensetive//
db.student.find({name:{$regex:/khan/i}}) // i represent in regular ex.. case insensetive//
db.monthlyBudget.find({
  $expr:{$gt:["$spent","$budget"]}   /// compare one documet with two fields //
})
db.sales.find({
  $expe:{&gt:["$price",{$mutiply:["$cost",1.2]}]}
})
```
findOneAndupdate and findOneAndDelete
```javascript
db.findOneAndUpdate(
  {name: "sachin"},
  {$set:{age:25, class:"BIT"}},
  {
    returnDocument:"after",
    projection:{name:1, age:1, _id:0},
    upsert: true
  }
)
db.student.findoneAndDelete(
{name:"ajay"},
{projection:{name:1,}, sort:{age:1}} // acending oder age
)
```
### MongoDB Aggregration Pipeline operators ###
```javascript
$match, $count, $sort, $sortByCount, $project, $limit, $skip, $sample
db.collection_name.aggregate([
  {$match:{age:{$gt:20}}},   // stage-1
  {$sort:{age:1}},           // stage-2
  {$project:{name:1,class:1,_id:0}} // stage-3
])

db.collection_name.aggregate([
  {$match: {$and: [   
      {$age:{ $gt:20}},
      {class:"BCA"}
    ]}
  }
]}

db.collection_name.aggregate([
  {$match: {age: {$lt:20}}},
  {$count: "names"}
]}

db.collection_name.aggregate([
  {$match: {age: {$gt:20}}},
  {$sort:{age:1, name:1}},
  {$project:{name:1, calss:1, _id:0 }}
]}

db.collection_name.aggregate([
  {$sort:{age:1, name:1}},
  {$project:{name:1, calss:1, _id:0,
    isValidate:{$gt:["$age",20]}
  }}
]}

db.students.aggregate([
  {$sortByCount:$class}
])

//$Limit 
db.collection_name.aggregate([
  {$match:{age:{$gt:20}}},
  {$sort:{age:1, name:1,]},
  {$project:{name:1, calss:1, _id:0 }},
  {$skip:2},
  {$limit: 2}
]}

db.collection_name.aggregate([
  { $sample: {size:2}}  // search randam data only 2 items
])
```
Gropup
```javascript
db.collection_name.aggregate([
  {$match: {age:{$gt: 20}}},
  {
     $group :{
        _id: "class",
         count: {$sum: 1},
        // count: {$count: {}}//
     }
  }
])

db.collection_name.aggregate([
  {
     $group :{
        _id: "class",
         student: {$push: "$name"}
     }
  }
])

db.collection_name.aggregate([
  {
     $group :{
        _id: "$age",
         student: {$push: "$$ROOT"}
     }
  }
])
```
### MongoDB Aggregate $lookup operator  ###
**get Data with the help of join collection,**
```javascript
// students DB Data
[{_id:1, name:"Ajay", class:"BCA"},{_id:2, name:"Johan", class:"Btech"},{_id:3, name:"Smith", class:"BSC"},{_id:4, name:"Jonathan", class:"BCA"},]
//
// library DB Data 
[{_id:1, book:"Atomic habits", student_id:1},{_id:2, book:"You Can", student_id:2},{_id:3, book:"India Today", student_id:4},]
//
db.library.aggregate([
  $lookup:{
     from: "students"
     localField:"student_id"
     foreignField:"_id"
     as:"Student"
  }
])

db.students.aggregate([
  $lookup:{
     from: "library"
     localField:"_id"
     foreignField:"student_id"
     as:"Book"
  },
  {$unwind:"$Book"}  // if adding this then data will be object case
])

// $replaceRoot Operator
db.library.aggregate([
  $lookup:{
     from: "students"
     localField:"student_id"
     foreignField:"_id"
     as:"Student"
  },
  {$replaceRoot:{newRoot:{$mergeObject:[
    {$arrayElemAt:["$student",0]}, "$$ROOT"
  ]}}},
  {project: {student:0}}
])
```

          
  



