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
   ![images](https://github.com/KennySoh/Technical-Interview/blob/master/encapsulations.PNG)
     
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
![images](https://github.com/KennySoh/Technical-Interview/blob/master/encapsulations.PNG)  
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


References  
1. Uncle Bob Solid Principles https://www.youtube.com/watch?v=pTB0EiLXUC8&t=387s
Useful quotes: 

