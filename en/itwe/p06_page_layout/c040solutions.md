# Typical CSS Solutions

---

# Links as Buttons

```html

<a href="..."><em>E-mail</em> burgetr@fit.vutbr.cz</a>

``` 

_E-mail_ burgetr@fit.vutbr.cz

---

# Links as Buttons

```html

<a class="button" href="...">
    <em>E-mail</em><span> burgetr@fit.vutbr.cz</span></a>

```

```css
.button:link {
   margin: 0 0.2em; padding: 0.1em 0;
   border: 2px solid black;
   text-decoration: none;
   background: #ccc;
   color: black;
}

``` 

_E-mail_ burgetr@fit.vutbr.cz

---

# Links as Buttons

```css

.button em {
   font-style: normal;
   margin:0; padding: 0.1em 0.5em;
   background: white;
   color: black;
}

``` 

_E-mail_ burgetr@fit.vutbr.cz

---

# Links as Buttons

```css

.button span {
   margin:0; padding: 0.1em 0.5em 0.1em 0.3em;
}

``` 

_E-mail_ burgetr@fit.vutbr.cz

---

# Links as Buttons

```css

.button:hover {
    background: #666;
    color: white;
}

.button:hover em {
    background: black;
    color: white;
}

``` 

_E-mail_ burgetr@fit.vutbr.cz

---

# Links with an icon

```html

<a href="...">Some link</a>

``` 

Some link

---

# Links with an icon

```css

a {
    background: #eeeeff url('newwin32.png') top right no-repeat;
    padding-right: 20px;
    padding-top: 15px;
}

``` 

Some link

---

# Using lists for menus ([Listamatic](http://css.maxdesign.com.au/listamatic/index.htm)) 

```html

<ul id="menu">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Using lists for menus

```css

ul#menu {
    padding: 0 1px 1px;
    margin-left: 0;
    background: gray;
    width: 13em;
} 

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Using lists for menus

```css

ul#menu li {
    list-style: none;
    margin: 0;
    border-top: 1px solid gray;
    text-align: left;
}

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Using lists for menus

```css

ul#menu li a {
    display: block;
    padding: 0.25em 0.5em 0.25em 0.75em;
    border-left: 1em solid #AAB;
    background: #CCD;
    text-decoration: none;
}

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Using lists for menus

```css

ul#menu li a:link { color: #448; }
ul#menu li a:visited { color: #667; }
ul#menu li a:hover {
    border-color: #FE3;
    color: #FFF;
    background: #332;
}

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Floating menus

```css

ul#menu {
    padding: 0 1px 1px;
    margin-left: 0;
    background: gray;
    width: 13em;
    @/float: left;/@ 
    @/margin-right: 1em;/@ 
} 

``` 

[Example](data/floatmenu1.html)

---

# Floating menus

```css

    body {
        border: 2px solid gray;
        margin-left: 5em;
    }

```

 [Example](data/floatmenu2.html)

---

# Floating menus

```css

ul#menu {
    padding: 0 1px 1px;
    margin-left: 0;
    background: gray;
    width: 9em;
    float: left;
    margin-right: 1em;
    @/position: relative;/@ 
    @/left: -4em;/@ 
}

``` 

[Example](data/floatmenu3.html)

---

# Floating menus

```css

ul#menu {
    padding: 0 1px 1px;
    margin-left: 0;
    background: gray;
    width: 9em;
    float: left;
    @/margin-right: -2em;/@ 
    position: relative;
    left: -4em;
}

``` 

[Example](data/floatmenu4.html)

---

# Horizontal list

```html

<ul>
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Horizontal list

```css

ul.vertlist1 li { display: inline; }

```

```html
<ul class="vertlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Horizontal list

```html

ul.vertlist1 li { display: inline-block; }

<ul class="vertlist">
  <li><a href="#">Item 1</a></li>
  <li><a href="#">Item 2</a></li>
  <li><a href="#">Item 3</a></li>
</ul>

``` 

  - Item 1
  - Item 2
  - Item 3

---

# Vertical line centering

  - Let's have a block whose **height is known**
  - Inside, there is a **single line** text, which we want to center

```html

<div class="box">
    Some text
</div>

```

---

# Vertical line centering

```css

#box {
    @/height: 5em;/@ 
    background-color: gray;
}

``` 

Some text

---

# Vertical line centering

```css

#box {
    @/height: 5em;/@ 
    @/line-height: 5em;/@ 
    background-color: gray;
}

``` 

Some text

---

# Image sprites

  - More images in one larger image
  - The individual images are extracted using the background positioning
  - More efficient and smooth user experience
  - [Image sprite 1](data/imageSprite.png)
  - [Image sprite 2](data/imageSprite2.png)

---

# Image sprites (II)

  - [Example 1](data/sprite1.html) ```html

a.smile { background: url("imageSprite.png") -315px -28px; }
a.smile:hover { background: url("imageSprite.png") -341px -28px; }

a.del { background: url("imageSprite.png") -269px -52px; }
a.del:hover { background: url("imageSprite.png") -269px -68px; }

``` 
  - [Example 2](data/sprite2.html)

---

# Fixed Page Header

  - [Example](data/fixHeader.html) ```html

#header {
  position: fixed; 
  top: 0; left: 0; 
  width: 100%; 
  z-index: 1; 
}

```

---

# Tabs

  - Combination of a content block and a list (several solutions available)
  - The list is styled to tabs
  - Different styles for the active tab and the :hover
  - [Example](data/tabMenu.html)
