# Html

Think of everything as boxes  
  
```html
<!doctype html>
<html>
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
border-bottom-left-radius:50px;
border-bottom-right-radius:50px;

border-radius: 50px 10px 50px 10px; 
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


# HTML & CSS Validators
background-color:#ff4add;
html validator: https://validator.w3.org/nu/#textarea  
css validator: https://jigsaw.w3.org/css-validator/validator  
