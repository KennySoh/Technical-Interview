
# The Complete Guide (incl Hooks, React Router
## Writing First React Code
### Calling Single React Componenets
```reactjs
function Person(props){
  return (
    <div className="person">
      <h1>{props.name}</h1>
      <p>Your Age: {props.age}</p>
    </div>
  );
}

ReactDom.render(<Person name="Max" age="28"/>, 
document.querySelector('#p1'));

ReactDom.render(<Person name="Kenny" age="22"/>, 
document.querySelector('#p2'));
```

```html
<div id="p1"></div>
<div id="p2"></div>
```
### Calling Nesting React Componenets together
```reactjs
function Person(props){
  return (
    <div className="person">
      <h1>{props.name}</h1>
      <p>Your Age: {props.age}</p>
    </div>
  );
}

var app=(
  <div>
    <Person name="Max" age="28" />
    <Person name="Kenny" age="29"/>
);

ReactDom.render(app, 
document.querySelector('#p1'));
```

```html
<div id="p1"></div>
```
## Next-Gen JavaScript
### let and const
```js
var x=1;

let y_variable=1;
const x_constant=1;
```
### Arrow Function 
```
function myFnc(x,y){
  console.log(x,y)
}

function myFnc=(x,y)=>{
  console.log(x,y)
}
```
### Exports & Imports(Modules) 
default export. 
```js
---person.js----
const person={
  name:'Max'
}

export default person
```

named export. 
```js 
---utility.js--- 
export const clean =()=> {...}
export const baseData =10;
```
  
The js script we are importing the other js exports into.
```
---app.js---
import person from './person.js'
import prs from './person.js'. #will just export the deafult if there is export default.

import {baseData} from './utility.js'
import {clean} from './utility.js'
```

### Classes 
```js
class Person{
  constructor(){
    this.name= 'Max';
  }
  
  printMyName(){
    console.log(this.name);
  }
}

const person= new Person();
person.printMyName();
```

Extends
```
class Human {
 constructor(){
  this.gender='male';
  }
  
  printGender(){
    console.log(this.gender);
  }
}

class Person extends Human{
  constructor(){
    super();  //Must add this if u are implementing a constructor on Person as well.
    this.name='Max';
    this.gender ='female';
   }
   printMyName(){
    console.log(this.name);
   }
}

const person= new Person();
person.printMyName();
person.printGender();
```
### Classes, Properties & Methods
A more modern syntax of using properties(variables) and methods(functions)
ES6 above vs ES7 
```
class Human{
  gender='male';
  printGender =()=>{
    console.log(this.gender);
  }
}

class Person extends Human{
  name='Max';
  gender='female';
  
  printMyName= () =>{
    console.log(this.name);
  }
}

const person = new Person();
person.printMyName();
person.printGender();
```

### Spread & Rest Operators
```js
--- Spread ---- Used to split up array elements OR object Properties
const newArray=[...oldArray,1,2]
const newObject={...oldObject,newProp:5}
```

```js
--- Rest ---- Used to merge a list of function arguments into an array
function sortArgs(...args){
  return args.sort()
}
```
```
--- Spread Example----
const numbers = [1,2,3];
const newNumbers1 [numbers,4]; 
const newNumbers2 [...numbers,4]; 

console.log(newNumbers1)  // [[1,2,3],4]
console.log(newNumbers2)  // [1,2,3,4] 

const person={
  name:'Max'
};

const newPerson={
  ...person,
  age:28
}
console.log(newPerson); // [object Object]{ age:28, name:"Max" }

```
```
--- Rest Example----
const filter = (...args)=>{
  return args
}

console.log(filter(1,2,3))  // [1,2,3]
```

### Destructuring
Easily extract array elements or object properties and store them in variables
```js
---- Array destructuring-----
[a,b]= ["hello,"Max"]
console.log(a) // hello
console.log(b) // Max

---- Object Destructuring----
{name}={name:'max',age:28}
console.log(name) //Max
console.log(age) // undefined
```

### Reference and primitive type
```js
// Primitive type (eg: number, string) means the underlying value gets copied
const number =1;
const num2 = nummber //underlying value gets copied

// reference type (eg: objects) , pointer get referenced
const person ={
 name:'Max'
}
const secondPerson = person; // Pointer is reference
person.name ='Manu';
console.log(secondPerson);
```
### Refreshing Array Functions
```js
const numbers = [1,2,3];

const doubleNumArray = numbers.map((num) => {
  return num*2;
});

console.log(numbers);
console.log(doubleNumArray);
```
## Section3 : Understanding the Base Features & Syntax
### The build workflow
***
**Why?** 
- We want to ship code as optimise as possible. 
- Use Next-Gen JavaScript Features to write less error prone code
- Be more Productive. css prefixes, or linting (tool to markout suboptimal code)
  
**How?**
- Use Dependency Management Tool npm or yarn ( Managing third party dependencies). 
- Use Bundler. Recommended: Webpack (Write moduler code, allow this modular code to compiled together)
- Use Compiler (Next-Gen JavaScript) Babel + Presets (Compiles nextgen js to browser readable js)
- Use a Development Server. 
***

### Using create react app. 
create react app tool to set up bundler, compiler, development server.
https://github.com/facebook/create-react-app. 
  
1. Need to download node.js to use npm. npm install.
https://nodejs.org/en/

2. npm install create-react-app.
```
sudo npm install create-react-app -g //install create-react-app tool
```
  
3. create new project. 
```
cd to [desired file path]
create-react-app [project-name] --scripts-version 1.1.5 // script-version defines a folder structure


```

