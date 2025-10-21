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

Tab 1. Caption on the top Name | Surname  
---|---  
John | Wayne  
Albert | Einstein  
Tab 2. Caption in the bottom Name | Surname  
---|---  
John | Wayne  
Albert | Einstein

---

# Borders in a table  
  
  - Borders can be set separately for the cells or the whole table
  - Special properties: 
    - `border-collapse: separate | collapse` \- cell border merging
    - `border-spacing: 5px` \- cell border spacing
    - `empty-cells: show | hide` \- whether to diplay or not the empty cells

---

# Examples

`table { border-collapse: separate }` Name | Surname  
---|---  
John | Wayne  
Albert | Einstein  
`table { border-collapse: collapse }` Name | Surname  
---|---  
John | Wayne  
Albert | Einstein

---

# Examples  
  
`table tr { border-top: 1px solid }` Name | Surname  
---|---  
John | Wayne  
Albert | Einstein  
`table tr { border: 1px solid }` Name | Surname  
---|---  
John | Wayne  
Albert | Einstein

---

# Examples  
  
` @CSS@ table { border: 1px solid }@@ table th { border: 1px solid }@@ table td { border: none;@@ border-left: 1px solid; } @/CSS@ ` Name | Surname  
---|---  
John | Wayne  
Albert | Einstein

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

# Bullet type

  - The `list-style-type` property
  - Applied to the `<li>` element ```html
@CSS@
ul li { list-style-type: square; }
@/CSS@
``` 
  - Unordered lists: 
    - `list-style-type: disc`
    - `list-style-type: circle`
    - `list-style-type: square`

---

# Numbering type

  - The `list-style-type` property
  - Ordered lists: 
    - `list-style-type: decimal`
    - `list-style-type: lower-roman`
    - `list-style-type: upper-roman`
    - `list-style-type: lower-alpha`
    - `list-style-type: upper-alpha`
    - `list-style-type: none`

---

# Images instead of the bullets

  - The `list-style-image` property

```html
@HTML@
<ul>@@
<li style="list-style-image: url('ok.gif')">@@
List item</li>@@
</ul>@@
@/HTML@
``` 

  - List item

---

# Bullet position

  - The `list-style-position` property
  - `list-style position: outside`
    - First item in longer text in longer text in longer text in longer text in longer text...
    - First item in longer text in longer text in longer text in longer text in longer text...
  - `list-style position: inside`
    - First item in longer text in longer text in longer text in longer text in longer text...
    - First item in longer text in longer text in longer text in longer text in longer text...

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

```html
@HTML@
The cursor over this@@
<span style="cursor: crosshair">word</span>@@
has a different shape.@@
@/HTML@
``` 

The cursor over this word has a different shape.

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
  - Denoted by „:” 
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

```html
@CSS@
a { color: #aaf; text-decoration: none; }@@
a:link { }@@
a:visited { color: #339; }@@
a:hover { text-decoration: underline; }@@
a:active { text-decoration: underline; color: red; }@@
@/CSS@
``` 

Example: Sample link.

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

```html
@HTML@
<ul class="menu">@@
<li>Blue item</li>@@
<li>Green item</li>@@
<li>Green item</li>@@
</ul>
``` @/HTML@ 

```html
@CSS@
.menu li { color: green; }@@
.menu li:first-child { color: blue; }
@/CSS@
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

```html
@CSS@
p { text-transform: none; }@@
p:first-line { text-transform: uppercase; }@@
@/CSS@
@HTML@
@@
<p>First line of this line will@@
be in capital letters. Any text follows. Any text follows.
Any text follows.</p>
@/HTML@
``` 

First line of this line will be in capital letters. Any text follows. Any text follows. Any text follows.

---

# Example 2

```html
@CSS@
p:first-letter {@@
    font-size: 200%;@@
    font-weight: bold;@@
    float: left;@@
}@@
@/CSS@
@HTML@
@@
<p>First letter will be large and floated@@
by the remaining text. Other text as normal. Other text as normal.@@
Other text as normal.</p>
@/HTML@
``` 

First letter will be large and floated by the remaining text. Other text as normal. Other text as normal. Other text as normal.

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

```html
@CSS@
div.remark:before {@@
    content: "Remark: ";@@
    font-weight: bold;@@
}@@
@/CSS@
@HTML@
@@
<div class="pozn">This rule doesn't always apply.</div>
@/HTML@
``` 

This rule doesn't always apply.
