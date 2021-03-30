
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
```js
---person.js----
const person={
  name:'Max'
}

export default person
```
```js
---utility.js---
export const clean =()=> {...}
export 
```
### 
