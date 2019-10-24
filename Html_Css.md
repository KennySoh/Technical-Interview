# Html

Think of everything as boxes  
  
```html
<!doctype html>
<html lang="en">
  <head>
    <!-- MetaTags for seo/ Css stylesheets-->
    <meta charset="utf-8">
    <title>Jane Smith's Profile</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <link href="https://fonts.googleapis.com/css?family=Muli%7CRoboto:400,300,500,700,900" rel="stylesheet">
  </head>
  <body>
    <!-- Normally Split into 3 Header/Main/Footer-->
    <header>
    <main>
    <footer>
  </body>
</html>
```
## Basic Web Page
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Kenny's Resume</title> 
    <link rel="stylesheet" href="resume.css">
  </head>
  <body>
    <img src="http://placeimg.com/200/200/any" alt="kenny webdeveloper">
    <h1>Treasure Porth, Web Developer</h1>
    <h2>Summary of Qualification</h2>
    <ul>
      <li>Experience as freelance developer</li>
      <li>Experience with Html,Css and Javascript</li>
      <li>Bachelor of Science, Economics</li>
    </ul>
  </body>
</html>
```
## Image Tag
```html
<!-- Html Tags <img>,  Attributes (src, alt, class)-->
<img src=images/portland.jpg alt="Drawing of Kenny" class="profile-image">  
```
Adding Caption to image: Use **figure** & **figcaption**
```html
<figure>
  <img src="moon.jpg">
  <figcaption>Explanation of moon</figcaption>
</figure>
```
## Paragraph Tag
```html
<p>This is a paragraph.</p>
```
## Link Tag
```html
<a href="#top">Anchor text, clickable</a>

<!--Image Link-->
<!--(target="_blank") sends to new tab-->
<a href="http://twitter.com/treehouse" target="_blank">
  <img src=images/portland.jpg alt="Drawing of Kenny" class="profile-image"> 
  </img> 
</a>
```
## Ordered & Unordered List 
```html
<ol>
  <li></li>
  <li></li>
</ol>


<ul>
  <li></li>
  <li></li>
</ul>
```

## Adding section tags, article, nav, aside
**section** tags to better structure different major section, each section should follow with <h1-9> tag to describe what the section is about  
**article** tags to seperate items in major sections  
nav tags markups for major links groups.   
**aside** for stuff that appears in the page like side bar  
**div** tag only when article or aside tag is not appropiate
```html
<!--Used to structure content in body-->
<section>
  <h2>Vr Articles</h2>
  <article>
    <h3> How the school uses Vr</h3>
    <p>loresum this is my first article>
  </article>
  <!--Used to structure articles in body-->
  <article>
    <h3> How the army uses Vr</h3>
    <p>loresum this is my secind article>
  </article>
</section>
  
<section>
  <h2>Financial Article</h2>
</section>

<!--nav to markup major links groups-->
<nav>
  <ul>
    <li><a href="cakes.html">cakes</a></li>
    <li><a href="cakes.html">cakes</a></li>
    <li><a href="cakes.html">cakes</a></li>
  </ul>
</nav>

<!--aside for sidebars or things not related to main content of page -->
<aside>
</aside>
```

## One Main Tag, Can have Multiple Header and Multiple Footer Tag
Example of splitting body
```html
<!DOCTYPE html>
<html>
  <head>
    <link href="styles.css" rel="stylesheet">
    <title>My Portfolio</title>
  </head>
  <body>
    <header>
      <nav>
         <ul>
          <li><a href="#">About</a></li>
          <li><a href="#">Work</a></li>
          <li><a href="#">Contact</a></li>            
        </ul>
      </nav>
      <h1>My Web Design &amp; Development Portfolio!</h1> 
      <p>A site featuring my latest work.</p>
    </header>
    </main>
      <section>
        <h2>Welcome</h2> 
        <p>Fusce semper id ipsum sed scelerisque. Etiam nec elementum massa. Pellentesque tristique ex ac ipsum hendrerit, eget feugiat ante faucibus.</p>
        <ul>
          <li><a href="#">Recent project #1</a></li>
          <li><a href="#">Recent project #2</a></li>
          <li><a href="#">Recent project #3</a></li>     
        </ul>
      </section>
    </main>
    <footer>
      <p>&copy; 2017 My Portfolio</p>
      <p>Follow me on <a href="#">Twitter</a>, <a href="#">Instagram</a> and <a href="#">Dribbble</a></p>
    </footer>
  </body>
</html>
```
## Block Quote Tag
```html
<blockquote>
  Some quote 
  <footer>
    <cite><a href="somesource.html"> Mark Zuckerberg</a></cite>
  </footer>
</blockquote>
```
Take note you can use multiple footer and header. Eg. Each article has a header/ footer
But you only can have one main tag.

## Creating breaks in content 
```html
<br> <!--Line Break: Similar to Enter Key in words-->
<hr> <!--Horizontal line: Normally to seperate different sections/topics-->

<strong></strong> <!--Bold the word: Emphasize importance-->
<em></em> <!--Italize-->
<small></small> <!--For Copyrights or shortruns of tags-->
This is <span>a sentence</span> <!--For Inline Elements you like to style with css-->
<div>This is a sentence</div><!--For Block Level Elements you like to style with css-->
```

## Linking to Sections of a Web Page
back to top link & in page links  
```html
<a href="#about"> </a>
<a href="aticle.html#contact-us"></a>  
  
<section id="about"></section>
<section id="contact-us"></section>
```
## File Paths
```html
<a href="../css/aticle.html#contact-us"></a> <!-- relative path: navigating from current directory-->
<a href="/article.html"> <!--"/" root relative path-->
<a href="https://github/article.html"> <!--"/" absolute relative path-->
```

## Email link with email automatically filled
```html
<!-- This opens the default email app and auto fills email and subject. %20 = "space"-->
Email<a href="mailto:cool@gmail.com?subject=Hi%20There!">cool@gmail.com</a>
```

## HTML Entities & Reserved Charaters 
use Html Entities (&Entity;) to display reserved characters. 

```html
&lt; "<" 
&gt; ">"
&amp; "&"
&copy; "Copyright symbol"
&nbsp; "spacebar"
```
ref: https://dev.w3.org/html5/html-author/charref


# CSS
```css

/* Stying by element, class , id */
h3 {
  color:red;
}
.main-nav{
  width: 100%;
  text-align: solid black 3px;
  border: solid black 3px;
  border-radius:10px;
}

#id{
  color: maroon;
  letter-spacing:2px;
}
```
Each {} is a css rule.  
Each rule begins with a selector (eg. main-nav)  
'width','color' are known as css properties

margin outside, padding inside  
  
reference: css-tricks.com  
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
https://webplatform.github.io/docs/css/properties/padding-top/

## Inline Style & Internal Style & External Style Sheets & Import
Ideally not, does not seperate html and css.. overides all other styles
```html
<!--Inline Style-->
<body style="background-color: orange;">
```
Useful only for smaller sites, not ideal as css remains in html. 
```html
<!--Internal Style-->
<head>
  <style>
    p{
      font-size:20px;
      font-weight:bold;
    }
```
Most Ideal, Using external stylesheet. Stylesheet is cache by the browser, so only have to download once. 
```html
<head>
  <link rel="stylesheet" href="css/style.css">
```
```css
body{
  text-align:center;
}
h1{
  font-size:72px;
  color:white;
}
```
via Import from html
```html
<head>
  <style>
    @import "css/import-styles.css"
```
via Import from css
```css
@import "css/import-styles.css"
```

## Descendant Selectors & Pseduo-Classes
```css
/* Span inside Header*/
header span{
}

/* Pseduo-Class*/

a:link{ /* Only for links with href*/
  color:orange;
}
div:visited{}
p:hover{}
a:active{/*mouse pressed*/}
a:focus{/*on tab*/}
}
```
## Comments
```css
Comments
/*Type Selector*/
/*Class selector*/
/* This makes our header orange */
```

## Common Datatypes
```css
color: datatypes (orange,tomato,blue);
font-size:
images
gradient
```
datatypes references: https://developer.mozilla.org/en-US/docs/tag/CSS%20Data%20Type

### Length
Relative vs Absolute
```
Absolute
width:260px; (Now, It represents cm instead of actual pixels, since many screens have different pixel-density)

Relative
width:50%;
font-size:150%;

1em relative to parent's font-size, default 16px;
width:1em; /*pixel to em: (X px/ 16px) */
Take note: Compounding multiple parent sizes. 

1rem relative only to root element html element of 16px. 
```
### Color
```
orange
#ffaa00
rgb(255,255,255) - white
rgba(255,199,73,.4)
```

### Text Styles
```
text-align: center, right, left;
text-transform: uppercase, lowercase, capitalize;
text-decoration: none, underline;
font-weight: normal,bold,lighter,bolder, 100(Take note, numeric value:100-900);
font-family: "Helvatica nue", Arial, sans-serif; ( Take note: web safe fonts declared at the end as backup)
line-height: 1.5;(Vertical spacing between lines)

font: normal 1em/1.5 Helvatice; (font-weight, text-size, line-height, font family)
```
web save font: https://www.cssfontstack.com/

### CSS Box Model
Block vs Inline  
Margin>Border>Padding>Content  
```css
/*Padding*/
padding-top:100px;
padding-right:100px;
padding-bottom:100px;
padding-left:100px;

padding: 100px 120px 200px 120px;(Top Right Btm Left)

/*Border*/
border-width: 10px;
border-style: solid dotted; (Top&Btm Sides)
border-color: red #ffa949 blue green; (Top Right Btm Left)
border-bottom-style: dotted; (Overwrites)

border:2px dotted tomato;

/*Margins*/
margin:105px;
margin:auto; (equal margin left and right)

/* Display*/
dispaly: none, block, inline, inline-block;
```
### CSS Basics

#### Width and Height
```
width:100px;(only for content)

box-sizing:border-box ( can be used in universal selector) 
width:75%px (for content and padding and borders)
max-width:100px(Limits to 100px)
```
#### Backgrounds: Color and Images
```
background-image:url('img/mountains.jpg');
background-size:40%, cover;
background-repeat:repeat-x, repeat-y,no-repeat;
background-color:#ff4add;
background-position:center top,20% 50%;

background:#ff4ad url('img/image.jpg');
```
#### Floats
```
float:right;
float:left;

if a block element contains floated children, its height will collapse.

1st method
overflow:auto;

2nd better method (Clear Fix)
.group:after{
  content:"";
  display:table;
  clear:both;
}
```
#### Lists
```css
ul{
  list-style-type:square;
}
ol{
  list-style-type:decimal-leading-zero;
}
```

#### Text Shadows
```
text-shadow:5px 8px 0 #222; (right btm blur color)
box-shadow:15px 15px 10px -5px rgba(0,0,0,.8);(right btm blur spread color)
box-shadow:inset 15px 15px 10px -5px rgba(0,0,0,.8); (inner shadow)
```

#### Border Radius
```
border-top-left-radius:50px;
border-top-right-radius:50px;
border-bottom-right-radius:50px;
border-bottom-left-radius:50px;

border-radius: 50px 10px 10px 50px; 
border-radius:50% (Circle) 
```

#### Gradients
```
background-image:linear-gradient(0deg, #ffa949, firebrick); default: Top->Btm (to top)
background-image:radial-gradient(circle,#ffa949,firebrick);
background-image:radial-gradient(circle at top right,#ffa949,firebrick);
background-image:radial-gradient(circle at top right,#ffa949 0%,firebrick 50%,dodgerblue 100%);
```

Transparent Gradients and Multiple Background
```
background: linear-gradient(#ffa949, transparent 90%),
            linear-gradient(0deg,#fff,transparent),
            #ffa949 url('../img/mountains.jpg') no-repeat center;
```

#### Importing Web Fonts with @font-face
@font-face{
  font-family:'Abolition Regular'; (Whatever you want)
    src: url('../fonts/abolition-regular-webfont.eot'); (IE)
    src: url('../fonts/abolition-regular-webfont.eot?#iefix') format('embedded-opentype'), (Older IE)
       url('../fonts/abolition-regular-webfont.woff') format('woff'), (Mozilla, all browsers)
       url('../fonts/abolition-regular-webfont.ttf') format('truetype'); (Safari, Android, IOS)
  
}

#### Media Query Basic (For different screen sizes)
```css
@media (max-width:960px){ (Viewport at or below:960px)
}
@media all(max-width:480px){ (Viewport at or below:480px, all is default)
}
@media( min-width:481px) and (max-width:700px){
}
```

```css
@media(max-width:1024px){.secondary-content{width:90%;}}
@media(max-width:768px){.secondary-content{width:100%;padding:20px;border:none;}}
```
Ensuring Iphones can have media queries
```html
<meta name="viewport" content="width=device-width">
```

#### Cascade :Importance  
1 User Agent styles, 2 User styles , 3 Author styles (Our Css is here)  
#### Cascade:Specificity and Source Order  
#id> .class  
inline> external style sheet  
Source order.. Last one takes effect  
#### Inheritance
css elements are inherited by parents
```
color:initial; (The parent's parent's value 
```
## CSS Layout
Normalise.css, Ensure all browsers are similar. (Overriding individuals user agent style sheet)  
https://necolas.github.io/normalize.css/8.0.1/normalize.css  
  
### Using Wrappers
A wrapper is commonly used to center a layout on the page. The wrapper keeps a layout from looking too wide or too narrow depending on the devie or viewport width. 
```
1st method: Using exiting wrappers
<body>
body{width:70%;margin:0 auto;} // Width prevents from going too wide, margin centers the wrapper

2nd method: Using div element
<div class="wrapper">
.wrapper{width:70%;margin:0 auto;}
```
### Full-wdith headers
```
<header> <footer>         {width:100%}
<div class="container">   {width:70%;margin:0 auto;}
```
### Vertical Margin Collapse but not Horizontal Margin
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/VerticalMargin.png)

### Creating a Mobile First Layout
Basic styles are served to mobile devices by default and then gradually adjusted for wider screens. 
```
/*Smaller than 769px will use the rest of the css*/
.container{padding:1em;}

/*Media Queries*/
@media (min-width:769px){
  .container{width:70%;margin:0 auto;max-width:1000px;}
}
```
### Creating a Sticky Footer
a footer that sticks to the btm of the page
```
<div class=wrap>     wrap everthing except footer
<footer>

.wrap{min-height:calc(100vh-89px);}          set it to 100% of view port minus height of footer(inspect tool)
```
### Positioning Elements Side by Side with inline Display.
```
display:inline;       (Browser will not apply width or height/ Top or Btm settings )
display:inline-block; (Can apply width or height/ Top or Btm settings )

Making inline,links hover the whole box
.main-nav a{display:block;padding:15px 10px;} (make them as wide as parent element)
```
### How Float Works
Typically, Contents (Inline and Block) are disaplayed in the Normal Document Flow (HTML Markup).  
Float gets taken out of Normal Document flow and shifted to left and right side of the documents.  
  
Normal Document Flow
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/NormalDocumentFlow.png)
  
Float
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Float.png)

#### Wrap Text Around Images. 
```
.img{
  float:right;
}

Text flows around image, Image is taken out of normal document flow. 
Technically a block element: Accepts width/height and top/btm values. 
But behaves like a inline element, because doesnt exist on a line on its own. 

Creating space need to add margins on the floated item. Adding on text that surrounds the image will not work because paragraph is in normal document flow and floated item is not. 
.img{
  float:right;
  maring:10px;
}
```
#### Creating a Horizontal Navigation with Float
```
.name{
  float:left;
}

.main-nav{
  float:right;
}
.main-nav li{
  float:left;
}

// Block-level containing height collapses
1) Give a fixed height
2) Setting overflow: auto or hidden; (contents will be hide)
3) .clearfix::after{ content:"";display:table;clear:both;}
```

### Css Layout: Absolute Positioning
 ```
 /* Taken out of normal document flow */
 position:absolute;
 top:0; (6em, 6% in relation to viewport)
 left:0;
 
 .main-header{
  position:relative; (all absolute position are now relative to class: .main-header)
}
 ```
 #### Creating an image Caption with Absolute Positioning
 Absolute Elements will always be relative to the first parent with position:relative  
 
 ```html
<!-- Featured image (normal flow)-->
<figure>
  <img class="feat-img" src="img/treats.svg" alt="Drinks and eats">
  <figcaption>
    <h4>Featured Drinks &amp; Eats!</h4>
    Croissant macaroon pie brownie cookie marshmallow liquorice gingerbread caramels toffee
  </figcaption>
</figure>
 ```
 ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/AbsolutePosition1.png)  
   
   
 ```html
  <!-- Featured image (Absolute Positioning)-->
  <figure>
    <img class=ïcon-location" src"img/location.svg" alt="Location">
    <img class="feat-img" src="img/treats.svg" alt="Drinks and eats">
  <figcaption>
    <h4>Featured Drinks &amp; Eats!</h4>
    Croissant macaroon pie brownie cookie marshmallow liquorice gingerbread caramels toffee
  </figcaption>
</figure>
 ```
 ```css
 figure{
  position:relative
 }
 figcaption{
    position:absolute;
    btm:0;
    width:100%; 
 }
 .icon-location{
    width:35px;
    position:absolute;
    top:-15px;
    right:-15px;
 }
 
 ```
  ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/AbsolutePosition2.png) 
  
### Css Layout:Fixed Positioning
```css
  .main-header{
    position:fixed;
    background:#fff;
    box-shadow: 0 1px 4px rbga(0,0,0,.4);
    width:100%;
    top:0;
  }
```

  ![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FixedPosition.png) 
 
### Z-index
Stacking order of Overlapping Absolute or Fixed position elements.
```css
/* Higher z-index is on top. main-header will be on top*/
.main-header{
  z-index:1000;
}
.icon-location{
  z-index:1;
}
```
 
# HTML & CSS Validators
background-color:#ff4add;
html validator: https://validator.w3.org/nu/#textarea  
css validator: https://jigsaw.w3.org/css-validator/validator  

# HTML Forms
## HTML Tables
Static Table without a database
```html
// th tells web crawlers its headers.
//scope="col" or "row", tells web crawler th is related to row or col items. 
<table>
  <tr>
    <th scope="col">Name</th>
    <th scope="col">Email</th>
    <th scope="col">Job Role</th>
  </tr>
  
  <tr>
    <th scope="row">Kenny</th>
    <td>ks.kennysoh@gmail.com</td>
    <td>Web Developer</td>
  </tr>
  
    <tr>
    <th scope="row">Thomas</th>
    <td>thomas@gmail.com</td>
    <td>Developer</td>
  </tr>
</table>
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/HTMLTable1.png) 
```html
//thead helps styling and good for to tell search engine
// tbody and tfoot
//caption
<table>
  <caption>Employee Information</caption>
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Job Role</th>
    </tr>
   </thead>
   <tfoot>
     <tr>
       <td colspan="3">Data is updated every 15min</td>
     </tr>
   </tfoot>
   <tbody>
    <tr>
      <th scope="row">Kenny</th>
      <td>ks.kennysoh@gmail.com</td>
      <td>Web Developer</td>
    </tr>

    <tr>
      <th scope="row">Thomas</th>
      <td>thomas@gmail.com</td>
      <td>Developer</td>
    </tr>
  </tbody>
</table>
```
## HTML Forms
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/HTMLForm1.png) 
```html
//1) action is the link for the method to post/get to
//2) input type->text,email,password | id->css,js,associate label with form control | name->serverside understanding
//3) Textarea
//4) Submit Button
//5) Label for="name" links with input id="name" | When click directs to input="name"
//6) Fieldset and legends | Organize form control into logical groupings
//

<form action="index.html" method="POST">
  <h1>Sign Up</h1>
  <fieldset>
    <legend><span class="number">1</span> Your basic info</legend>
    <label for="name">Name:</label>
    <input type="text" id="name" name="user_name"> 

    <label for="email">email:</label>
    <input type="email" id="email" name="user_email"> 

    <label for="password">Password:</label>
    <input type="password" id="password" name="user_password"> 
  </fieldset>
  <fieldset>
    <legend><span class="number">2</span> Your profile</legend>
    <label for="bio">Biography:</label>
    <textarea id="bio" name="user_bio"></textarea>
  </fieldset>
  <button type="submit">Sign Up</button>
</form>
```
### HTML Forms: Select Menus & Radio Buttons & Check Boxes
```html
//7) Select Menu: Drop down list to select options
<form action="index.html" method="POST">
  <h1>Sign Up</h1>
  <fieldset>
    <label for="job">Job role:</label>
    <select id="job" name="user_job">
      <optgroup label="Web">
        <option value="frontend_developer">Front-End Developer</option>
        <option value="php_developer">PHP Developer</option>
      </optgroup>
    </select>
  </fieldset>
  
//8) Radio Buttons (Can put <br> after each input)
  <label>Age:</label>
  <input type="radio"  id="under_13" value="under_13" name="user_age"><label for="under_13" class="light">Under 13</label> 
  <input type="radio"  id="over_13" value="over_13" name="user_age"><label for="over_13" class="light">13 or Over</label>
  
//9) Checkboxes
    <label>Age:</label>
  <input type="checkbox"  id="under_13" value="under_13" name="user_age"><label for="under_13" class="light">Under 13</label> 
  <input type="checkbox"  id="over_13" value="over_13" name="user_age"><label for="over_13" class="light">13 or Over</label>
  
  
  <button type="submit">Sign Up</button>
</form>
```
https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms

# CSS Selectors
## Attribute Selector: Class , For, Name
```css
// .form-contact and #container are more efficient
[class]{
  color:red
}
[class="form-contact"]{
  color:red
}
form[class="form-contact"]{
  color:red
}
div[id="container"]{
  max-width:1800px;
}

//Attribute selector are handy when trying to select non-class or id attributes. (Example forms)
input[type="text"]{
  background:red;
}
input[placeholder]{
  background:red;
}

//Styling buttons
input[type="button"],
input[type="reset"],
input[type="submit"]{
  cursor:pointer;
}

a[target="_blank"]{
  color:#39add1;
  text-decoration:none;
  border-bottom:1px dotted;
}
```
## DRY: Dont Repeat Yourself
For maintability if possible try not to repeat code, apply class to multiple elements. 
```css
/* DRY Classes*/
//Can be applied to anything that wants to be rounded
.br{
  border-radius:.5em;
}
.avatar{
  display:block;
  margin:0 auto 2em;
}
.rounded{
  border-radius: 50%;
}

//applied to any form btns
.btn{
  cursor:pointer;
  font-size:.85em;
  font-weight:400;
  color:#fff;
  padding-left:20px;
  padding-right:20px;
  text-transform:uppercase;
}
.default{background-color:#52bab3;}
.error{background-color:#ff784f;}

@media(min-width:769px){
  .inln{
    width:auto;
    display:inline-block;
  }
}
```
```html
<img class="br avatar rounded">
<input class="btn default inln">
```
## Child, Adjacent, and General Sibling Combinators
> , + , -
```css
/*Combinators*/

//Child
form>a{ //direct child
}
//Adjacent(Immediately following) Siblings
div + p { //selects all <p> elements that are placed immediately after <div> elements:
  background-color: yellow;
}
//General Siblings
div ~ p { //selects all <p> elements that are siblings of <div> elements: 
  background-color: yellow;
}
```
## :first-child and :last-child
```css
.main-nav li:first-child{
  border:none;
  border-radius:5px 0 0 5px;
}

.main-nav li:last-child{
  border:none;
  border-radius:0px 5px 5px 0px;
}

```
## :only-child and :empty
```
<li>Item2<span>&check;</span></li>
<li></li>
<li>Item6<span>&check;</span></li>

:only-child{ //targets elemnts which are the only child. 
}
:empty{//making sure theres no empty html tags/ or when something returns empty.
}
```

## :nth-child & nth-of-type
```
li:nth-child(even){}
li:nth-child(odd){}
li:nth-child(1){//target the first element}
li:nth-child(an+b){}
li:nth-child(2n+3){//select item3 , then item5, item7 ....}
li:nth-child(-n+3){//select item3 ,item2,item1}

div:nth-child(4){//targets only the 4th child, so if 4th child is a h1,fails}
div:nth-of-type(4){//targets the 4th div}
```

## :root & target
```css
:root{ //why not just use html{} because markup can be svg and xml, 
       //root pseduoclass might be different from html{}
}

// When <a href=#somewhereonpage> is clicked, its targeted
// http://yourwebsite.com/#somewhereonpage
:target{ 
  background:#384047;
}
#col-c:target{background:red}
```
## :not() - The Negation Pseudo-Class
```css
div:not(#col-a){ //target all div but not the #col-a}
div:not([type="submit"]){//target all div but not type=submit}
```

## Pseudo-Elements-::first-line , ::first-letter and ::before , ::after
```css
.intro:first-line{ //the first line }
.intro:first-letter{ //the first letter }

.jpg::before{
   content:"JPG - "; //insert "JPG -" before .jpg
   content: url(../img/icn-zip.svg); //insert images before .jpg
}
.jpg::after{
   content:"JPG - "; //insert "JPG -" after .jpg
   content: url(../img/icn-zip.svg); //insert images after .jpg
}

h1::before,
h1::after{
  content:"";
  display:inline-block;
  width:24px;
  height:24px;
  border-radius:50%;
  background:coral;
  margin:0 10px;
}
```
## The atr() CSS Function
Displays the attribute value.
```css
.d-loads a::after{
  content:attr(title);
}
```
## Substring Matching Attribute Selectors- "Begin With","Ends With", "Contains"
Begins With ^
Ends With $
Contains *
```css
a[href^="http://"]{
  color: #52bab3;
  text-decoration:none;
  background-repeat:no-repeat;
  background-size:18px 18px;
  padding-left:25px;
}
a[href$=".pdf"]{background-image:url('../icn-pictures.svg'};
img[src*="thumbnails"]{}
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/SubstringMatching1.png) 

## Element States Pseudo-Classes
```css
:disabled{ // disabled form elements, with a light grey background
}
input[type="checkbox"]:checked + label{ //onced a check box is checked, adjacent label is bold;
  font-weight:900;
}
```
# CSS Flexbox
Flexbox is a remarkable layout feature, that better than float and disaply:inline. 
## Flexbox Basics and Terminology
### Flex Container & Flex Item
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox1.png)
### Main Axis & Cross Axis
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox2.png)
### Creating a Flex Container
```html
<div class="container">
  <div></div>
  <div></div>
  <div></div>
</div>
```
```css
// Flex Items stretch to fill the Flex container height. Cross axis start to end
 .container{
  display:flex;
  height:300x;
}

 .container{
  display:inline-flex;
  height:300x;
}
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox3.png)
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox4.png)

### Controlling the Direction of Flex Items & Wrapping Flex Items & justify-content(space between items, main axis)
Only apply to flex container.
```css
.container{
  display:flex;
  flex-direction: row; <- default(row-reverse, column, column-reverse)
  flex-wrap: wrap; //Wrapping Flex Item, Goes to next line. 
  
  //Fills the space after margin and padding is accounted.
  justify-content: flex-end; (center, space-between, space-around.)
  }
  
.item1{
  margin-right:auto; ( Makes item1 flush to the left and items flush to the right. aong with justofy content)
}
```
### Changing the order of flex items
```css
.container{
  display:flex;
 }
.item-6{
  order:-1; (default is 0, this makes item6 displayed first)
  order:1; ( this make item6 displayed last)
}
```
### Growing Flex Items
flex item to fill up the container.  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox5.png)
```css
.item{
  flex-grow:1; default->0 
}
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox6.png)
```css
.item3{
  flex-grow:3;
}
```
### Smarter Layouts with flex-basis and flex
```
.item{
  flex-grow:1; default->0 
  flex-basis:200px; (min-width of 200px, next line if smaller)
  
  flex: 1; (flex-grow, flex-basis, flex-shrink) - shorthand property,automatically sets the rest to 0;
}
```

### Aligning Flex Items on the Cross Axis
```
.container{
  display:flex;
  align-items:stretch; <-default (flex-start,flex-end,center)
}
```
### Vertical and Horizontal Centering
```css
//1st way
.container{
  displat:flex;
  min-height:50vh;
  
  justify-content:center;
  align-items:center;
}

//2nd way
.container{
  displat:flex;
  min-height:50vh;  
  justify-content:center;
}
.item{
  align-self:center;
}

//3rd way
.container{
  displat:flex;
  min-height:50vh;
  
  margin:auto;
}
```
## Flexbox Examples
1) Building a Navigation Bar with Flex Box (.main-header,.main-nav)  
2) Creating a 2 col layout (.row, .col,.primary)  
3) Creating a 3 col layout (.row, .col,.primary)
```css
@media(min-width:769px){
  .main-header,.main-nav,.row{
    display:flex;
  }
  
  .main-header{
    flex-direction:column;
    align-item:center;
  }
  .col{
    flex:1; //2col  
    flex:1 50%; //2col but 3col in 1025px
  }
  .row{
    flex-wrap:wrap;//2col but 3col in 1025px
  }
}
@media(min-width:1025px){
  .main-header{
    flex-direction:row;
    justify-content:space-between;
  }
  .primary{
    flex:2;//2col
    flex:1.4;//3col in 1025px
  }
  .col{
  flex-basis:0;//3col in 1025px
  }
}
```
### Aligning "Learn More" btn to btm of col
```css
.col{
  display:flex;
  flex-direction:column;
}
.button{
  margin-top:auto;
  align-self:flex-end;
}
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/FlexBox7.png)

### Creating a sticky footer with FlexBox.
```css
body{
  display:flex;
  flex-direction:column;
  min-height:100vh;
}
.row{
  flex-grow:1;
}
```
# CSS Transitions and Transforms
## Creating Your First Transition with transition-duration
Transitioning CSS properties  
***
1) List the properties to transition
2) Define how long the transition should tkae
3) Set an optional delay and change in speed
***
```
Transitioning a property (state change)
1. Start value
2. End value

.photo-container{
  background:lightblue;
  transition-duration: 1s,0.4s; //takes a second to fade to blue or back to red. default to all properties. 

  //Transitioning Specific Properties with transition-property
  transition-property: background, color; (Defauly is all not ideal, overhead to check)
  
  //Control a Transition's Start Time with transition-delay
  transition-delay:2000ms;
  
  //Change a Transition's Speed with Timing Funcitons
  transition-timing-funciton:ease; ( linear, ease-in, ease-out, ease-in-out)

  //transition Shorthand
  transition: opactity .3s ease-out .2s, background .4s linear .3s; //properties,duration,timing, delay
  transition:all .5s;
}
.photo-container:hover{
  background:red;
}
.photo-container:active{
  background:darkred;
}
```
## Animatable CSS properties
If a CSS property, has an identifiable halfway point, it can accept a transition.
https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties

## Transformation
```
2d Transform
img{
  transition:transform 0.5s;
}
img:hover{
  transform:rotate(-5deg);
  
  //Other transformation
  transformation:skewX(10deg) 
  transformation:skewY(10deg)
  transformaiton:scale(1.1) //(x,y) :(2,1.5)
  
  transform-origin:50% 50%; // default transforms relative to center. 0 0 :topleft, bottom right;
  
  //Moving Content with translate()
  transform: translateX(150px);
  transform: translate(50%, 50px);
  
  //Combining Transforms
  transform: rotate(-5deg) scale(1.1) translateY(-20px);
}
```
### Making a Slide Transition
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Translation1.png)
```
.slide .photo-overlay,
.slide img{
  transition: transorm .6s ease-out;
}
.slide .photo-overlay{
  transform: translateX(-100%);
}
.slide:hober .photo-overlay{
  transform: translateX(0);
}
.slide:hover img{
  transform: translateX(100%);
}
```
## Custom Timing Functions with cubic-bezier()
Making bouncy effects  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/Translation2.png)  
The transition starts slow , then rapidly accelerates towards the end of its duration.
  
https://codepen.io/Guilh/full/ZQxoOX/  
www.cubic-bezier.com  

## 3D Transform
```
//Activate 3d Space with perspective
.content{
  perspective:700px;
  perspective-origin:100% 50%;
}
.photo{
  transition: transform 1s cubic-bezier(.55,-.62,.27,1.2);
  transform-style:preserve-3d;
}
.photo:hover{
  transform:rotateY(-180deg)
}
.side-a,.sideb{
  backface-visibility:hidden;
}
.side-b{
  transform:rotateY(180deg);
  
  transform:rotateZ(90deg);// Same as rotate(90deg)
  transform:rotate(0,1,1,90deg);
}
```
### 3d Cube
```html
<div class="cube-container">
  <div class="photo-cube">

    <img class="front"src="img/photos/1.jpg" alt="">
    <div class="back photo-desc">
      <h3>Earth from Space</h3>
      <p>Aenean lacinia bibendum nulla sed consectetur. Fusce dapibus, tellus ac cursus commodo.</p>
      <a href="#" class="button">download</a>
    </div>
    <img class="left" src="img/photos/2.jpg" alt="">
    <img class="right" src="img/photos/3.jpg" alt="">

  </div>
</div>	
```
```css
/* ================================= 
  Photo 3D Transforms & Transitions
==================================== */

.cube-container {
	box-shadow: 0 18px 40px 5px rgba(0,0,0,.4);
  perspective:800px;
}

.photo-cube{
  transition:transform 2s ease-in-out;
  width:220px;
  height:220px;
  transform-style:preserve-3d;
}

.photo-cube{
  transform:rotateY(-270deg);
}

.front,
.back,
.left,
.right{
  width:100%;
  height:100%;
  display:block;
  position:absolute;
}

.front{
  transform: translateZ(110px); /* +ve Move towards viewer*/
}

.back{
  transform: translateZ(-110px) rotateY(270deg); /* +ve Move towards viewer*/
  transform-origin:center left;
}

.left{
  transform:rotateY(-270deg) translateX(110px);
  transform-origin:top right;
}
.right{
  transform:translateZ(-110px) rotateY(180deg);
}
```
### Translate3d
```css
transform: rotateY(-270deg) translate3d(100px,-50px,50px);
transform:rotateY(-270deg) translateX(110px);
transform:rotateY(-270deg) translate3d(110px,0,0);
```

# Sass
Sass is a stylesheet language that extends the capabilities of CSS. It makes your job easier by adding advanced functionality and time-saving features to your CSS workflow.   
  
Needs Sass ->CSS preprocessor-> Css  
***
- Store values in bariables you can regerence anywhere in your stylesheet
- Compose reusable blocks of styles you can shate with other rule sets
- Split your styles into partials to make your stylesheets modular and easier to maintain
***

## Installing Sass
https://blog.teamtreehouse.com/install-sass-macos-homebrew  
https://blog.teamtreehouse.com/install-sass-windows-chocolatey  

Sass Supports 2 Syntaxes
***
- Sass:"Indented syntax" -original syntax //input.sass
- SCSS:" Sassy CSS"- latest generation of Sass //input.scss (Normally use this)
***

## Watch sss -Compiling Sass to CSS
```
Command Line
sass input.scss output.css
sass --watch input.scss:output.css //Sass watches for changes input.scss to automatically update output.css
```
## Compile a Directory of Sass Files
-scss  
--styles.scss  
-css  
--style.css  
```
Command Line
sass --watch scss:css
```
## Sass Variables
```scss
$white:#fff;

$color-primary:#278da4;
$color-secondary:#b13c69;
$color-accent:#eeea72;
$color-shade:#eee;

$color-text:#343434;
$color-bg:#3acce2;
$color-bg-light:#009fe1;
$font-stack-primary:'Raleway',san-seriff;

body{
color:$color-primary;
}
```
### Nested Selector
```scss
.main-nav{
	margin-top:1em;
	li{
		display:none;
	}
	a{
		display:none;
	}
	&:hover{
	}
}

.btn{
	&-callout{ //target class btn-callout
	}
}
p{
	.intro &{ //targets .intro p (reverses order)
	}
}
```
### Introducing Mixins
Allows you to Break down to modular chunks.  
***  
1. Create a mixin with the @mixin directive
2. Include a mixin inside other rules, using @include
3. @mixin rules need ot appear above the rules including them
***

```scss
@mixin skewed{
	//for repeated codes
	content:'';
	display:block;
	width:100%;
}

footer{
	&::after{
		@include skewed; // needs to be after @mixin decalration
	}
}



// Other examples
$max-width:1000px;

@mixin center{
	width:90%;
	max-width:$max-width;
	margin-left:auto;
	margin-right:auto;
}
```
### Pass content Blocks to Mixins
```
@mixin skewed{
	color:red;
	&::after{ //can include pseduo elements
		content:'';
		display:block;
		width:100%;
		@content; //allows additional css to be decalred later
	}
}

@include skewed{ //additional css decalred here
	background-color:$white;
	bottom:-25px;
}
```

### Extend the Properties of Selectors
```
// Using Sass we can 
.btn{color:red;} //default
.btn-callout{@extend .btn}

//Results
.btn, .btn-callout{color:red}
```

### Extend Placeholder Selectors (best practice)
```
%btn{color:red;}
.btn-callout{@extend %btn;}

//Results, %btn only appears on .btn-callout;
.btn-callout {color:red;} 
```
### Sass Comments
```
/*================
 Major Sections (multi line)
===================*/

//Smaller Sections (Single line)
```

## Add Logic
### Seperate Your Stylesheet into Partials
Allows you to split css into different files. prevent a long css file.  
Instead of having mutiple css style links => alot of http request calls, sass allows your to seperate css files and compile it into one big css file. Maintable and no extra http calls. 
  
Transfer //variables into partials/_variables
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/SCSS1.png)
```
// Importing Partial Variables
@import 'partials/variables',
	'partials/mixins';
```
Good partial split
```
//Utilities
@import 'utilities/variables',
	'utilities/mixins',
	'utilities/functions',
	'utilities/helpers';

//Base Styles
@import 'base/reset',
	'base/base';

//Laout Styles
@import 'layout/containers',
	'layout/header',
	'layout/card',
	'layout/footer';
```
### Nesting Media Queries
Sass lets you nest media queries directly inside the initial rules you're modifying. This keeps media queries local to the original selector, and makes writing and maintaining them easy.
```scss
$break-xs:300px;
.main-content{
	@media(max-width:$break-xs){
		color:red;
	}
}
```
### Color Functions
```
$base:#3accec2;
$base-dark:darken($base,25%);
$base-light:lighten($base,25%);
$base-complement: complement($base); //(Opposite color for high contrast)
```
### Custom Functions
```
@function divide($var-a, $var-b){
	@return($var-a/$var-b);
}
.test{
	line-height:divide(32px/16px);//returns 2
}


@function px-to-pc($target,$context:$max-width){  //$context:$max-width (gives default value : $max-wdith)
	@return ($target/$context)*100%;
}


@function per-line($items){
	$g-pct: px-to-pc($gutte)*2;
	$g-total:$items*g-pct;
	@return (100%/$items)-$g-total;
}
@media (min-width:$break-s){
	flex:1 per-line(2);
}

```
### Creating powerful mixins Functions
```
@mixin center($w){
	width:$w;
}

//Null and keyword
@mixin roundy($dim,$brdr:null){
	width:$dim;
	border:$brdr;
}
@include roundy(50%, 145px solid){
}
@include roundy($dim: 50%){}
```

### Add Conditional Logic to Stylesheet
```
body{
	@if(1>90){
		backgrpund-color:green;
	}
}

//media queries
@mixin mq($break){
	@if $break=='xs'{
		@media(max-width:$break-xs){
			@content;
		}
	}
	
	@else if $break=='sm'{
		@media(max-width:$break-sm){
			@content;
		}
	}
	
	@else if $break=='med'{
		@media(max-width:$break-m){
			@content;
		}
	}
	
	@else if $break=='large'{
		@media(max-width:$break-l){
			@content;
		}
	}
}
```
### Storing Values in Maps
```
$breakpoints:(
	'xs':575px,
	'sm':600px,
	'med;:768px,
	'lg':992px,
);
//Using Directly
@media(max-width:map-get($breakpoints,'xs'));

//Storing into variable first
@mixin mq($break){
	$value:map-get($breakpoints,$break);
	$sm:map-get($breakpoints,'sm');
}
```
### Loops with @for
```
@for $i from 1 through 10{	
	.box-#{$i}{
		background-color:adjust-hue(tomato,$i*20);
	}
}

@for $i from 1 to 10{} //Stop at 9
```

### Loop Through Lists with @each
```
$teachers:('andre,'alena','joel','danielle','nick'); //list

@each $teacher in $teachers{
	.teacher-#{$teacher}{
		background-image:url('img/#{$teacher}.jpg');
	}
}
```
### Loop Through Data in a Map with @each
```
//Theme Colors
$themes:(
	'ent':#79939,
	'arch':#4434,
	'edu':#24545,
	'sim':#23443,
);

@each $theme, $color in $themes{
	.icn-#{$theme}{
		color:$color;
	}
}
```

### Handling Errors with @error and @warn, @debug
```
$value:map-get($breakpoints,"foo");

@if $value==null{
	@error "#{$break} is not a valid breakpoint name."; //Stops it from running
	@warn "#{$break} is not a valid breakpoint name."; //Just informs of code deprecations
}


```
### Debugging Sass with Sourcemaps
```
Source maps is in style.css.map file.

To enable Source maps
- in inspect tools 
- click (top right)... -> Settings
- Preferences-> Enable css sourcemaps

now u can go direct from inspect to styles.css
```

# Javascript
## History
***
- Es6/ Es2015 is the industry standard by the committee tc39.  
- Vanilla, Plain or Pure Javascript refers to use of javascript without any frameworks or libraries. 
- Type Checkers such as "TypeScript" or "Flow"
- Coffee Script or Dart. 
***

### Landscape of Javascript
***
- Dyanmic Programming Language, A language that execute at run-time. 
- Web broswers have an Interpretor or a Java Script Engines. 
- JIT just in time complier. 
***

### Text Editors & Tools
Linters and Formatters. Linters read and spot possible errors. Formatter ensure consistent style.  
Some tools are (ESLint & Prettir).

### Javascript Build Tools
When starting a new JavaScript project, developers usually set up a build system using tools that help manage all of the moving parts of the project, and just about everything needed to build and run their application.
***
- Package managers (npm, Yarn.)
- Module bundlers (webpack, rollup.js, browserify)
- Compilers ( Babel , to understand different flavour of js, typescrit vs coffee script)
- Task runners (Gulp, npm)
***

### Javascript developer's workflow
***
- Simple just code and refresh browser
- More advanced use build system such as React, Vue, Angular.
- Detecting and debugging
***

## Javascript Coding
### Importing js in HTML
```html
<script src="phaser.js"></script>
<script>
alert("HI");
document.write("<h1> Welcome to Javascript Basics</h1>");
</script>
```
### The Javascript console 
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/js1.png)

### Variable
```
var message="Hello"; //Possible var names ( price$, home_alone, pricePerUnit )
```
  
var include different type of values.  
Values : Strings, Number  

\ to escape.  
Eg: 'She\'s Mine'  
  
### Capturing Vistor Input
```
var vistorName= prompt('what is your name?'); //return user input
```
### Object-> Property & Methods
```
vistorName.length // var is an object, length is a property
vistorName.toLowerCase() // toLowerCase() is a Method.
```
### Numbers
int, float , scientific notation  
5,3.14,9e-6 (0.000009)
### Converting Number <-> String
```
parseInt(someString);
parseFloat('1.8 grams of salt');// returns 1.8 , can extract if starts with number
parseInt(' Year 2008') //returns NaN ,Not a Number
```
### Math Object, Random Number 
```
Math.round(2.2);//returns 2
Math.round(4.9)//returns 5
Math.floor(4.9)// round down
Math.random()//return 0 to not including 1
```

### Conditional Statement
```
if (answer==='Ruby'){}
else if{}
else{}

if( answer>1 && 22<age || 3<1){}
```
### Comparison Operators
Normal vs Strict
if(3=='3') //true
if(3==='3')//false
if(''==0)//true

if('alaphabet'<'big')//ture
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/js2.png)

### Boolean Value
```
var correctGuess=false;
```
### Introducing Functions
Javascript is known as funcitonal programming language
```
function alertRandom(upper,eat){
	var randomNumber=Math.floor(Math.random()*upper)+1;
	var test=1+eat;
	alert(randomNumber);
};
alertRandom(1,1);
```
### Testing
```
function getRandomNumber(lower,upper){
	if(isNaN(lower)||isNaN(upper)){
		throw new Error('error message');
	}
	return Math.floor(Math.random()*(upper-lower+1)+lower;
}

console.log(getRandomNumber('nine',24); //does not work
isNaN('nine') // Not a Number? True

```
## Loops, Arrays, Objects
### Loops
```
while(){
	break;
}

do{ //always runs the first time.
}while()

for(var i=1;i<=10;i+=1){
	document.write(i);
}
```
### Arrays
```
var myShopping=[
	'milk',
	'shopping'
];
var assorted=['s',1,true];

assorted[0]; //accessing array
assorted.push(7,8,9); //push to end of array
assorted.unshift(0,1); //add to begining of array

assorted.pop(); //remove last item
assorted.shift(); //remove first item

var daysInWeek=['Monday','Tuesday','Wednesday'];
var daysString=daysInWeek.join(', '); // Returns in comma seperated string

var currentStudents=['jack'];
var newStudents=['jordan'];
var allStudents=currentStudents.concat(newStudents);//concat arrays

var currentStudents.indexOf('jack'); // returns -1 if not in array, Useful for search buttons

//2d arrays
var grades=[
	[80,90,100,95],
	[75,95,85]
];
```

### Objects
Objects have properties & methods
```
var student={
	name:"Dave",
	grades:[80,85,90,95]
};

//accessing properties
student.name;
student['name'];

for(var propName in student){ //looping through and providing property names
	console.log(student[propName]); //does not work .propName
}

//Array of Object
var objects = [
	{question: "How", answer: 12}, 
	{question: "When", answer: 6},
	{question: "Where", answer: 14}
];
```
### JSON (JavaScript Object Notation) & AJAX
Data format used to transmit data
```
{
	name:"Kenny"
	points:{
		total:14639,
		name:hahah
		}
}
```
### Build an Object Challenge
```
<div id='output'></div>

var message='';
var student;

function print(message){
	var outputDiv = document.getElementById('output');
	outputDiv.innerHTML = message;
}

for (var i=0; i<students.length;i+=1){
	student =students[i];
	message+='<h2>Student:'+student.name+'</h2>';
}
print(message);
```

### ES2015 introduced, var-> Const & Let
```
const pi=3.14159;// (constant) only declare once. 
const doesnt affect array or objects from changing but prevents it from being reassign

let description="ahhah"; // for variables that u want to reassign
```
  
let is good in for loops.  Localises the code block scope.  Var is no longer recommended. 
Keep outputing "Button 10 Pressed", Output global scope i
```
const buttons= document.getElementsByTagName("button");
for(var i=0;i<buttons.length;i++){
	const button = buttons[i];
	button.addEventListener("click",function(){
		alert("Button" + i + "Pressed");
	});
}
```
Let, localised output of i. "Button 1 -10 pressed"
```
const buttons= document.getElementsByTagName("button");
for(let i=0;i<buttons.length;i++){
	const button = buttons[i];
	button.addEventListener("click",function(){
		alert("Button" + i + "Pressed");
	});
}
```
## jQuery, javascript library
For Dom Programming easier. 
```
//javascript
const box=document.querySelector('.box');
box.style.display='none';

//jqurey
jQuery('.box').hide();// longer form
$('.box').hide(); //shortest form
$('.box').show();

//javascript
box.addEventListner('click;,function(){
	alert('You clicked me!');
});

//jquery
$('.box').click(function(){
	alert('You clicked me!');
});
```
### Animating Elements with jQuery
---Visibility Methods---  
hide()  
show()  
  
fadeIn()  
fadeOut()  
slideDown()  
slideOut()  
delay()  
```
$('#flashMessage').hide().fadeIn(1000);
$('#flashMessage').delay(3000);
$('#flashMessage').slideUp();
```  
---Changing Content inside Elements---  
```
$('#element').text();//get text
$('#element').text("James"); //set text

$('#element').html(); //getter, get html contents in element
$('#element').html("<h2> Hello</h2>"); //setter, set html content in elements
```  
--- Event listener, val() for form input forms---  
```
$("#preview-button").click(function(){
	const title=$('#blogTitleInput').val();
	const content=$('#blogContentInput').val();
});

.mouseover()
.keypress()
.focus()
```
### Adding jQuery to a Project
https://jquery.com/
```
	<script src="js/jquery-3.2..min.js"></script> //placed here so all contents are in dom first
	<script src="app.js"></script> // insert ur js file after 
</body>
```

The second method is to use CDN (external host), More efficient and users dont have to redownload jQUery if previosuly downloaded.  
http://code.jquery.com/  Select minified version(all uncessary character have been removed),faster for computer
```
copy the scipt tag ...
```

### Unobtrusive Javascript Principles
***
- Seperation of concerns (HTML, CSS, JS -Modularized)
- Cross browser consistency ( jQuery)
- Progressive Enhancement (Works when js is blocked, Firewall,Plugin, Network issues js not loaded, Older Broswers)
***
Ensure when js is disabled site still works, Example. Google Search by voice triggered by js.... so when js is turned off it does not appear. 
### Adding New Elements to the DOM
```
//Create the "Reveal Spoiler" Button
const $button=$('<button> Reveal Spoiler </button>'); // use $ before variable convention, for jquery variables.

$('.spoiler').append($button);//Append to web page, add as last element within the selected parent element
$('.spoiler').prepend($button);// Append as first element
```
### Using on() for Event Handling
adding multiple event listener and not repeating codes.
```
$('#element').on('click keypress',function(){
	//do stuff when the element is clicked OR when a key is pressed
	
});
```
### Using Events with Dynamically Added Elements
When project gets too large, alot people editing code... you might add event handling before appending a element like button. To prevent the error use Event Delegation.   
  
Event Delegation Listen to events on parent element instead of element...
```
//------HTMl--------------
<p class="spoiler">
	<span>Darth Vader is Luke Skywalker's Father! Noooooooooooo!</span>
</p>

//------Javascript---------
$('.spoiler').on('click','button',function(){ 
	//Adds the event handler onto the parent element. So you can dynamically add elements no matter the ordering
}

//Append Button. Commonly placed first..
const $button=$('<button> Reveal Spoiler </button>');
$('.spoiler').append($button);
```
### The Event Object
Event Object contains a bunch of event that just occured.
```
//Event object declared
$('#element').on('click',function(event){
	//do something with event on click
	console.log(event);
	
	$(event.target).hide(); // hide the specific button clicked
	
})
```
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/js3.png)
### Traversal 
```js
$('li').eq(0); //return 1st list item
$('li').eq(1).prev().css({color:'green'});
$('li').eq(0).next();
```
### jQuery-Specific Selectors 
***
- CSS Selector
	- h1, p ,a
	- #footer,.profile-image
	- :first,:last
- jQuery Specific Selectors
	- :radio, :checkbox, :password
	- :odd, :even
	- :visible, :hidden
***
```
const $odd=$('a:odd'); // select odd elements ,$odd for jQuery Variables
$odd.hide();

const $secureLinks=$('a[href^="https://"]');
const $pdfs=$('a[href$=".pdf"]');
```
### jQuery dynamically changing attributes with attr()
```
$('#my-iamge').attr("alt");//Getter
$('#my-image').attr("alt","Sunset in Barcelona")//Setter
```
### jQuery changing element styles and classes
```
$element.css("backgroundColor")//Getter
$element.css("backgroundColor","green")//Setter

$('.my-element').addClass("className")
$('.my-element').removeClass("className")
$('.my-element').toggleClass("className")

```
### Stopping Browser's Default Behaviour, event.preventDefault()
```
$pdfs.on('click',function(event){
	//check if checkbox has been checked
	//if zero checkboxes are checked
	/*-----$(':checked')// returns array of checked elements on page-------*/
	if($(':checked').length===0){
		//prevent download of document	
		event.preventDefault();
		//alert the user
		aalert("PLease check the box to allow PDF downloads.');
	}
	//else allow the download
});
```
### jQuery each method, loop through a jQuery collection
```
$('a').each(function(index,element){ //loop through a jQuery collection
	console.log(index,$(element).atrr('href'));
});

$('a').each(function(){ //loop through a jQuery collection, using this
	console.log($(this).atrr('href')); //this refers the current item in the collection
});
```
## jQuery Plugin
jQuery Librarys
jCacluators, jQuery Adaptive Model, jQuery ListNav, lightbox, video
  
-Finding Plugins   
https://www.sitepoint.com/jquery-popular-plugins-list/    
https://www.unheap.com/  
***   
- A good plugin
	- Does what u need
	- Good documentation
		- How call, Html Setup, Options Avalible
	- Is it still actively supported. (Github Commits)
	- Responsive Friendly
	- Mobile Friendly
***
### Plugin Files
Consist of:
***
- A CSS File
- Javascript File (Compulsory)
- Images
***

### Downloading & File restructing for easier use
Animsition(jQuery plugin), allows transition effect when toggling pages, Fade left/right.
***
1. Download Github zip(src is what author used to code the plugin, dist is what u use)
2. rename dist -> Animsition(Name of plugin), send css and js into Animsition folder
3. Ensure u keep plugin in one file. Easier to maintain 
***

### Adding jQuery Plugin to a Webpage
***
1. Attach CSS files 
```
<link rel="stylesheet" href="js/animation/animsition.min.css"> //placed above, so u can overwrite with ur own main.css
<link rel="stylesheet" href="css/main.css"> 
```
2. Attach jQuery 
3. Attach the plugin Javascript file 
```
//it's best to place all your script references at the end of the page, just before </body>
	<script src="js/jquery-1.11.2.min.js"></script>
	<script src="js/animsition/jquery.animsition.min.js"></script>
</body>
```
4. Structure ur HTML
5. Add your own Javascript 
6. Select an element on the apge using jQuery
7. call the plugin function
***
## Sticky js plugin
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/js4.png)
### Plugin Events
Event<->Response  	// clicked<->Img popups
```
$(.header).sticky();

$(".header").on('sticky-start',function(){ // 'sticky-start is event when nav menu starts to stick
	$(.description).html('We build <strong> great<strong> apps.
});


$(".header").on('sticky-end',function(){ // 'sticky-end is event when nav menu starts to stick
	$(.description).html('We build great apps.
});
```
## Carousel- similar to a slideshow
slick - https://kenwheeler.github.io/slick/
```
$('.slides').slick({
	fade:true,
	autoplay:true,
	autoplaySpeed: 2000,
	arrows:false,
	dots:true
});

change slick-theme.css to personalise.
```
### The Carousel Challenge
***
1. Adding Slick CSS files
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/slideshow2.png)
2. Attach jQuery and the Slick Plugin files
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/slideshow3.png)
3. Add a div to hold the slides & Add the 'slides'  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/slideshow4.png)
4. Add the programming to call the plugin  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/slideshow5.png)
5. Lastly , customize css on main.css so future theme updates dont conflict
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/slideshow6.png)
***

# Arrow Syntax
```
//Function declaration
function sayName(){
	return null;
}

//Function Expression 
const sayName=function(){
	return null;
}

//Function Arrow Expression
const sayName=(x,y)=>{
	return x+y;
}

//More consise arrow 
const sayName=x=>{ x*x;} // Only one arguement, only one line 
```
# JavaScript and the DOM

## Interactive pages with JavaScript
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/jsdom1.png)
***
1. Selecting elements on the page
2. Manipulating elements
3. Listening for user actions
***

## Thinking Globally, global scope- window object
There is a gloabl object known as "window"
```js
----------JS console--------------
window // Print on console to see

//window variables
alert('I made the browser message me') //similar to window.alert("I made...")
location.href // similar to window.location.href
window.dom

//DOM is document object Model,is a representation of the document that JavaScript uses to navigate and make changes to a webpage.

document.getElementById('myHeading').style.color='purple'
document.getElementById('myHeading').style.backgroundColor='yellow'
```
## DOM , tree like sturcture
The DOM is a representation of a webpage that JavaScript can use
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/jsdom2.png)

## Listening / Responding to Event, Simple Example
### Selecting Elements, using document.getElement
```js
const myHeading=document.getElementById('myHeading');
const myButton = document.getElementsByTagName('button'); //return a collection/array of elements
const myTextInput= document.getElementsByClassName('myTextInput');

myButton[0].addEventListner('click',()=>{
	myHeading.style.color=myTextInput[0].value;
});
```
### Using CSS Queries to Select Page Elements
```
document.querySelectorAll('li') //Return HTML Collection of all 'li'
document.querySelector('li') //Return first HTML element 'li'
document.querySelector('#id')
document.querySelectorAll('.class')

document.querySelector('[title=label]') // return element with title='label'
document.querySelector('li:nth-child(even)') 
```
### Broswer Support and Documentation
Mdn Document Page :https://developer.mozilla.org/en-US/docs/Web/API/Document  
https://caniuse.com/  

### Getting and Setting Text with textContent and innerHTML
```
let myHeading=document.querySelector('h1');
myHeading.textContent // returns "The header value"
myHeading.textContent="This is a new heading";

let ul=document.querSelector('ul');
ul.innerHTML="<li> first</li>" //can change html
```

### Changing Element Attributes
```
input.type
input.className
input.type="checkbox"
```

### Styling Elements
```
Element.style.prop

p-description=document.querySelector('p.description');
p-description.style.color // returns "darkblue";
p-description.style.backgrounColor= 'lightblue';

//Toggle display
toggleList.addEventListner('click',()=>{
	if(listDiv.style.display=='none'){
		listDiv.style.display='block';
	}else{
		listDiv.style.display='none';
	}
});
```
### Creating New DOM Elements
Added Element will not appear on the DOM 
```
const addItemInput=document.querySelector('input.addItemInput');

addItemButton.addEventListner('click',()=>{
	let li=document.createElement('li');
	li.textContent=addItemInput.value;
}
```
### Appending Nodes, appendChild()
In the last video, you saw how to create elements, but they won't appear on the page until you add them to the DOM. In this video, you'll select an existing node, then learn to append, or add, a new node as a child.
```
<ul>
	<li></li>
</ul>

let ul=document.getElementsByTagName('ul')[0]; //1) Select parent element
let li=document.createElement('li');
li.textContent= addItemInput.value;
ul.appendChild(li);
```
### Removing Nodes, removeChild()
```
let ul=document.getElementsByTagName('ul')[0]; //1) Select parent element
let li=document.querySelector('li:last-child');
ul.removeChild(li);
```
## Events
### What is an Event
Any time you interact with a webpage, you generate all kinds of events. An event is something you do on the web page, like moving your mouse around, scrolling, or clicking a link. Browsers "listen" for events and, with JavaScript, we can do something in response to an event.
***
- Mouse Events
	- click
	- dblclick
	- mousedown
	- mousemove
	- mouseover
	- mouseout
- Keyboard
	- keydown
	- keyup
	- keypress
- load (Load event trigger once all html,css, js has been loaded to the page)
***
### Functions as Parameters
```
function say(something){
	console.log(something);
}

// We declare a function as a parameter/input
function exec(func, arg){
	func(arg);
}

exec(say,'Hi There');

// ------Can also transform into----------
function exec(func, arg){
	func(arg);
}

exec(function say(something){ //this become an statement->experesssion
	console.log(something);
},'Hi There');

```
### Delaying Execution with setTimeout()
```
window.setTimeout((something)=>{ //(something) is a callback function when other events takeplace.
	console.log(something);
}, 3000, 'Greetings, everyone!');
```
### Listening for Events with addEventListener()
https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener  
  
Syntax
```
target.addEventListener(type, listener[, options]);
target.addEventListener(type, listener[, useCapture]);
target.addEventListener(type, listener[, useCapture, wantsUntrusted  ]); // Gecko/Mozilla only
```
List Hover change to UpperCase  
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/jsdomevent1.png)
```
for(let i=0;i<listItems.length;i+=1){
	listItems.addEventListener('mouseover',()=>{
		lsitItems.textContent=listItems.textContent.toUpperCase();
	});
	listItems.addEventListener('mouseout',()=>{
		lsitItems.textContent=listItems.textContent.toLowerCase();
	});
}
```
### Event Bubbling and Delegation
An event received by an element doesn't stop with that one element. That event moves to other elements like the parent, and other ancestors of the element. This is called "event bubbling".

If any child is clicked, callback function is triggered
![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/jsdomevent2.png)

### The Event Object
```
//When event handler is called, it receives an event object to know which children called it
document.addEventListener('click',(event)=>{
	// event is an object with info & methods
	if(event.target.tagName=="li"){
		console.log(event.target); //returns child being clicked.
	}
});
```
## Element Traversal
### Traverse Up the DOM, parentNode
```
listDiv.addEventListener('click',(event)=>{
	if(event.target.tagName=='BUTTON'){
		let li=event.target.parentNode;
		let ul=li.parentNode;
		ul.removeChild(li);
	}
});
```
### previousElementSibling and insertBefore
previousSibling vs previousElementSibling. previousElementSibling always return DOM elements.   
Avoid previousSibling.
```
listDiv.addEventListener('click',(event)=>{
	if(event.target.tagName=='BUTTON'){
		if(event.target.className=='remove'){
			let li=event.target.parentNode;
			let ul=li.parentNode;
			ul.removeChild(li);
		}
		if(event.target.className=='up'){
			let li=event.target.parentNode;
			let prevLi=li.previousElementSibling;
			let ul=li.parentNode;
			if(prevLi){ //prevLi == null if its the first node..
				ul.insertBefore(li,prevLi);
			}
		}
	}
});

```
### nextElementSibling
```
let nextLi=li.nextElementSibling;// returns next sibling
ul.insertBefore(nextLi,li);
```
### Getting All Children of a Node with children
```
ul.children; // return list of children
```
### firstElementChild & lastElementChild
```
firstListItem=ul.firstElementChild;
lastListItem=ul.lastElementChild;
```
## Debugging Javascript 
*** 
1. console.log()
2. Breaking on Events and Basic Stepping
	1. Go to Sources Tab in inspect element
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs1.png)
	2. Breakpoints on Event , so we go to the callback function of an event( eg. click event)
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs2.png)
	3. Step over each line , with the step button. 
3. Basic and Conditional Line Breakpoints
	1. Adding a line breakpoint, just click on the line, it will pause here
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs3.png)
	2. Can also add conditional line breakpoint so callback function only pause when a certain class is triggering it. 
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs4.png)

4. Debugging Functions
	1. Step into function 
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs5.png)
	2. Call Stack, Scope keep tracks of nested function calls
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs6.png)

5. Debugging Exception Errors
	1. Pause on exceptions, to see the state just before error is thrown
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs7.png)
	2. Moving down the stack calls.
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs8.png)
	  We find local scope: li is undefined but block scope: is defined. li exist in local scope and cannot use the outer scope. 
6. Breaking on DOM Changes and Watch Expressions
	1. Attribute Modification , Node Removal, Subtree Modification
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs9.png)
	2. Watch Expression, keep track of selected variables
	![images](https://github.com/KennySoh/Technical-Interview/blob/master/oop/debuggingjs10.png)

## Conditional Terminology
### Switch Statement
```
switch(day){
	case 0:
		console.log('Sunday');
		break;
	case 1:
		console.log('Monday');
		break;
	default:
		console.log('Wrong day');
		break;
	
}
```
### Ternary Operator
```
<boolean> ? <expression if true> : <expression if false>

//Normal if else
if(isTrue){
	console.log('yes');
}else{
	console.log('no');
}

//Ternary Operator
isTrue? console.log('yes'):console.log('no');

var yesOrNo = isTrue ? 'yes':'no';
```

### Short Circuit Evaluation
Stopping code execution as soon as possible  
Truthy https://developer.mozilla.org/en-US/docs/Glossary/Truthy  
```
console.log(3===3 && 'cow' && 'chicken') // logs 'chicken', take note: 3===3, 'cow' returns truthfy
console.log(3===3 && false && 'chicken') // logs false
3===3 && false && console.log('chicken')// equivalent to if (3==3&&false){ console.log('chicken')}
console.log(3===4||false || 0);
```
Commonly used generic If Else & Switch, But useful when
```
function isAdult(age){
	return age && age>=18;
}
```

## Dom Scripting By Example
```
ul.addEventListener('click',(e)=>{
	if(e.target.tagName==='BUTTON'){
		const button=e.target;
		const li=button.parentNode;
		const ul=li.parentNode;
		if( button.textContent=='remove'){
			ul.removeChild(li);
		}else if(button.textContent==='edit'){
			const span=li.firstElementChild;
			const input=document.createELement('input');
			input.type='text';
			input.value=span.textContent;
			li.insertBefore(input,span);
			li.removeChild(span);
			button.textContent='save';
		}else if(button.textContent==='save'){
			const input=li.firstElementChild;
			const span=document.createELement('span');
			span.textContent=input.value;
			li.insertBefore(span,input);
			li.removeChild(input);
			button.textContent='edit';
		}
	}
});
```
### DOMContentLoaded Event
```
//Wrapping js with DOMContentLoaded so it runs only after Dom is loaded
document.addEventListener('DOMContentLoaded',()=>{
	//js goes here
});
```
### Refactor 2: Readable Branching Logic
```
const nameActions={
	remove:()=>{
		ul.removeChild(li);
	},
	edit:()=>{
	},
	save:()=>{
	}
};

const action=button.textContent;
nameActions[actions]();
```
## Template Literals
### Basic and Multiple Line Strings
```
const templateLiteral= `<p>Template literal</p>`;

const templateLiteralMultiLine=`
	<ul> 
		<li>Potato</li>
		<li>Onion</li>
	</ul>
	`;
	
document.querySelector('.vegetables').innerHTML=vegetableList;

```
### Interpolation
```
// using this syntax ${ variable} 
function like(thing){
	return 'I like '+ thing;
}

function love(thing){
	return `I love ${thing}`;
}
```
# Vector Graphics
### SVG 
An SVG is a series of interconnected points called vectors. These points and lines form shapes that are automatically projected into the pixel grid of a computer screen. The end result is a graphic that has infinite resolution, regardless of how the image is resized. 
### Creating an SVG
Using adobe illustrator

SVG optimiser https://github.com/svg/svgo
```
//Ways to include svg
-----------1st way----------------
<img src="img/star.svg" alt="Star Logo">

-----------2nd way----------------
<div class="graphic-with-text>
	<p> This text will go on top of the graphic.</p>
</div>
.graphic-with-text{
	color:#FFF;
	background:transparent url('../img/star.svg') center center no-repeat;
	height:200px;
}
```
