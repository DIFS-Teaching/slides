# Table style

  - We can change the style of
    - The whole table - `<table>`
    - Rows - `<tr>`
    - Cells - `<td>`, `<th>`
    - Columns - `<col>`, `<colgroup>`
    - Header, footer, body - `<thead>`, `<tfoot>`, `<tbody>`
    - Caption - `<caption>`

---

# Selectors

  - Usually context selectors
    - `table { ... }`
    - `table td { ... }`
    - `table.results td { ... }`
    - `table th.main { ... }`
    - `table tr#row1 { ... }`
  - Using cascade:
    - `tr { ... }`
    - `table.results tr { ... }`

---

# Table captions - `<caption>`

  - Caption position
    - `caption-side: top`
    - `caption-side: bottom`
    - `caption-side: left`
    - `caption-side: right`
  - Other properties
    - `text-align`
    - `vertical-align`
    - `width`

---

# Table caption -- example

<pre class="code-render" default-style="
table {
    border-collapse: collapse;
    border: 1px solid #aaa;
    margin-bottom: 1.5em;
}
td, th { padding: 0.2em 0.8em; border: 1px solid #ccc; }
caption { font-weight: bold; font-style: italic; }
.top caption { caption-side: top; }
.bottom caption { caption-side: bottom; }
" resizable="true" style="height: 300px; width: 90%; margin: auto">
<table class="top">
    <caption>Tab 1. Caption on the top</caption>
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<table class="bottom">
    <caption>Tab 2. Caption at the bottom</caption>
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
</pre>

```css
.top caption { caption-side: top; }
.bottom caption { caption-side: bottom; }
```

---

# Borders in a table

  - Borders can be set separately for the cells or the whole table
  - Special properties:
    - `border-collapse: separate | collapse` \- cell border merging
    - `border-spacing: 5px` \- cell border spacing
    - `empty-cells: show | hide` \- whether to diplay or not the empty cells

---

# Border Examples

<pre class="code-render" default-style="
table { margin-bottom: 0.8em; font-size: 0.85em; }
td, th { padding: 0.15em 0.5em; }
.t1 { border-collapse: separate; border: 1px solid #999; }
.t1 td, .t1 th { border: 1px solid #999; }
.t2 { border-collapse: collapse; border: 1px solid #999; }
.t2 td, .t2 th { border: 1px solid #999; }
.t3 { border-collapse: collapse; }
.t3 tr { border-top: 1px solid #555; }
.t4 { border: 1px solid #555; border-collapse: collapse; }
.t4 th { border: 1px solid #555; }
.t4 td { border: none; border-left: 1px solid #555; }
" resizable="true" style="height: 420px; width: 90%; margin: auto">
<p><code>border-collapse: separate</code></p>
<table class="t1">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<p><code>border-collapse: collapse</code></p>
<table class="t2">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<p><code>tr { border-top: 1px solid }</code> (rows only)</p>
<table class="t3">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
<p><code>table + th border, td left border only</code></p>
<table class="t4">
    <tr><th>Name</th><th>Surname</th></tr>
    <tr><td>John</td><td>Wayne</td></tr>
    <tr><td>Albert</td><td>Einstein</td></tr>
</table>
</pre>

```css
/* separate borders (default) */
table { border-collapse: separate; }
/* merged borders */
table { border-collapse: collapse; }
/* horizontal lines only */
table tr { border-top: 1px solid; }
/* full outer + left cell borders */
table { border: 1px solid; }
table th { border: 1px solid; }
table td { border: none; border-left: 1px solid; }
```

---

# Table and cell background

  - Each layer is either transparant (`border-color: transparent`) or it has a colour or an image assigned
  - The layers go in following order (bottom to top)
    1. Table `<table>`
    2. Column groups `<colgroup>`
    3. Columns `<col>`
    4. Row groups `<thead>`, `<tbody>`, `<tfoot>`
    5. Rows `<tr>`
    6. Cells `<td>`, `<th>`

---

# List styling

  - The list items can be style (ordered or unordered)
  - We can define
    - **Bullet type** (unordered)
    - **Numbering type** (ordered)
    - **An image instead of the bullet**
    - **Bullet position** (inside or outside)

---

# Bullet and Numbering Types

<pre class="code-render" default-style="
.col { display: inline-block; vertical-align: top; width: 45%; margin-right: 4%; }
ul, ol { margin: 0.2em 0 0.2em 2em; }
li { margin-bottom: 0.2em; }
" resizable="true" style="height: 360px; width: 90%; margin: auto">
<div class="col">
    <strong>Unordered (<code>ul</code>)</strong>
    <ul style="list-style-type: disc"><li>disc (default)</li></ul>
    <ul style="list-style-type: circle"><li>circle</li></ul>
    <ul style="list-style-type: square"><li>square</li></ul>
    <ul style="list-style-type: none"><li>none</li></ul>
</div>
<div class="col">
    <strong>Ordered (<code>ol</code>)</strong>
    <ol style="list-style-type: decimal"><li>decimal</li></ol>
    <ol style="list-style-type: lower-roman"><li>lower-roman</li></ol>
    <ol style="list-style-type: upper-roman"><li>upper-roman</li></ol>
    <ol style="list-style-type: lower-alpha"><li>lower-alpha</li></ol>
    <ol style="list-style-type: upper-alpha"><li>upper-alpha</li></ol>
    <ol style="list-style-type: none"><li>none</li></ol>
</div>
</pre>

  - The `list-style-type` property — applied to the `<li>` element

```css
ul li { list-style-type: square; }
ol li { list-style-type: lower-roman; }
```

---

# Images instead of the bullets

  - The `list-style-image` property

<pre class="code-render" default-style="
ul li {
    list-style-image: url('data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%2210%22 height=%2210%22%3E%3Ccircle cx=%225%22 cy=%225%22 r=%224%22 fill=%22%23e44%22/%3E%3C/svg%3E');
}
" resizable="true" style="width: 45%; height: 130px; float: right; z-index: 1">
<ul>
    <li>List item one</li>
    <li>List item two</li>
    <li>List item three</li>
</ul>
</pre>

```html
<ul>
    <li style="list-style-image: url('ok.gif')">
        List item</li>
</ul>
```

---

# Bullet position

  - The `list-style-position` property

<pre class="code-render" default-style="
.outside { list-style-position: outside; background: #eef; }
.inside { list-style-position: inside; background: #efe; }
ul { width: 18em; margin: 0.3em auto; padding-left: 2em; }
" resizable="true" style="height: 220px; width: 90%; margin: auto">
<p><code>list-style-position: outside</code> (default):</p>
<ul class="outside">
    <li>First item in longer text in longer text in longer text in longer text...</li>
</ul>
<p><code>list-style-position: inside</code>:</p>
<ul class="inside">
    <li>First item in longer text in longer text in longer text in longer text...</li>
</ul>
</pre>

---

# The `list-style` property

  - Sumarizes the `list-style-*` properties
  - Format:
    - `list-style: type position image`
  - Examples:
    - `list-style: square inside none`
    - `list-style: lower-alpha outside url("obr.gif")`

---

# Mouse cursor

  - The `cursor` property allows to change the mouse cursor look when placed over the particular element on the page.

<pre class="code-render" default-style="" resizable="true" style="width: 45%; height: 100px; float: right; z-index: 1">
The cursor over this
<span style="cursor: crosshair">word</span>
has a different shape.
</pre>

```html
The cursor over this
<span style="cursor: crosshair">word</span>
has a different shape.
```

---

# Cursor types

auto| crosshair| default
---|---|---
hand| pointer| move
text| wait| help
nw-resize| n-resize| ne-resize
---|---|---
w-resize| | e-resize
sw-resize| s-resize| se-resize

  - Pointer cursor for all the browsers:
    - `cursor: pointer; cursor: hand`

---

# Pseudo Elements and Classes

  - Abstract class for denoting special elements or their state
  - They define the look of various parts
    - **Pseudo classes** : in different states
      - E.g. links visited, not visited, focused, etc.
      - Specificity as for classes
    - **Pseudo elements** : different parts of elements
      - First element, first letter, before, after, ...
      - Specificity as for elements
  - Denoted by „:"
    - `p:first-letter { font-size: 20px; }`

---

# Pseudo Classes: Link Style

  - Static (relatively)
    - Not visited link:
`a:link { color: green; }`
    - Visited link:
`a:visited { color: red; }`
  - Dynamic
    - Mouse moved over:
`a:hover { ... }`
    - Link activation:
`a:active { ... }`
    - Keyboar focus:
`a:focus { ... }`

---

# Typical Link Style

  - Highlighted by color, underlines on moving mouse over
  - It gets highlighed when activated, gets darker when visited

<pre class="code-render" default-style="
a { color: #aaf; text-decoration: none; }
a:link { }
a:visited { color: #339; }
a:hover { text-decoration: underline; }
a:active { text-decoration: underline; color: red; }
" resizable="true" style="width: 45%; height: 100px; float: right; z-index: 1">
Example: <a href="#">Sample link</a>.
</pre>

```css
a { color: #aaf; text-decoration: none; }
a:link { }
a:visited { color: #339; }
a:hover { text-decoration: underline; }
a:active { text-decoration: underline; color: red; }
```

---

# Some tricks about links

  - Element `<a>` always belongs to some pseudoclass
    - It's changing according to circumstances
  - Rule `a { ... }` has lower priority than the rules with a pseudoclass
    - Pseudoclass has the same specificity as a class
  - The `a` rule cannot redefine the properties already defined for pseudoclasses

---

# Pseudo Class :first-child

  - The first child element of its parent element

<pre class="code-render" default-style="
.menu li { color: green; }
.menu li:first-child { color: blue; }
" resizable="true" style="width: 40%; height: 150px; float: right; z-index: 1">
<ul class="menu">
    <li>Blue item</li>
    <li>Green item</li>
    <li>Green item</li>
</ul>
</pre>

```html
<ul class="menu">
    <li>Blue item</li>
    <li>Green item</li>
    <li>Green item</li>
</ul>
```

```css
.menu li { color: green; }
.menu li:first-child { color: blue; }
```

  - Similarly `last-child`, much more in CSS3

---

# Pseudo Elements: Firtst Letters and Lines

  - Element `:first-line`
    - Denotes the first line of an arbitrary element
    - E.g. `p:first-line` \- first line of a paragraph
    - Depends on the window width, font size, ...
  - Element `:first-letter`
    - Denotes first letter of an element
    - E.g. `p:first-letter` \- first letter of a paragraph

---

# Example 1

<pre class="code-render" default-style="
p { text-transform: none; }
p:first-line { text-transform: uppercase; }
" resizable="true" style="width: 45%; height: 150px; float: right; z-index: 1">
<p>First line of this paragraph will be in capital letters. Any text follows. Any text follows. Any text follows.</p>
</pre>

```css
p { text-transform: none; }
p:first-line { text-transform: uppercase; }
```

```html
<p>First line of this line will
be in capital letters. Any text follows. Any text follows.
Any text follows.</p>
```

---

# Example 2

<pre class="code-render" default-style="
p:first-letter {
    font-size: 200%;
    font-weight: bold;
    float: left;
}
" resizable="true" style="width: 45%; height: 160px; float: right; z-index: 1">
<p>First letter will be large and floated by the remaining text. Other text as normal. Other text as normal. Other text as normal.</p>
</pre>

```css
p:first-letter {
    font-size: 200%;
    font-weight: bold;
    float: left;
}
```

```html
<p>First letter will be large and floated
by the remaining text. Other text as normal. Other text as normal.
Other text as normal.</p>
```

---

# Generated content

  - Low support in browsers (missing in MSIE)
  - Allows to generate a text that is not present in the document
  - Pseudo-elements `:before` a `:after`
    - `:before` \- add a text before the element contents
    - `:after` \- after the text contents
  - The `content:` property
    - The text string to be inserted

---

# Example

<pre class="code-render" default-style="
div.remark:before {
    content: 'Remark: ';
    font-weight: bold;
}
" resizable="true" style="width: 45%; height: 100px; float: right; z-index: 1">
<div class="remark">This rule doesn't always apply.</div>
</pre>

```css
div.remark:before {
    content: "Remark: ";
    font-weight: bold;
}
```

```html
<div class="pozn">This rule doesn't always apply.</div>
```
