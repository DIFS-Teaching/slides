# Practical CSS usage

---

# External Style Definitions

  - Use external style definitions 
    - One definition for a set of documents
  - Multiple style sheets may be used ```html
@HTML@
<link ="" rel="stylesheet" src="common.css" type="text/css"/>
<link ="" rel="stylesheet" src="section.css" type="text/css"/>
@/HTML@
```

---

# Distinguish between `id` and `class`

  - `id` attribute 
    - For unique elements
    - Easier to use (more specific selector)
    - Clearer style sheet
  - `class` attribute 
    - For repeating elements

---

# Class and id names

  - Use descriptive class and id names 
    - Should describe the **meaning** , not the appearance
    - Bad: `rightcolumn`, `redtext`
    - Correct: `menu`, `important`
  - Use a small set of class names 
    - Many names are hard to remember
    - Use context selectors
```html
@CSS@
p span.first {...} /* first letter of the paragraph */ 
p.first {...} /* first paragraph in the article */ 
li.first {...} /* first list item */ 
@/CSS@
```

---

# Context Selectors

  - Don't create useless classes, use context selectors
  - Wrong:

```html
@HTML@
<h2 class="articleheading">Heading</h2>
<p class="articlepar">...</p>
 ...
<p class="articlepar">...</p>
@/HTML@
``` ```html
@CSS@
.articleheading { ... }
.articlepar { ... }
@/CSS@
```

---

# Context Selectors

  - Right:

```html
@HTML@
<div class="article">
   <h2>Title</h2>
   <p>...</p>
   ...
   <p>...</p>
</div>
@/HTML@
``` ```html
@CSS@
.article h2 { ... }
.article p { ... }
@/CSS@
```

---

# Context Selectors

  - Wrong:

```html
@HTML@
<ul>
<li class="menu">...</li>
<li class="menu">...</li>
 ...
<li class="menu">...</li>
</ul>
@/HTML@
``` ```html
@CSS@
.menu { ... }
@/CSS@
```

---

# Context Selectors

  - Right:

```html
@HTML@
<ul class="menu">
<li>...</li>
<li>...</li>
 ...
<li>...</li>
</ul>
@/HTML@
``` ```html
@CSS@
ul.menu li { ... }
@/CSS@
```

---

# Combine Classes

  - Use more classes for one element
    - `class="importantmessage"` vs. `class="message important"`
  - Cascade the rules ```html
@CSS@
h1, h2 {
   font-family: "Arial CE", Arial, sans-serif;
   font-weight: bold;
}
h1 {
   font-size: 200%
}
h2 {
   font-size: 160%
}
@/CSS@
```

---

# Writing the Style Sheet

  - Write with a clear style
  - Choose some selector order 
    - Elements, id, classes, ...
    - Or according to the page organization
  - Choose some property specification order 
    - E.g. sizes, margins, position, colors and borders
  - Write rules to separate lines 
    - Easy to copy
  - Use comments `/* comment */`
