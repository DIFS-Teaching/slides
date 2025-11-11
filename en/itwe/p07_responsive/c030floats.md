<!-- .slide: class="section" -->
 
<header>
  <h1>Grid System: Floats</h1>
</header>

---

# 1. Rows

- blocks will be positioned into columns on rows -- class ***.row***

<br>

- necessary to address ***issues with floating elements:***
  - *clear: both* -- breaking floating (float) blocks after each row:
  ```css
  .row::after {
      content: "";
      clear: both;
  }
  ```
  - *overflow: hidden* -- some columns in a row may have a smaller height than the resulting row height
(columns of the next row could overlap the previous row):
  ```css
  .row {
      overflow: hidden;
  }
  ```

---

# 2. Columns

- elements will be organized into columns within a row:

<br>

- necessary to define classes for columns of different widths:
  ```css
  [class*="col-"] { float: left; }

  .col-1 { width: 25%; } /* 1/4 */
  .col-2 { width: 50%; } /* 2/4 */
  .col-3 { width: 75%; } /* 3/4 */
  .col-4 { width: 100%; } /* 4/4 */
  ```
  - the ***`float`*** property causes elements to float and align side by side 
  - the ***`width`*** property determines how much space a column will relatively occupy in a row
  - the number of columns can be chosen to best suit the specific problem
  - a *12-column layout* is often used (easily divisible)

---

# 2. Columns: HTML

- classes will be assigned to elements in the HTML document based on the desired layout:

```html
<div id="content" class="row">
  <div id="sidebar" class="col-1">
    <!-- 1/4 -->
  </div>
  <div id="article" class="col-3">
    <!-- 3/4 -->
  </div>
</div>
```

<pre class="code-render" default-style="
.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: '';
  clear: both;
}

[class*='col-'] {
  float: left;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

#sidebar {
  background-color: lightblue;
}

#article {
  background-color: lightpink;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 300px;">

<div id="content" class="row">
  <div id="sidebar" class="col-1">
    sidebar<br>1/4
  </div>
  <div id="article" class="col-3">
    article<br>3/4
  </div>
</div>

</pre>

<span class="note">💡 Test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats1.html"></div>

<div class="note"><a href="assets/examples/responsive/floats1.html">source</a></div>

---

# 3. Breakpoints

- use ***Media Queries*** for breakpoints for different browser window (viewport) widths
  - e.g., [Bootstrap breakpoints](https://getbootstrap.com/docs/5.3/layout/breakpoints/), ...

```css
/* Small devices – default display */
[class*="col-"] { float: left; width: 100%; }

/* Medium devices (tablet) */
@media only screen and (min-width: 768px) {
  .col-md-1 { width: 25%; }
  .col-md-2 { width: 50%; }
  ...
}

/* Large devices (PC) */
@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; }
  .col-md-2 { width: 50%; }
  ...
}
```

---

# 3. Breakpoints: HTML

- classes will be assigned to elements in the HTML document based on the desired layout<br> for different width groups:

```html
<div id="content" class="row">
  <div id="sidebar" class="col-md-2 col-lg-1">
  </div>
  <div id="article" class="col-md-2 col-lg-3">
  </div>
</div>
```

<pre class="code-render" default-style="

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: '';
  clear: both;
}

[class*='col-'] {
  float: left;
  width: 100%;
  height: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

#sidebar {
  background-color: lightblue;
}

#article {
  background-color: lightpink;
}

[class*='col-']::after {
  content: '100%'
}

@media only screen and (min-width: 768px) {
  .col-md-1 { width: 25%; } /* 1/4 */
  .col-md-2 { width: 50%; } /* 2/4 */
  .col-md-3 { width: 75%; } /* 3/4 */
  .col-md-4 { width: 100%; } /* 4/4 */
  .col-md-1::after { content: '1/4' }
  .col-md-2::after { content: '2/4' }
  .col-md-3::after { content: '3/4' }
  .col-md-4::after { content: '4/4' }
}

@media only screen and (min-width: 1200px) {
  .col-lg-1 { width: 25%; } /* 1/4 */
  .col-lg-2 { width: 50%; } /* 2/4 */
  .col-lg-3 { width: 75%; } /* 3/4 */
  .col-lg-4 { width: 100%; } /* 4/4 */
  .col-lg-1::after { content: '1/4' }
  .col-lg-2::after { content: '2/4' }
  .col-lg-3::after { content: '3/4' }
  .col-lg-4::after { content: '4/4' }
}

" resizable="true" style="height: 300px;">

<div id="content" class="row">
  <div id="sidebar" class="col-lg-1 col-md-2">
    sidebar
  </div>
  <div id="article" class="col-lg-3 col-md-2">
    article
  </div>
</div>

</pre>

<span class="note">💡 Test different example widths</span>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats2.html"></div>

<div class="note"><a href="assets/examples/responsive/floats2.html">source</a></div>

---

# 4. Border and Padding

- often, we want to set some ***`padding`*** or ***`border`*** for blocks positioned into columns

<pre class="code-render" default-style="

.row {
  overflow: hidden;
  border: 4px solid blue;
}

.row::after {
  content: ' ';
  clear: both;
}

[class*='col-'] {
  float: left;
  border: 0px solid red;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: green;
}

.row > *:nth-child(odd) {
   color: black;
}

.row > *:nth-child(even) {
   color: gray;
}

p {
  font-size: 14px;
  text-align: justify;
  margin: 0;
  background-color: white;
}

#form {
  margin-bottom: .5rem;
}

input {
  font-size: 24px;
}

.col-1 { width: 25%; } /* 1/4 */
.col-2 { width: 50%; } /* 2/4 */
.col-3 { width: 75%; } /* 3/4 */
.col-4 { width: 100%; } /* 4/4 */

" resizable="true" style="height: 600px;">

<div id="form">
  border: <input id="border-width" type="number" min="0" value="0">
  padding: <input id="padding" type="number" min="0" value="0">
</div>

<div id="content" class="row">
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
  <div class="col-1">
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur tempus faucibus libero, sed ultricies  ectus iaculis ut. Suspendisse tincidunt lorem sed leo tempus, vitae euismod eros dictum. In enim elit,  aucibus et turpis quis, pretium pretium metus. Nulla ornare purus id sollicitudin ornare. Vivamus ac magna in lacus facilisis molestie. Sed dapibus nulla dignissim elit hendrerit viverra. Morbi rhoncus tristique erat ac scelerisque. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean at semper enim. Praesent ac augue non dolor aliquam blandit. Pellentesque ullamcorper diam nec massa luctus, a viverra neque vulputate.
    </p>
  </div>
</div>

<script>
  function setListener(type) {
  let elem = document.getElementById(type);
  if(elem) {
    elem.addEventListener("change", (e) => {
    let cols = document.querySelectorAll("[class*='col-']");
    for(let i = 0; i < cols.length; i++) {
      cols[i].style[type] = elem.value + "px";
    }
    });
  }
  }

  setListener("border-width");
  setListener("padding");
</script>

</pre>

<div style="text-align: center; margin-top: 4rem">

**Actual box width** = <span style="color: lightgray">`margin`</span> + <span style="color: red">`border`</span> + <span style="color: green">`padding`</span> + `width`

</div>

=--

<!-- .slide: class="editor" -->

# Example

<div data-iframe="assets/examples/responsive/floats3.html"></div>

<div class="note"><a href="assets/examples/responsive/floats3.html">source</a></div>

---

# Summary

- a way to create a Grid system when Flexbox and Grid were not available

<br>

- ***disadvantages***:
  - need to set `overflow` and `clear` properties
  - column height may not fill the row height
  - floating elements are generally better suited for text wrapping, not layout creation
  - gaps between columns must be handled using `padding`

<br>

- Solution: ***Flexbox***
