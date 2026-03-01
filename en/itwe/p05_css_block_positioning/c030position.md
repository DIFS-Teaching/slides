# Positioning

  - Manual specification of the object's position on the page
  - Absolute
    - Placing an object to a particular place independently on the remaining text
  - Relative
    - Moving the object relatively to its normal position
  - The `position` property
    - `position: static` \-- normal flow
    - `position: absolute` \-- absolute positioning
    - `position: relative` \-- relative positioning
    - `position: fixed` \-- fixed positioning

---

# Relative positioning

  - The position relative to normal placement
    - `position: relative`
  - The block remains in normal flow; it's just moved
  - The distance from the top left corner
    - `top: length` \- moving down
    - `left: length` \- moving right
  - The distance from the bottom right corner:
    - `bottom: length` \- moving up
    - `right: length` \- moving left
  - May be combined
  - Negative value - reverse direction

---

# Relative positioning - example

<pre class="code-render" default-style="
.word { font-weight: bold; }
" resizable="true" style="width: 40%; height: 120px; float: right; z-index: 1">
This is <span class="word">bold</span> text.
</pre>

```html
<style>
    .word {
        font-weight: bold;
    }
</style>
...
This is <span class="word">bold</span> text.
```

=--

# Relative positioning - example

<pre class="code-render" default-style="
.word {
    font-weight: bold;
    position: relative;
    top: -0.5em;
    left: 5px;
}
" resizable="true" style="width: 40%; height: 120px; float: right; z-index: 1">
This is <span class="word">bold</span> text.
</pre>

```html
<style>
    .word {
        font-weight: bold;
        position: relative;
        top: -0.5em;
        left: 5px;
    }
</style>
...
This is <span class="word">bold</span> text.
```

---

# Absolute positioning

  - `position: absolute`
  - The object is **removed** from the normal flow
    - Doesn't influence the text in the normal place
  - It is placed to a particular place on the page
    - It can overlap the objects being already on that place
    - It is necessary to „make space"
  - The distance from the top left corner of the **containing block**
    - `top: length`
    - `left: length`
  - The distance from the bottom left corner
    - `bottom: length`
    - `right: length`

---

# Containing Block

  - Initial containing block is the _Viewport_
  - Elements with position `relative` or `static`
    - The nearest ancestor block is the containing block
  - Elements with position `absolute`
    - The nearest ancestor block with position `relative`, `absolute` or `fixed` is the containing block
  - Elements with position `fixed`
    - Viewport is always the containing block

---

# Coordinate System

  - Normally, the coordinate system is formed by the **Viewport**
  - Objects that have `position: absolute` or `relative` or `fixed`, create a **local coordinate system** for absolute positioning
    - Nested object with `position: absolute` are positioned from within the parent

=--

# Coordinate System (II)

  - Child blocks are positioned within **Viewport** (parent is `static`):

<pre class="code-render" default-style="
#parent { background: #eef; border: 2px solid #aaf; height: 130px; }
#child1 { position: absolute; top: 10px; left: 10px; background: #fbb; border: 1px solid red; padding: 4px; }
#child2 { position: absolute; top: 45px; left: 80px; background: #bfb; border: 1px solid green; padding: 4px; }
" resizable="true" style="height: 180px; width: 90%; margin: auto">
<div id="parent">
    Parent (position: static)
    <div id="child1">child1 (absolute)</div>
    <div id="child2">child2 (absolute)</div>
</div>
</pre>

```html
<div id="parent">
    <div id="child1" style="position: absolute">...</div>
    <div id="child2" style="position: absolute">...</div>
</div>
```

=--

# Coordinate System (III)

  - Child blocks are positioned within **parent block** (parent is `relative`):

<pre class="code-render" default-style="
#parent { background: #eef; border: 2px solid #aaf; height: 130px; position: relative; margin: 10px; }
#child1 { position: absolute; top: 10px; left: 10px; background: #fbb; border: 1px solid red; padding: 4px; }
#child2 { position: absolute; top: 45px; left: 80px; background: #bfb; border: 1px solid green; padding: 4px; }
" resizable="true" style="height: 180px; width: 90%; margin: auto">
<div id="parent">
    Parent (position: relative)
    <div id="child1">child1 (absolute)</div>
    <div id="child2">child2 (absolute)</div>
</div>
</pre>

```html
<div id="parent" style="position: relative">
    <div id="child1" style="position: absolute">...</div>
    <div id="child2" style="position: absolute">...</div>
</div>
```

---

# Absolute positioning - example

<pre class="code-render" default-style="
.container { position: relative; height: 180px; background: #f5f5f5; border: 1px solid #ccc; }
.word {
    font-weight: bold;
    position: absolute;
    top: 60px;
    left: 120px;
    background: yellow;
    padding: 2px 6px;
}
" resizable="true" style="width: 45%; height: 220px; float: right; z-index: 1">
<div class="container">
    <p>Normal text in container.</p>
    <span class="word">bold</span>
</div>
</pre>

```html
<style>
    .word {
        font-weight: bold;
        position: absolute;
        top: 150px;
        left: 500px;
    }
</style>
...
This is <span class="word">bold</span> text.
```

---

# Fixed positioning

<pre class="code-render" default-style="
.word {
    font-weight: bold;
    position: fixed;
    top: 20px;
    right: 20px;
    background: yellow;
    padding: 4px 8px;
    border: 1px solid #999;
}
" resizable="true" style="width: 45%; height: 200px; float: right; z-index: 1">
<p>Normal text content here. The bold word is fixed to the top-right corner of the viewport.</p>
<span class="word">bold (fixed)</span>
</pre>

```html
<style>
    .word {
        font-weight: bold;
        position: fixed;
        top: 150px;
        left: 500px;
    }
</style>
...
This is <span class="word">bold</span> text.
```

---

# Positioned Element Width and Height

  - The equation for width:
**left** \+ margin-left + border-left-width +
\+ padding-left + width + padding-right +
\+ border-right-width + margin-right + **right** = _containing_block_width_
  - The `auto` values for `left` and `top` are derived from _static position_
  - Computation of multiple `auto` values is defined in the [specification](http://www.w3.org/TR/CSS21/visudet.html#abs-non-replaced-width)
  - The **height** is computed analogously

---

# Object overlaping

  - Two elements may overlap (relative or absolute positioning)
  - Normally, the later specified object overlaps the earlier object
  - This can be changed using the `z-index` property
    - `z-index: 10`
    - The number gives the Z coordinate of the object (the higher number the „higher" placed is the object)
    - If not specified, **0** is used

---

# Overlaping: example

<pre class="code-render" default-style="
.box { padding: 1em; border: 2px solid; }
" resizable="true" style="width: 45%; height: 180px; float: right; z-index: 1">
<div style="height: 120px; position: relative; background: #f5f5f5;">
    <div class="box" style="position: absolute; top: 15px; left: 20px; background: #bbf; border-color: blue;">First box</div>
    <div class="box" style="position: absolute; top: 50px; left: 60px; background: #fbb; border-color: red;">Second box</div>
</div>
</pre>

```html
<div style="height: 4em; position: relative">
    <div class="box" style="position: absolute;
         top: 30px; left: 180px">
         First box</div>
    <div class="box" style="position: absolute;
         top: 60px; left: 200px">
         Second box</div>
</div>
```

=--

# Overlaping: example

<pre class="code-render" default-style="
.box { padding: 1em; border: 2px solid; }
" resizable="true" style="width: 45%; height: 180px; float: right; z-index: 1">
<div style="height: 120px; position: relative; background: #f5f5f5;">
    <div class="box" style="position: absolute; top: 15px; left: 20px; background: #bbf; border-color: blue; z-index: 1;">First box (z-index: 1)</div>
    <div class="box" style="position: absolute; top: 50px; left: 60px; background: #fbb; border-color: red;">Second box</div>
</div>
</pre>

```html
<div style="height: 4em; position: relative">
    <div class="box" style="position: absolute;
         top: 30px; left: 180px; z-index: 1">
         First box</div>
    <div class="box" style="position: absolute;
         top: 60px; left: 200px">
         Second box</div>
</div>
```

---

# Object hiding

  - Two possibilities
    1. `display: none`
       - The element is totally ignored during rendering
    2. `visibility: hidden`
       - The object occupies the place on the page but it is not displayed

---

# Visibility - example

<pre class="code-render" default-style="" resizable="true" style="width: 45%; height: 160px; float: right; z-index: 1">
<p>1. <code>display: none</code>:<br>
This is <span style="display: none">invisible</span> text. (gap removed)</p>
<p>2. <code>visibility: hidden</code>:<br>
This is <span style="visibility: hidden">invisible</span> text. (space preserved)</p>
</pre>

```html
This is <span style="...">invisible</span> text.
```

  1. `display: none`

This is invisible text. (gap removed)

  2. `visibility: hidden`

This is &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; text. (space preserved)

---

# Why to hide the text

  1. `display: none`
     - The elements displayed in browsers with no CSS support (alternative navigation, auxiliary labels, ...)
     - Element intended for other media types (e.g. for printing)
  2. `visibility: hidden`
     - The elements that may be displayed later (scripting)
