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

## Image Tag
```html
<!-- Html Tags <img>,  Attributes (src, alt, class)-->
<img src=images/portland.jpg alt="Drawing of Kenny" class="profile-image">  
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

## Adding section tags, article, nav
section tags to better structure different major section  
article tags to seperate items in major sections  
nav tags markups for major links groups.   
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
    <section>
      <h2>Welcome</h2> 
      <p>Fusce semper id ipsum sed scelerisque. Etiam nec elementum massa. Pellentesque tristique ex ac ipsum hendrerit, eget feugiat ante faucibus.</p>
      <ul>
        <li><a href="#">Recent project #1</a></li>
        <li><a href="#">Recent project #2</a></li>
        <li><a href="#">Recent project #3</a></li>     
      </ul>
    </section>
    <footer>
      <p>&copy; 2017 My Portfolio</p>
      <p>Follow me on <a href="#">Twitter</a>, <a href="#">Instagram</a> and <a href="#">Dribbble</a></p>
    </footer>
  </body>
</html>
`
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

