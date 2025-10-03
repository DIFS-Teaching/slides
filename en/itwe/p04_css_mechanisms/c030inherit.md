
# Property inheritance

  * Some property values are inherited by the child elements

```html
@HTML@
<p class="intro concl">Following text is@@
    <span class="imp">important</span></p>@@
@/HTML@
``` ```html
@CSS@
p { color: red; border: 1px solid blue; }
@/CSS@
``` 
  * The text color applies to the child element too
  * Only the parent element `<p>` has the border
  * The [CSS specification](http://www.w3.org/TR/CSS21/propidx.html) defines which properties are inherited

---

# Typical Usage of Inheritance

```html
@CSS@
body {@@
    color: white;@@
    background-color: black;@@
}@@
@@
h1 {@@
    color: red;@@
}
@/CSS@
``` 

  * All the text will be white 
    * All the elements inherit their color from the `body` element
  * Only the headings (and their descendant elements) will be red 
    * We define red color for `h1`

---

# The `inherit` value

  * Each property can have a special `inherit` value
  * The property value is then always inherited from the parent

```html
@HTML@
<div id="menu">@@
	<h1>Menu</h1>@@
	<p>First paragraph</p>@@
	<p>Second paragraph</p>@@
</div>
@/HTML@
```

---

# Example

# Menu

First paragraph

Second paragraph

```html
@CSS@
#menu { border: 3px #99ff99 solid; }
@/CSS@
```

---

# Example

# Menu

First paragraph

Second paragraph

```html
@CSS@
#menu { border: 3px #99ff99 solid; }@@
#menu p { border: inherit; }
@/CSS@
```

---

# Example

# Menu

First paragraph

Second paragraph

```html
@CSS@
#menu { border: 10px #99ff99 solid; }@@
#menu p { border-style: dashed; border-color: inherit; }
@/CSS@
```

