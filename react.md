# Steps to build a react project from scratch
***
- Create a wire frame (Draw.io)
- Clean Up ur React Project
- 
***

## Create-React-App & clean up your project
```
npx create-react-app <your_project>

Start cleaning up 
- Delete all the content in App,js. #BEM naming class
- Delete all the App.css
- Modify index.css 
// ( add this at the top of the file , this remove browser default styles )
* {
    margin: 0;
}
```

## Start planning out your app & put comments into your page
```
{/* Header */}
{/* Sidebar */}
{/* Body- Recommended Video */}
```

## ES7 Code snippets
```
rfce > this will create component for you
```

## Material UI Icons
```
// with npm
npm install @mui/icons-material

https://mui.com/material-ui/material-icons/?query=alert&theme=Sharp

import MenuIcon from '@mui/icons-material/Menu';
```

## Building out the Header
1. Add out the Html Elements + MaterialUI Icons
```
<div clasName="header">
    <MenuIcon />
    <img className="header__logo" src="https://upload.wikimedia.org/wikipedia/commons alt="" />
    <input type="text" />
    <SearchIcon />
    <VideoCallIcon />
    <AppsIcon />
    <NotificationsIcon />
    <Avatar alt="Kenny" src="img" />
</div>
```

2. Use flexbox for layout
```
import './Header.css';

.header{
    display: flex;
    align-items: center;  //make things vertically - centered
}

.header__logo{
    
}
```





















# How I approach a react project. 

Project structure ( Styled-Component, Typescript, React router, Redux )
- pages
    - api
    - component 
        - Booking
    - BookingPage
    - HomePage
    - AllBooking
- services
- redux
- utils

Mobile first 
- Ensure the Layout ( 2 col, sider … etc)
- ( Create the nav bar, @media Queries )

Pages start putting all the different pages in 
- Fill in the pages 

Axios, Fetch hooking up backend 
- Ensure interface is created for req , res, dataschema. 



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

## Section 3 
### What are Components? 
### React Code is Written in a Declarative Way
### Creating a new React Project

-- Create a new react app --
```
-- Make sure node and npm is installed --
1) Download https://nodejs.org/en/
node -v //needs to be above version ? , to use npx 
npm -v 

-- using the create react app tool. https://reactjs.org/docs/create-a-new-react-app.html --
npx create-react-app my-app
cd my-app
npm start
```
-- Opening an existing react app --  
```
npm install //Will look into package.json and install all necessary dependency
npm start
```

### Analysing a react app
-- src> Index.js --  
```
import React from 'react';
import ReactDOM from 'react-dom';  <-- We are importing react dom 
import './index.css';
import App from './App'; <--  we are importing the App function from App.js
import reportWebVitals from './reportWebVitals';


ReactDOM.render( 
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
  
-- public > index.html --  
```
This is where the main html page is
```
  
-- src> App.js --  
```
import logo from './logo.svg';
import './App.css';

function App() {. <-- we export this function
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
``` 
### Build a First Custom Component
To create a new component, We follow a component tree in react. 
-- src>components>ExpenseItem.js ---
```js
import './ExpenseItem.css'

function ExpenseItem() {
 return <div className="expense-item"><h2>Expense item!</h2></div>
}

export default ExpenseItem;
```

Importing component into App.js. 
-- src>App.js---  
```js
import ExpenseItem from './components/ExpenseItem';
import Exp

<ExpenseItem></ExpenseItem> //Make sure its uppercase so react can detect its custom component. 
```
-- src > components> ExpenseItem.css --
```css
.expense-item{
 width:15px;
}

```
### Writing more complex code. 
Using the code>preference>Format Document ( To prettify the code)
```
up_arrow + Option + F // to prettify ur code. 
```
### Adding Basic Styling
### Outputting Dynamic Data 
```
function ExpenseItem(){
  const expenseDate = new Date(2021,2,28)
  
  return (
    <div className = "expense-item">
      <div> { expenseDate.toISOString() }</div> // JSX: How we use js code..
      <div className="expense-item__decription'>
      </div>
    </div>
  )
}
```
### Passing Data via "Props"
-- src > App.js --
```
const expenses = [
 {
    id:'e1',
    title: 'Toilet Papper'
 },
 {
    id:'e2',
    title: 'Car insurance'
 }
]

<ExpenseItem title= {expenses[0].title} ></ExpenseItem>
```

-- src>components> ExpenseItem.js --
```
function ExpenseItem(props){

return ( 
<div>
{props.title}
</div>
}
```
### Adding normal js to components
### Splitting components into multi-smaller components
### The Concept of "Composition" ( "children props")
https://realpython.com/inheritance-composition-python/. 
Composition : A car **has a** engine, has a steering wheel. 
Inheritance: A sportscar **is a** car. 
  
Card adds like a wrapper. 
```
function Card(props){
  const classes = 'card' +props.className;
  
  return <div className={classes}> {props.children} </div>
}

export default Card;

-- App.js--
<Card>
  <ExpenseItem></ExpenseItem>
  <ExpenseItem></ExpenseItem>
</Card>
```

### A First Summary
### A Closer Look at JSX
### Arrow Function 
```
const App=()=>{
}
```
## Section 4: React State & Working with Events
