# Overview for Technical-Interviews
**General Software Concepts**
1. OOPs Concepts
2. SOLID principles
3. Stateless or Stateful 
4. SQL Queries
5. Non-SQL Queries
6. DataStructures 
7. Algorithms  
   
**Web Concepts**  
1. HTML, CSS
2. JS  
  
**Framework Specific**  
1. React, Angular
2. Mongodb


# OOPs Concepts
4 Pillars  ( Encapsulation, Abstraction, Inheritance, Polymopherism )
## Encapsulation
   The grouping of related Property and Methods into objects. 
   ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/encapsulations.PNG)
     
   "The best functions are those with no parameters!" Uncle Bob (Advantage over sphagetti code/ allows you to have lesser parameters)

```javascript
//Encapsulation 
let employee={
   baseSalary: 30000
   overtime: 10, 
   rate:2
}
getWage: function(){
   return this.baseSalary+this.overtime*this.rate
}

//vs normal function
function getWage(baseSalary,overTime,rate){
   return baseSalary+(overTime * rate)
}

```
## Abstraction
Hiding functions & variables as private, Exposing only certain functions & variables as public.  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/abstraction.PNG)  
Advantages.
1. Simpler Interface
2. Reduce impact of changes (eg. public changes affecting private codes)  
## Inheritance 
One class acquires the properties( methods & fields) of another  
Advantages.  
1.  Prevent repeated codes for similar methods & field across multiple classes (eg. Health <- inheirted- EnemyHealth & PlayerHealth)
## Poly mopherism 
Many Forms. Can have diffrent types of inputs(Dog,Cat,Cow) but similar method call ( playSound()) generates different output

//getSound method declaration 
Dog.getSound Method, Dog-> Woof  
Cat.getSound Method, Cat-> Meow  
Cow.getSound Method, Cow-> Moo  
// only write this once.  
soundGenerate.getSound(Dog dog), Dog->Woof
  
  
References  
1. Java Notes https://www.youtube.com/watch?v=pTB0EiLXUC8&t=387s
# SOLID Concepts
S.O.L.I.D. STANDS FOR: 
S — Single responsibility principle  
O — Open closed principle  
L — Liskov substitution principle  
I — Interface segregation principle  
D — Dependency Inversion principle  


## S- Single Responsibility Principle  
Every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class.   
  
The following example is a TypeScript class that defines a Person, this class should not include email validation because that is not related with a person behaviour: (**"Dont put function that change for different reasons in the same class"** Uncle Bob) 
```typescript
class Person {
    public name : string;
    public surname : string;
    public email : string;
    constructor(name : string, surname : string, email : string){
        this.surname = surname;
        this.name = name;
        if(this.validateEmail(email)) {
          this.email = email;
        }
        else {
            throw new Error("Invalid email!");
        }
    }
    validateEmail(email : string) {
        var re = /^([\w-]+(?:\.[\w-]+)*)@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$/i;
        return re.test(email);
    }
    greet() {
        alert("Hi!");
    }
}
```

We can improve the class above by removing the responsibility of email validation from the Person class and creating a new Email class that will have that responsibility:
```typescript
class Email {
    public email : string;
    constructor(email : string){
        if(this.validateEmail(email)) {
          this.email = email;
        }
        else {
            throw new Error("Invalid email!");
        }        
    }
    validateEmail(email : string) {
        var re = /^([\w-]+(?:\.[\w-]+)*)@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$/i;
        return re.test(email);
    }
}

class Person {
    public name : string;
    public surname : string;
    public email : Email;
    constructor(name : string, surname : string, email : Email){
        this.email = email;
        this.name = name;
        this.surname = surname;
    }
    greet() {
        alert("Hi!");
    }
}
```
## O — Open closed principle     
"Modules should be open for extension but closed for modification"-Bertrand Meyer  
The Open Closed Principle (OCP) is the SOLID principle which states that the software entities (classes or methods) should be open for extension but closed for modification.  
  
Basically, we should strive to write a code which doesn’t require modification every time a customer changes its request. Providing such a solution where we can extend the behavior of a class (with that additional customer’s request) and not modify that class, should be our goal most of the time.
  
An Example - calculating area    
Caculating without extensions ( A ton of if, else)
```javascript
public double Area(object[] shapes)
{
    double area = 0;
    foreach (var shape in shapes)
    {
        if (shape is Rectangle)
        {
            Rectangle rectangle = (Rectangle) shape;
            area += rectangle.Width*rectangle.Height;
        }
        else
        {
            Circle circle = (Circle)shape;
            area += circle.Radius * circle.Radius * Math.PI;
        }
    }

    return area;
}
```
Instead we should have a shape interface (with get Area() method) that Rectangle/Circle Class extends from.  
1. Shape Interface
```javascript
public abstract class Shape
{No 
    public abstract double Area();
}
```
2. Rect/Circle Class Extends  
```javascript
public class Rectangle : Shape
{
    public double Width { get; set; }
    public double Height { get; set; }
    public override double Area()
    {
        return Width*Height;
    }
}
```
3. No more switch statement 
```javascript
public class Circle : Shape
{
    public double Radius { get; set; }
    public override double Area()
    {
        return Radius*Radius*Math.PI;
    }
}
public double Area(Shape[] shapes)
{
    double area = 0;
    foreach (var shape in shapes)
    {
        area += shape.Area();
    }

    return area;
}
```
## L — Liskov substitution principle
Ability to replace any instance of a parent class with an instance of one if its child classes without negative side effects. 

**Layman Explanation (Parent: Rectangle, Child: Square).** More famously known as the [ Circle-ellipse problem ](https://en.wikipedia.org/wiki/Circle-ellipse_problem)  
  
In mathematics, a Square is a Rectangle. Indeed it is a specialization of a rectangle. The "is a" makes you want to model this with inheritance. However if in code you made Square derive from Rectangle, then a Square should be usable anywhere you expect a Rectangle. This makes for some strange behavior.  
  
**(Replacing Parent:Rectangle with Child:Square, breaks code violates L Principle)**
Imagine you had SetWidth and SetHeight methods on your Rectangle base class; this seems perfectly logical. However if your Rectangle reference pointed to a Square, then SetWidth and SetHeight doesn't make sense because setting one would change the other to match it. In this case Square fails the Liskov Substitution Test with Rectangle and the abstraction of having Square inherit from Rectangle is a bad one.
  
 **The solution** 
**Model your classes based on behaviours not on properties; model your data based on properties and not on behaviours.** If it behaves like a duck, it's certainly a bird. If a Square doesnt behaves like a Rectangle, then dont inherit! (Although in real-life square is rect)
  
"Objects of subtypes should behave like those of supertypes if used via supertype methods." From Prof Barbara Liskov's lecture
  
**Dropping inheritance**  
This solves the problem at a stroke. Any common operations desired for both a Circle and Ellipse can be abstracted out to a common interface that each class implements

## I — Interface segregation principle  
ISP splits interfaces that are very large into smaller and more specific ones so that clients will only have to know about the methods that are of interest to them. Such shrunken interfaces are also called role interfaces.

Example: A big interface
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Solid_i1.PNG) 

ISP principle, Split into smaller roles.  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Solid_i2.PNG)
  
**Conclusion**  
1. Favouring Composition of Inheritance  
2. Favouring Decopling over Coupling  
Similar to Microservices.  

**Correct abstraction is the key to Interface Segregation Principle** 
So ISP is a poor guidance when designing software, but an excellent indicator of whether it’s healthy or not. Don’t think about ISP when designing your software. Think about whether your abstractions are reusable and composable, and whether your objects are encapsulated and cohesive.

## D — Dependency Inversion principle  
The Dependency Inversion Principle (DIP) states: 
   A. High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g. interfaces).  
   B. Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.  
   
 **Traditional Layers Pattern**  
 ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Solid_d1.PNG)  
 Highly Coupled.  
   
 **Dependency inversion Pattern**   
 ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Solid_d2.PNG)  
Introduction of inheritance/implementation of abstract classes or interfaces. 

References  
1. Uncle Bob Solid Principles https://www.youtube.com/watch?v=pTB0EiLXUC8&t=387s
2. Examle for Open closed Principle http://joelabrahamsson.com/a-simple-example-of-the-openclosed-principle/
3. Example for Liskov Sub Principle https://www.youtube.com/watch?v=Mmy1EUKC_iE
4. Example for Isp https://www.youtube.com/watch?v=xahwVmf8itI
  
# Stateless vs Stateful
 **Stateless applications** don’t “store” data vs **stateful applications** require backing storage. 
 
 
# SQL Queries
SQL databases are primarily called as Relational Databases (RDBMS). SQL databases are table based databases   
SQL databases have predefined schema.

ERM diagram
- Entity
- Relationship
## **CRUD (create read update delete)**

- A databse can be located in many places:
   - within ur android
   - on a remote webserver
   - spread throughout many remote servers"in the cloud")

DataBase Software
Oracle, Microsoft SQL Server Acess, PostgreSQL, MySQL, SQLite

SELECT name
FROM countries
WHERE population > 200000;

Schema, constraints 
  
# OFFICIAL SQL SITE
## DDL (Data Definition Language)
This includes changes to the structure of the table like creation of table, altering table, deleting a table etc.  
  
All DDL commands are **auto-committed.** That means it saves all the changes permanently in the database.

| Commands       | Description  |
| ------------- |:-------------:|
| CREATE      | to create new table or database |
| ALTER     | for alteration      |
| TRUNCATE | delete data rom table     |
| DROP | to drop a table     |
| rename | to rename a table     |

## DML (Data Manipulation Language)
DML commands are used for manipulating the data stored in the table and not the table itself.  
  
DML commands are not auto-committed. It means changes are not permanent to database, they can be rolled back. 

| Commands       | Description  |
| ------------- |:-------------:|
| INSERT     | to insert a new row |
| UPDATE    | to update existing row      |
| DELETE | to delete a row     |
| MERGE | merging two rows or two tables     |

## TCL (Transaction Control Language)
These commands are to keep a check on other commands and their affect on the database. These commands can annul changes made by other commands by rolling the data back to its original state. It can also make any temporary change permanent.  

| Commands       | Description  |
| ------------- |:-------------:|
| COMMIT    | to permanently save |
| ROLLBACK   | to undo change     |
| SAVEPOINT | to save temporarily     |
  
## DCL (Data Control Language)
Data control language are the commands to grant and take back authority from any database user.  

| Commands       | Description  |
| ------------- |:-------------:|
| GRANT   | grant permission of right |
| REVOKE  | take back permission     |
  
## DQL (Data Query Language)
Data query language is used to fetch data from tables based on conditions that we can easily apply.  

| Commands       | Description  |
| ------------- |:-------------:|
| SELECT   | retrieve records from one or mroe table |

## My SQL data type (there is more)
1. Number type  
   a. Int  
   b. Float  
   c. Double  
2. Text type  
   a. Varchar  
   b. Text  
   c. Char  
3. Data type  
   a. Date  
   b. Time  
   c. DateTime  

## DDL (Creating or Deleting Table/ Database etc)
### Creating Table
Create table table-name(columnName1 datatype, coloumnName2 datatype...);
Eg: create table customer(CustID int(4). CustName varchar(10), CustEmail varchar(15));

### Adding new coloumn
Alter table tableName
   Add column columnName datatype;
Eg. Alter table Customer
            add column CustDOB date; 

## Data Manipulation Language (CRUD)
### Create
Insert a pet into data base 
INSERT INTO <table_name> (<columns_name_1>,<columns_name_2>,..) 
               VALUES (<value_1>,<value_2>,...);

INSERT INTO pets (_id,name, breed, gender, weight) 
               VALUES (1,"Tommy","Pomeranian",1,4);

### READ
SELECT * FROM pets WHERE _id ==1;
1 | "Tommy" | " Pomeranian" | 1 | 4 

SELECT * FROM pets WHERE weight>=18;
SELECT name, weight FROM pets WHERE gender == 1 ORDER BY weight DESC;

### UPDATE
UPDATE pets SET weight = 20 WHERE _id == 2;

### DELETE 
DELETE FROM <table_name> ;
DELETE FROM pets;

DELETE FROM pets WHERE _id=<id_pets_interested in> 

## Integrity Constraint 
1. Primary Key 
2. Foreign Key
3. Unique Key
4. Default
5. Not Null
6. Check

## Relationships
- One-One 
- One-Many
- Many-Many  

References  
1. SQL Documentation https://www.studytonight.com/dbms/introduction-to-sql.php

# Non-SQL Queries 
 NoSQL database are primarily called as non-relational or distributed database.  
 NoSQL databases are document based, key-value pairs, graph databases or wide-column stores.
 
 AWS DynamoDB
 
 # DataStructures | Algorithm | Concepts - Overview
 
 |DataStructures |Algorithm   | Concepts|
|:-------------:|:-------------:|:-------------:|
| Linked List        | Breadth First Search  |Bit Manipulation|
| Binary Trees       | Depth First Search    |Singleton Design Patterns |
| Tries              | Binary Search         |Factory Design Patterns   |
| Stacks             | Merge Sort            |Memory (Stack vs Heap)    |
| Queues             | Quick Sort            |Recursion                 |
| Vectors/ ArrayList | Tree Insert           |BIG-O Time                |
| Hash Tables        |                       |                          |



 
 
