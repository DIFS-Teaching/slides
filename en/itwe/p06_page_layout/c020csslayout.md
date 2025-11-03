# CSS Layout

  - Visual blocks are created mostly using the sectioning HTML elements 
    - Semantic elements `<header>`, `<footer>`, `<article>`, ...
    - The `<div>` element for remaining parts
    - The `id` and `class` attributes
  - The positions of the elements is defined by CSS 
    - Width and height
    - Margins
    - Floating blocks
    - Positioning (absolute or relative)

---

# Page width

  - Full width 
    - Standard state (minimal margins)
  - Narrowed page with a margin 
    - The width depends on the window size
    - Specified relatively (percentage)
  - Fixed width 
    - The width is specified absolutely

---

# Design aspects

  - We are limited with the actual screen width
  - Wide range of browsing devices 
    - Desktop even 2560px, mobile phone 320px
  - It's inconvenient to read long text lines 
    - Use narrow lines
    - Greater font
    - More columns

---

# Narrowed centered page

```html
<body>
    <div id="content">
        ... page content ....
    </div>
</body>
```

---

# Narrowed centered page

```css
body {
    margin: 0; padding: 1em;
}
#content {
    width: 80%;
    @/margin: auto;/@ 
    padding: 1em;
}
```

[Example](data/page_w_rel.html)

---

# Fixed width

```css
body {
    margin: 0; padding: 1em;
}
#content {
    @/width: 1000px;/@ 
    margin: auto;
    text-align: left;
    padding: 1em;
}
```

[Example](data/page_w_abs.html)

---

# Positioning the elements side-by-side

  - With tables: for small local areas 
    - Fixed small parts of the page, form fields, ...
    - Easy to set up
  - Absolute positioning
  - Floating objects
  - Special `display:` values

---

# Absolute positioning

  - Left element has absolute position
  - Right element has a right margin
  - [Example](data/pos1.html)

```css
#left {
    width: 5em;
    position: absolute;
    left: 0; top: 0;
}
#right {
    margin-left: 5em;
}
```

---

# Absolute positioning

- Disadvantages 
  - How to determine the vertical position? (enclose into a DIV)
  - Absolutely positioned element can overlap preceding a following text

---

# Absolute positioning (II)

- Absolute positioning within a parent element 
  - The parent element must have _position: relative_
  - [Example](data/pos1b.html)

```css
#content {
    width: 80%; margin: auto;
    position: relative;
}
#menu {
    width: 140px;
    position: absolute;
    right: -70px; top: 30px;
}
```

---

# Floating Blocks

- Left element is floating
- Right element is flowing around
- [Example](data/pos2.html)

```css
#left {
    width: 5em;
    float: left;
}
#right {
    width: 10em;
}
``` 
- Complications when the heights are different: [example](data/pos2b.html)

---

# Floating Blocks (II)

- Solution: left margin
- [Example](data/pos2c.html)

```css
#left {
    width: 5em;
    float: left;
}
#right {
    width: 10em;
    margin-left: 5em;
}
```

---

# All Blocks Floating

- [Problem:](data/pos3a.html) the `clear:` property cannot be used in the contents
- [Solution:](data/pos3b.html) both (all) blocks floating 
  - They are placed side by side from the left
  - [Any number of blocks (columns)](data/pos3c.html)

```css
#levy {
    width: 5em;
    float: left;
}
#pravy {
    width: 10em;
    float: left;
}
```

---

# Three-column layout

- Traditional page layout
- Usually the columns: menu - content - additional info
- Typicaly solved by a table (trivial) 
  - All the disadvantages of tables (slow)
- A bit complicated using CSS

---

# Three-column layout (II)

- Principle: 
  - Left column: floating left, fixed width and height
  - Right column: similarly, floating right
  - Content: eventual margins
  - Footer: `clear: both`
- Variants: 
  - All the columns may have `float: left`
  - An enclosing “container” block with `overflow: hidden`
- Problems 
  - The height of columns doesn't meet the width of content 
    - May be solved by a color background
    - [Example](http://www.pixy.cz/blogg/clanky/css-3col-layout/) (Petr Stanicek)

---

# Special `display` Property Values

- Inline block `display: inline-block`
  - Blocks positioned as inline elements
- Table cells `display: table-cell`
  - They create an _anonymous table_
  - Similarly `table-row`, `table`, `inline-table`
- [Examples](data/pos4a.html)
