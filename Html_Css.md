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

## 

# HTML & CSS Validators
html validator: https://validator.w3.org/nu/#textarea  
css validator: https://jigsaw.w3.org/css-validator/validator  
