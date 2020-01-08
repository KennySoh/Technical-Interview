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
<h1 v-once > {{ title }} </h1> //preventing this from re-rendering if data.title changes down the road
### How to Output Raw HTML
<a href="http://google.com">  
{{ finishedLink }} , defaults renders text form ... This behaviour prevents xss attacks  
  
### 
