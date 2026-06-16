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
```
```javascript
//Run mongo DB
window R > CMD > mongosh
CTRL + L // use for clear cmd //
show dbs // dispaly all database //
show collection // display all collection in side DB
DB // show database
```
          
  



