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


