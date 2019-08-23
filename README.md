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
 
 # Overview - DataStructures | Algorithm | Concepts 
 
 |DataStructures |Algorithm   | Concepts|
|:-------------:|:-------------:|:-------------:|
| Linked List        | Breadth First Search  |Bit Manipulation|
| Binary Trees       | Depth First Search    |Singleton Design Patterns |
| Tries              | Binary Search         |Factory Design Patterns   |
| Stacks             | Merge Sort            |Memory (Stack vs Heap)    |
| Queues             | Quick Sort            |Recursion                 |
| Vectors/ ArrayList | Tree Insert           |BIG-O Time                |
| Hash Tables        |                       |                          |

## DataStructures
### Arrays & Strings
Array are abstract data strucuture. Need to be together in memory. Linked list are pointers
#### HashTables (Dictionary)
Hashtables maps key, value pairs.

```java
   Map<String, Integer> table = new Hashtable<>(); 
   table.put("Pen", 10); 
   table.put("Book", 500); 
   table.put("Clothes", 400); 
   table.put("Mobile", 5000); 
```

```python 
   streetno = {"1":"Sachine Tendulkar", "2":"Dravid", "3":"Sehwag", "4":"Laxman","5":"Kohli"}
```

```js
   var myHash = {}; // New object
   myHash['one'] = [1,10,5];
   myHash['two'] = [2];
   myHash['three'] = [3, 30, 300];
```
#### ArrayList (Dynamically Resizing Array):
An array that resizes itself as needed while providing O(1) access. 
```java
   List<String> animals = new ArrayList<>();
   animals.add("Lion");
   animals.add("Tiger");
   animals.add("Cat");
   animals.add("Dog");
```

### Linked List

**Creating a Linked List**
Understand the difference between a singly linked list vs doubly linked list. 
```java
class Node{
   Node next=null; 
   int data;   
   public Node(int d){
      data=d;
   }
   void appendToTail(int d){
      Node end = new Node(d);
      Node n = this;
      while(n.next !=null){ n = n.next;}
      n.next=end;
   }
}
```
**Deleting a Node from a Singly Linked List**
```java
   Node deleteNode(Node head, int d){
      Node n=head;
      if (n.data==d){
         return head.next; 
      }
      while (n.next!=null){
         if(n.next.data==d){
            n.next=n.next.next;
            return head; 
         }
         n=n.next
      }
   }
```
## Stacks and Queues 
Stack -> First in Last Out  
Queues -> First in First Out  
  
**Implementing a Stack**
```java
Class Stack {
   Node top;
   Node pop(){
      if(top!=null){
         Object item - top.data;
         top= top.next;
         return item;
      }
      return null;
   }
   void push(Object item){
      Node t = new Node(item);
      t.next = top;
      top = t;
   }
}
```
  
**Implementing a Queue**
```java
Class Queue{
   Node first,last;
   void enqueue(Object item){
      if(!first){
         back= new Node(item);
         first=back;
      } else{
      back.next=new Node(item);
      back = back.next;
      }
   }
   Node dequeue(Node n){
      if(front!=null){
         Object item =front.data;
         front = front.next; 
         return item; 
      }
      return null; 
   }
}
```
### Trees and Graphs ( Hierarchy Data)
1. Implement a tree/ find a node/ delete a node/ other well- known algorithm  
2. Implement a modification of a known algorithm  
  
Not all binary trees are binary search trees  
  
Concepts:
Root, Children, Parent, Sibiling, Leaf(Nodes with no child) 
Depth and Height ( Node 3 has a depth of 1 an height 0, Node2 has a depth of 1, height of 1)  
   
#### Binary Trees  
Nodes can only have at most 2 child.  
- In-order: Traverse left, current node the right  
- Pre-Order: Traverse cureent node, then left , then right  
- Post-order: Traverse left node, then right node then current node  
- Insert Node  
      tree  
      ----  
       1    <-- root  
     /   \  
    2     3    
   /   
  4  

```java
class Node 
{ 
    int key; 
    Node left, right; 
  
    public Node(int item) 
    { 
        key = item; 
        left = right = null; 
    } 
} 
```
#### Graph Traversal 
- Depth first search: searching all its children before sibilings 
- Breadth first search: search all irs sibilings before going to children 

BFS
// This class represents a directed graph using adjacency list 
// representation 
```java
class Graph 
{ 
    private int V;   // No. of vertices 
    private LinkedList<Integer> adj[]; //Adjacency Lists 
  
    // Constructor 
    Graph(int v) 
    { 
        V = v; 
        adj = new LinkedList[v]; 
        for (int i=0; i<v; ++i) 
            adj[i] = new LinkedList(); 
    } 
  
    // Function to add an edge into the graph 
    void addEdge(int v,int w) 
    { 
        adj[v].add(w); 
    } 
  
    // prints BFS traversal from a given source s 
    void BFS(int s) 
    { 
        // Mark all the vertices as not visited(By default 
        // set as false) 
        boolean visited[] = new boolean[V]; 
  
        // Create a queue for BFS 
        LinkedList<Integer> queue = new LinkedList<Integer>(); 
  
        // Mark the current node as visited and enqueue it 
        visited[s]=true; 
        queue.add(s); 
  
        while (queue.size() != 0) 
        { 
            // Dequeue a vertex from queue and print it 
            s = queue.poll(); 
            System.out.print(s+" "); 
  
            // Get all adjacent vertices of the dequeued vertex s 
            // If a adjacent has not been visited, then mark it 
            // visited and enqueue it 
            Iterator<Integer> i = adj[s].listIterator(); 
            while (i.hasNext()) 
            { 
                int n = i.next(); 
                if (!visited[n]) 
                { 
                    visited[n] = true; 
                    queue.add(n); 
                } 
            } 
        } 
    } 
  
    // Driver method to 
    public static void main(String args[]) 
    { 
        Graph g = new Graph(4); 
  
        g.addEdge(0, 1); 
        g.addEdge(0, 2); 
        g.addEdge(1, 2); 
        g.addEdge(2, 0); 
        g.addEdge(2, 3); 
        g.addEdge(3, 3); 
  
        System.out.println("Following is Breadth First Traversal "+ 
                           "(starting from vertex 2)"); 
  
        g.BFS(2); 
    } 
} 
```
} 

## Algorithm 
### Merge sort
```java
*/class MergeSort 
{ 
    // Merges two subarrays of arr[]. 
    // First subarray is arr[l..m] 
    // Second subarray is arr[m+1..r] 
    void merge(int arr[], int l, int m, int r) 
    { 
        // Find sizes of two subarrays to be merged 
        int n1 = m - l + 1; 
        int n2 = r - m; 
  
        /* Create temp arrays */
        int L[] = new int [n1]; 
        int R[] = new int [n2]; 
  
        /*Copy data to temp arrays*/
        for (int i=0; i<n1; ++i) 
            L[i] = arr[l + i]; 
        for (int j=0; j<n2; ++j) 
            R[j] = arr[m + 1+ j]; 
  
  
        /* Merge the temp arrays */
  
        // Initial indexes of first and second subarrays 
        int i = 0, j = 0; 
  
        // Initial index of merged subarry array 
        int k = l; 
        while (i < n1 && j < n2) 
        { 
            if (L[i] <= R[j]) 
            { 
                arr[k] = L[i]; 
                i++; 
            } 
            else
            { 
                arr[k] = R[j]; 
                j++; 
            } 
            k++; 
        } 
  
        /* Copy remaining elements of L[] if any */
        while (i < n1) 
        { 
            arr[k] = L[i]; 
            i++; 
            k++; 
        } 
  
        /* Copy remaining elements of R[] if any */
        while (j < n2) 
        { 
            arr[k] = R[j]; 
            j++; 
            k++; 
        } 
    } 
  
    // Main function that sorts arr[l..r] using 
    // merge() 
    void sort(int arr[], int l, int r) 
    { 
        if (l < r) 
        { 
            // Find the middle point 
            int m = (l+r)/2; 
  
            // Sort first and second halves 
            sort(arr, l, m); 
            sort(arr , m+1, r); 
  
            // Merge the sorted halves 
            merge(arr, l, m, r); 
        } 
    } 
  
    /* A utility function to print array of size n */
    static void printArray(int arr[]) 
    { 
        int n = arr.length; 
        for (int i=0; i<n; ++i) 
            System.out.print(arr[i] + " "); 
        System.out.println(); 
    } 
  
    // Driver method 
    public static void main(String args[]) 
    { 
        int arr[] = {12, 11, 13, 5, 6, 7}; 
  
        System.out.println("Given Array"); 
        printArray(arr); 
  
        MergeSort ob = new MergeSort(); 
        ob.sort(arr, 0, arr.length-1); 
  
        System.out.println("\nSorted array"); 
        printArray(arr); 
    } 
} 
```
# Web 
## HTML 
```html
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>This is a Heading</h1>
<p>This is a paragraph.</p>
   
 <a href="../html-link.htm"><img src="flower.jpg" width="82" height="86" title="White flower" alt="Flower"></a>

</body>
</html>
```

## CSS 
3 Main ways to add css  
  
Using the inline style attribute on an element
```css
<div>
    <p style="color: maroon;"></p>
</div>
```
  
Using a <style> block in the <head> section of your HTML
```css
<head>
    <title>CSS Refresher</title>
    <style>
        body {
            font-family: sans-serif;
            font-size: 1.2em;
        }
    </style>
</head>
```
 Loading an external CSS file using the <link> tag  
```css
<head>
    <title>CSS Refresher</title>
    <link rel="stylesheet" href="/css/styles.css" />
</head>
```
