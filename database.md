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
## Inserting Data 
### INSERT
```
INSERT INTO table_name(column_name) 
VALUES (data);

INSERT INTO cats(name,age)
VALUES ('Jetson', 7);
-> Query OK, 1 row affected(0.01 sec)
```
### SELECT
View all the data
```
SELECT * FROM cats;
```

### Multiple INSERT
```
INSERT INTO table_name (column_name, column_name) 
    
VALUES  (value, value), 
        (value, value), 
        (value, value);

INSERT INTO cats(name,age)
VALUES ('Jetson',7),
        ('Kenny',10);
```
### MYSQL Warning, A note about warning
Warnings happen when u insert a varchar thats over the limit or wrong datatype
```
CREATE TABLE cats ( name varchar(10),age int);

INSERT INTO cats(name,age)
VALUES ('This is a string that is over 10',7);  //name is over > varchar(10), Results in warning

> Query OK, 1 row affected, 1 warning 

SHOW WARNINGS;
> Warning | 1265 | Data truncated for column 'name' at row 1
```
### NULL and NOT_NULL
```
INSERT INTO cats() 
VALUES();

SELECT * FROM cats
> name | age
> NULL | NULL
```
In order to ensure a column must not be empty, define the column not null when creating table
```
CREATE TABLE cats2(
name VARCHAR(100) NOT NULL,
age INT NOT NULL
);

DESC cats2;
> Field | Type        | Null | Key | Default | Extra|
> name  | varchar(100)| NO   |     | NULL    |      |
> age   | int(11)     | NO   |     | NULL    |      |

INSERT INTO cats2(name) VALUES('Texas');
>Query OK, 1 row affected, 1 warning 

SHOW WARNINGS;
>Warning |1384 | Field age doesnt have a default value|

SELECT * FROM cat2
> name    | age
> 'Texas' |  0        // Age automatically set to 0, If name not defined sets to '' empty string
```
### To Set Default Values
```
CREATE TABLE cats3
(
  name VARCHAR(100) DEFAULT 'unamed',
  age INT DEFAULT 99
);
```
Set NOT NULL
```
CREATE TABLE cats3
(
  name VARCHAR(20) NOT NULL DEFAULT 'no name provided',
  age INT NOT NULL DEFAULT 99
);

INSERT INTO cats4(name,age) VALUES ('Cali', NULL);
>ERROR 10248 Column cannot be NULL
```
### A Primer on Primary Keys
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/database_3_3.png)
Unique identifier Primary Key
```
CREATE TABLE unique_cats
  (
    cat_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
  );

CREATE TABLE unique_cats
  (
    cat_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT
  );
INSERT INTO unique_cats(cat_id, name, age) VALUES (1,"James",3);
```
## CRUD commands
### CREATE
```
INSERT INTO cats(name, age) VALUES(‘Taco’, 14);
```
### READ
```
SELECT * FROM cats; 

SELECT age FROM cats; 

SELECT age, breed, name, cat_id FROM cats;
 
SELECT cat_id, name, age, breed FROM cats; 
```
### Introduction to WHERE
```
-Select by age:

SELECT * FROM cats WHERE age=4; 

-Select by name:

SELECT * FROM cats WHERE name='Egg'; 

-Notice how it deals with case:

SELECT * FROM cats WHERE name='egG'; (case insensitive)
```
### Advance Select Where
```
SELECT cat_id FROM cats; 

SELECT name, breed FROM cats; 

SELECT name, age FROM cats WHERE breed='Tabby'; 

SELECT cat_id, age FROM cats WHERE cat_id=age; 

SELECT * FROM cats WHERE cat_id=age;
```
### Introduction to Aliases
```
SELECT cat_id AS id, name FROM cats;
SELECT name AS 'cat name', breed AS "kitty breed" FROM cats;
```
### The UPDATE Command 
```
UPDATE cats SET breed ="Shorthair" WHERE breed="Tabby";
UPDATE cats SET age=14 WHERE name="Misty";
```

### Introduction to DELETE
```
DELETE FROM cats; //delete all cats
DELETE FROM cats WHERE name="egg";
DELETE FROM cats WHERE age=4;
```

## The World Of STRING Functions
### Running SQL Files 
Instead of running sql create commnads, we can run files 
```
1) Create new file and save as .sql
----first_file.sql----
CREATE TABLE cat (name VARCHAR(100), age INT);
-----------------

2) Running the sql 
>>>source first_file.sql // will run the sql file.
```
### Loading Our Book Data 
```
CREATE DATABASE book_shop;
USE book_shop;
source book_data.sql
DESC book;// describe book table to verify
```

### Working with CONCAT
combines 2 string coloumns. Example: fname +" "+ lname => full name 
```
SELECT author_fname, author_lname FROM books; 
SELECT CONCAT('Kenny',' ','Soh') FROM books; 
SELECT CONCAT('Kenny',' ','Soh') FROM books AS "full name"; 
```

### 
