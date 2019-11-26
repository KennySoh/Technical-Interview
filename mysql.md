# MySQL 
https://www.youtube.com/watch?v=7S_tz1z_5bA . 
SQL structure query language . 
  
Database Management System, DBMS  : MySQL, SQLite , Posgres, SQL server, Oracle
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/mysql1.png)  
  
## Download
Download Community server .dmg file: https://dev.mysql.com/downloads/mysql/
Download MYSQL WorkBench graphical tool. https://dev.mysql.com/downloads/workbench/

## Creating database
Select the lightning icon to run existing database codes. ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/mysql2.png)

Table is Created
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/mysql3.png)

## Exploring the database
***
- Tables
- View (virtual tables) 
- stored procedures (Query the top10 paying customers , predefined functions) 
- functions 
***

Clicked Tables, and the table calander icon to see the details of the table . 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/mysql4.png)

## Select Statement
```
USE table_name;

--SELECT customer_id, first_name // "--" this is a comment
--SELECT column1,column2
//or
SELECT *
FROM customers 
WHERE customer_id = 1
ORDER BY first_name
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/mysql5.png)

## Select clause
```
SELECT column1, column2, (points * 10) + 100 AS discount_factor
FROM customers

SELECT DISTINCT state // this selects database with no duplicate state entry
FROM customers 
```
## Make Changes: Double click the specific data and apply changes
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/mysql6.png)
