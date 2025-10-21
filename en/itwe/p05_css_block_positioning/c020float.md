# Floating objects

  - Object that are flowed by the surrounding text
  - Creating a floating object: 
    - `float: left` or
    - `float: right`
  - Floating elements become automaticaly **block** elements
  - The floating object is 
    - Removed from the normal text flow (doesn't influence the text on the original place)
    - Shifted to the border of the parent element
  - Different way of width computation 
    - It is better to set an explicit width
    - If not set, it is automaticaly computed (shring-to-fit algorithm)

---

# Floating demonstration

  - [Normal flow (default)](data/float0.html)

```html
@HTML@
...@@
<div @="" class="floating" id="menu">@@
    <h1>Menu</h1>@@
    <ul>@@
        <li>Red</li>@@
        <li>Green</li>@@
        <li>Magenta</li>@@
        <li>Yellow</li>@@
        <li>Dark blue</li>@@
    </ul>@@
</div>@@
...
@/HTML@
```

---

# Creating a floating object

```html
@HTML@
<style type="text/css">@@
    #menu { background-color: #eef;@@
            border: 1px solid #aaf;@@
            width: 12em; }@@
    .floating { float: left; }@@
</style>
@/HTML@
``` [Sample](data/float1.html)

---

# Margins

```html
@HTML@
<style type="text/css">@@
    #menu { background-color: #eef;@@
            border: 1px solid #aaf;@@
            width: 12em;@@
            @/padding: 0;/@ @@
            @/margin-right: 1em;/@ }@@
    .floating { float: left; }@@
</style>
@/HTML@
```

---

# Heading

```html
@HTML@
<style type="text/css">@@
    #menu { ... }@@
    @/#menu h1 { font-weight: bold;@@
               font-size: 100%;@@
               color: #fff;@@
               background-color: #55f;@@
               margin: 0;@@
               padding: 0.5em; } /@ @@
    .floating { float: left; }@@
</style>
@/HTML@
``` [Sample](data/float2.html)

---

# Paragraph block size

```html
@HTML@
<style type="text/css">@@
    #menu { ... }@@
    #menu h1 { font-weight: bold;@@
               font-size: 100%;@@
               color: #fff;@@
               background-color: #55f;@@
               margin: 0;@@
               padding: 0.5em; }@@
    .plovouci { float: left; }@@
    @/p { border: 5px solid red; }/@ @@
</style>
@/HTML@
``` [Sample](data/float3.html)

---

# Clear

  - The floating objects are placed by the browser 
    - Side by side to the appropriate margin
    - When there is no space then below each other
    - => The floating object can horizontaly overflow the flowing text
  - When some text shouldn't flow along the floating objects: 
    - `clear: left | right | both`
  - First, previous floating object are placed, then the text is placed below
  - [Example](data/clear1.html)

---

# Containing block height (again)

  - When a block has `height:auto`, its height depends on its contents
  - For `overflow: visible`
    - Only in-flow content is considered
    - If the block contains floating blocks only, it has a **zero height** in the result
  - Otherwise (e.g. `overflow: hidden`) 
    - Floating content is considered too
  - [Example](data/overflow1.html)

---

# Block Height: Example

```html
@HTML@
<div class="contents">@@
	<div class="col">Column 1</div>@@
	<div class="col">Column 2</div>@@
</div>@@
<p>Next contents</p>
@/HTML@
``` ```html
@CSS@
.contents {@@
	border: 5px solid blue;@@
}@@
.col {@@
	float: left;@@
	background: gray;@@
}@@
@/CSS@
```

---

# Block Height: Example (II)

```html
@CSS@
.contents {@@
	overflow: visible;@@
}
@/CSS@
``` 

Column 1

Column 2

Next contents

---

# Výška bloku: příklad (III)

```html
@CSS@
.contents {@@
	overflow: hidden;@@
}
@/CSS@
``` 

Column 1

Column 2

Next contents
