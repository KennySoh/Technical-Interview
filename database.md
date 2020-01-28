# Introduction to Databases - Stanford
https://www.youtube.com/watch?v=spQ7IFksP9g&list=PLroEs25KGvwzmvIxYHRhoGTz9w8LeXek0&index=2 . 
  
Database = set of named **relations** (or **tables**) . 
Each relation has a set of named **attributes**(or **columns**) . 
Each **tuple** (or **row**) has a value for each attribute . 
  
Schmea - Strucutal description of relations in database . 
Instance - the content of database . 
  
NULL - special value for "unkown" or "undefined" . 
Key - attribute whose value is unique in each tuple. Or set of attribute whose combined values are unique . 
  
## Querying relational databases
***
1. Design schema; create using DDL
2. "Bulk load" initial data
3. Repeat: execute queries and modifications
***
  
Ad-hoc queries in high-level language  
***
- All students with GPA> 3.7 applying to Stanford and MIT only
- All engineering departments in CA with <500 applicants
- College with highest average accept rate over last 5 years
***
  
Queries return relations("compositional" , "closed") . 
- "closed" means it returns the same type after query.... returns query . 
- "compositional", Q2 the ability to run query over the result of the previous query.  
***
- Relational Algebra -Formal . 
- SQL - actual/implemented
***

## XML
***
Basic Constructs
- Tagged elements (nested)
- Attributes
- Text
***
```
<Bookstore>
  <Book ISBN="ISBN-0-13-142132 Price="85" Edition = "3rd">
  </Book>
</Bookstore>
```
## JSON
## Relational-Algebra-1

# The Ultimate MYSQL BootCamp
https://www.udemy.com/course/the-ultimate-mysql-bootcamp-go-from-sql-beginner-to-expert/learn/lecture/7054304#overview

## What is a Database
***
1. a collection of data ( eg. a phonebook)
2. a method to accessing and manipulating data (eg. find all first name: Nate)
***
### Database vs DBMS
App >> DBMS >> Database
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/database_2_1.png)
### SQL vs MYSQL 
Structured Query Language,SQL is the language we use to "talk" to our database
```
SELECT * FROM Users WHERE Age >= 18;
```
Working with MySQL/Posgres is primary working with SQL

### Installation 
https://ide-run.goorm.io/
```
mysql-ctl start #Creates Database server
mysql-ctl stop
mysql-ctl cli
mysql> Type all the sql commands here
mysql> Select 1 + 1;
mysql> exit
```
## Creating Databases and Tables
### Creating Databases
```
mysql-ctl start #Creates Database sever

mysql-ctl cli #Start the CLI
>SHOW DATABASES;
>CREATE DATABASE hello_world_db;
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/database_3_1.png)

### Drop Database (Delete Database)
```
DROP DATABASE database_name;
```
### USE Database (Which database u want to use)
```
>USE <database name>;
-- example:
>USE dog_walking_app;
 
>SELECT database();
dog_walking_app
```
### Tables, A Database is a bunch if table
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/database_3_2.png)
- Coloumns (Name, Breed, Age)
- Rows
#### Tables, Datatypes
- Name: varchar(100)
- Breed: varchar(100)
- Age: int
- Cat Age: Age*7 ( This must be all number)

***
- Numeric Types: INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT, DECIMAL , NUMERIC, FLOAT, DOUBLE, BIT
- String Types: CHAR, VARCHAR, BINARY, VARBINARY, BLOB, TINYBLOB, MEDIUMBLOB, LONGBLOB, TEXT, TINYTEXT, MEDIUMTEXT, LONGTEXT, ENUM
- Date Types: DATE, DATETIME, TIMESTAMP, TIME, YEAR
***
### Creating your own table
```
CREATE TABLE tablename
  (
    column_name data_type,
    column_name data_type
  );
  
CREATE TABLE cats
  (
    name VARCHAR(100),
    age INT
  );
  
SHOW TABLES;

SHOW COLUMNS FROM cats;
DESC cats; #describe cats same as show column in this context
```
### Delete Tables
```
DROP TABLE <tablename>; 
DROP TABLE cats; 
```
