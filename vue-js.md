### Lets Create our first vue instance
### Setup locally
# Using vue instance to interact with the DOM
### Understanding VueJS Templates
vue take the html {{ title }} and renders a final html that get rendered in the browser
### How the VueJS Template Syntax and Instance Work Together
### Accesing Data in the Vue Instance
this.title anyway in the vue instance -> data{title:"Hello World!"}
### Binding to Attributes
cant use src="{{ link }}" in html attribute.... have to bind it, v-bind:href="link"
### Understanding and Using Directives
### Disable Re-rendering with v-once
```
<h1 v-once > {{ title }} </h1> //preventing this from re-rendering if data.title changes down the road
```
### How to Output Raw HTML
```
<a href="http://google.com">  
{{ finishedLink }} , defaults renders text form ... This behaviour prevents xss attacks  

<p v-html="finishedLink"></p> # allow raw html to be rendered careful of XSS cross site scripting attacks.
```
### Listening to Event 
```
v-on:click="increase" # onClick html event
```
### Getting Event Data from the Event Object
```
<p v-on:mousemove="updateCoordinates">   #html event is automatically passed down into function
 
methods:{
  updateCoordinates:function(event){
    this.x = event.clientX;
    this.y = event.clientY;
  }
}
```
### Passing your own Arguements with Events
```
<button v-on:click="increase(2)"> Click Me </button>  #html event is automatically passed down into function
<button v-on:click="increase(2,$event)"> Click Me </button>

methods:{
  increase: function(step){
  }
  increase: function(step,event){
  }
}
```
### Modifying an event with Event Modifiers
```
<span v-on:mousemove.stop>
<span v-on:mousemove.prevent> 
```
### Listening to Keyboard Events
```
<input type="text" v-on:keyup.enter.space="alertMe"> # when key up both "enter" and "space", runs alertMe function

```
### Writing Javascript Code in Templates
```
# Only can be in a single line , but not recommended
<button v-on:click="counter++">Click me</button> ## automatically increment counter js code
<p>{{ counter * 2 > 10 ? 'Greater than 10' : 'Smaller than 10' }} </p> # turnary expression
```

### Using Two-Way-Binding
```
<input type= "text" v-model="name">
<p>{{ name }}</p>
```

### Reacting to Changes with Computed Properties 
Computed properties will only change if the data it uses changes
```
computed:{
 output: function(){
  return this.counter > 5 ? 'Greater 5' : 'Smaller than 5';
 }
},
```
