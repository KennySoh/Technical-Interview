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
### An Alternative to Computed Properties: Watching for Changes
```
watch:{
 counter:function(value){
  setTimeout(function(){
   vm.counter = 0;
  }, 2000);
 }
}
```
### Saving Time with Shorthands
```
v-on:click 
@click //shorthand

v-bind:href
:href //shorthand
```

### Dynamic Styling with CSS classes - Basics
```
---css---
.red{ background-color: red; }

---js----
data:{
 attachRed: false
}

---html---
<div id="app">
 <div class="demo" @click="attachRed = !attachRed" :class="{red:attachRed}"></div> 
</div>
```
### Dynamic Styling with CSS classes - Using Objects
```
computed:{
 divClasses: function(){
  return {
   red: this.attachRed,
   blue: !this.attachRed
  };
}
---html---
<div id="app">
 <div class="demo" @click="attachRed = !attachRed" :class="divClasses"></div> 
</div>
```
### Dynamic Styling with CSS classes - Using Names
```
----puting class Names directly----
<div class="demo" :class="color"></div>

<input type="text" v-model="color">
----a list into class----
<div class="demo" :class="[color,{red:attachRed}]">  // if color is green, shows red if attachRed=true... applies both class

<input type="text" v-model="color">
```

### Setting Styles Dynamically( without CSS classes)
```
--- 1. directly injected style----
<div class="demo" :style="{'background-color'}"></div>

---2. directing to a computed style---
<div class="demo" :style="myStyle"></div>

computed:{
 myStyle:function(){
  return {
  backgroundColor: this.color,
  width: this.width + 'px'
  };
 }
}
```
### Styling Elements with the Array Syntax 
```
---3. combination of parsing styles---
<div class="demo" :style="[myStyle, {height: width + 'px'}]"></div>

computed:{
 myStyle:function(){
  return {
  backgroundColor: this.color,
  width: this.width + 'px'
  };
 }
}
```
# Conditionals & List
### Conditional rendering with v-if
```
<p v-if="show">You can see me! </p>
<p v-else>Now you see me!</p>
```
### Using an Alternative v-if Syntax
```
---grouping multiple elements but doont use div---
<template v-if="show"> 
 <h1> Heading </h1>
 <p> Inside a template </p>
</template>
```
### Dont Detach it with v-show
```
<p v-show="show"> do u see me </p> #This results in display: none, elements are rendered but not displayed... 
                                   #v-if is more efficient because it remove entirely from dom
```
### Rendering Lists with v-for
```
<ul>
 <li v-for ="ingredient in ingredients">{{ ingredient }}</li>
</ul>
```
### Getting the Current Index
```
<ul>
 <li v-for ="(ingredient,i) in ingredients">{{ ingredient }} {{ i }}</li>
</ul>
```
### Using an Aleternative for v-for syntax
```
<template>
 <h1>{{ ingredient }}</h1>
 <p>{{ index }}</p>
</template>
```
### Looping through Objects
```
<li v-for="person in perons">
 <div v-for="(value,key) in person">{{ key }}:{{ value }})</div>
</li>

<li v-for="person in perons">
 <div v-for="(value,key,index) in person">{{ key }}:{{ value }}({{ index }})</div>
</li>
```
### Looping through a List of Numbers
```
<span v-for="n in 10">{{ n }}</span>
```
### Keeping Track of Elements when using v-for 
```
<ul>
 <li v-for="(ingredient, i) in ingredients">{{ ingredient }} ({{ i }}) </li>
</ul>
<button @click="ingredients.push('spice')">Add New</button> 
```
