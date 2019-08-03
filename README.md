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
One class acquires the properties( methods & fields of another)  
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
A class should have one, and only one, reason to change. 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/encapsulations.PNG)

// Current Functions Have Responsibility to 3 diff organisation (CEO,CFO,CTO) 
3 Different Organisation, calls 3 Seperatable Methods ( Non-compartmentalised , any changes might affect other codes) 
  


References  
1. Uncle Bob Solid Principles https://www.youtube.com/watch?v=pTB0EiLXUC8&t=387s
Useful quotes: 

