# Floating blocks

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

# Creating a Floating Object

<pre class="code-render" default-style="
#menu {
    background-color: #eef;
    border: 1px solid #aaf;
    width: 12em;
    padding: 0;
    margin-right: 1em;
}
#menu h1 {
    font-weight: bold;
    font-size: 100%;
    color: #fff;
    background-color: #55f;
    margin: 0;
    padding: 0.5em;
}
.floating { float: left; }
" resizable="true" style="width: 45%; height: 300px; float: right; z-index: 1">
<div class="floating" id="menu">
    <h1>Menu</h1>
    <ul>
        <li>Red</li>
        <li>Green</li>
        <li>Magenta</li>
        <li>Yellow</li>
        <li>Dark blue</li>
    </ul>
</div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut.</p>
<p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident.</p>
</pre>

```css
#menu {
    background-color: #eef;
    border: 1px solid #aaf;
    width: 12em;
    padding: 0;
    margin-right: 1em;
}
#menu h1 {
    font-weight: bold;
    font-size: 100%;
    color: #fff;
    background-color: #55f;
    margin: 0;
    padding: 0.5em;
}
.floating { float: left; }
```

```html
<div class="floating" id="menu">
    <h1>Menu</h1>
    <ul>...</ul>
</div>
<p>text...</p>
```

---

# Float and In-Flow Block Size

<pre class="code-render" default-style="
#menu {
    background-color: #eef;
    border: 1px solid #aaf;
    width: 12em;
    padding: 0;
    margin-right: 1em;
}
.floating { float: left; }
p { border: 5px solid red; }
" resizable="true" style="width: 45%; height: 260px; float: right; z-index: 1">
<div class="floating" id="menu">
    <ul>
        <li>Red</li>
        <li>Green</li>
        <li>Magenta</li>
    </ul>
</div>
<p>The paragraph block box extends behind the floating element — the red border reveals its full width.</p>
</pre>

  - A `<p>` element is a **block** — its box covers the full width, even behind the float
  - The text *wraps around* the float, but the **block box** doesn't shrink

```css
.floating { float: left; }
p { border: 5px solid red; }
```

---

# Clear

  - The floating objects are placed by the browser
    - Side by side to the appropriate margin
    - When there is no space then below each other
    - => The floating object can horizontally overflow the flowing text
  - When some text shouldn't flow along the floating objects:
    - `clear: left | right | both`
  - First, previous floating object are placed, then the text is placed below

<pre class="code-render" default-style="
.box {
    float: left;
    width: 8em;
    background: #ddf;
    border: 1px solid #aaf;
    margin-right: 1em;
    padding: 0.5em;
}
.cleared { clear: both; border-top: 2px solid red; padding-top: 0.3em; }
" resizable="true" style="height: 200px; width: 90%; margin: auto">
<div class="box">Float 1</div>
<div class="box">Float 2</div>
<p class="cleared">This paragraph has <code>clear: both</code> — starts below both floats.</p>
<p>This paragraph has no clear — wraps around the floats.</p>
</pre>

---

# Containing Block Height

  - When a block has `height:auto`, its height depends on its contents
  - For `overflow: visible`
    - Only in-flow content is considered
    - If the block contains floating blocks only, it has a **zero height** in the result
  - Otherwise (e.g. `overflow: hidden`)
    - Floating content is considered too

<pre class="code-render" default-style="
.contents {
    border: 5px solid blue;
    margin-bottom: 1em;
}
.col {
    float: left;
    background: gray;
    color: white;
    padding: 0.5em;
    margin-right: 0.3em;
}
.visible { overflow: visible; }
.hidden { overflow: hidden; }
" resizable="true" style="height: 270px; width: 90%; margin: auto">
<p><strong>overflow: visible</strong> — blue border collapses to zero height:</p>
<div class="contents visible">
    <div class="col">Column 1</div>
    <div class="col">Column 2</div>
</div>
<p style="clear:both"><strong>overflow: hidden</strong> — blue border wraps the floats:</p>
<div class="contents hidden">
    <div class="col">Column 1</div>
    <div class="col">Column 2</div>
</div>
<p style="clear:both">Next contents</p>
</pre>
