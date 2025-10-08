<!-- .slide: class="section" -->

# Styling the Block Elements

---

# Box model

  * A model that describes the dimensions of any object on the page
  * Box model parts: 
    * Content width and height
    * Border width
    * Margins
  * There are corresponging CSS properties for each part

---

# Box model

<pre class="code-render" default-style="" resizable="false" style="height: 20em;">
<div class="textbox" style="border-style: dashed; box-shadow: none; text-align: center; font-family: sans-serif; padding: 2em">
	<span title="Outer margin, always transparent">Margin</span>
	<div style="background-color: gray; border: 10px solid green; padding: 0.5em 2em; margin-top: 1em">
		<span title="Inner padding, background color (image)">Padding</span>
		<div style="background-color: white; color: black; padding: 3em 0em; margin: 1em;">
			Element content
			<br/><br/>
			<code style="color: red;">&lt;-----------------&nbsp;width&nbsp;-----------------&gt;</code>
		</div>		
		<div style="width: 4em; background-color: #057205ff; color: white; position: relative; left: -1.5em; top: 1.1em;">border</div>
	</div>
</div>
</pre>

---

# Content width and height

* **Inline elements**
  * Always computed automatically
* **Block elements**
  * Set explicitly using the `width` a `height` properties
  * Computed from remaining features: 
    * Size of the parent element
    * Content size
    * Margins and borders
* **Root element** (`<html>`) 
  * The size is given by the browser window size

---

# Content width and height

  * Width 
    * `width: auto`
    * `width: 120px`
    * `width: 60%`
  * Height 
    * `height: auto`
    * `height: 30px`
    * `height: 80%`

---

# Minimal width and height

* Maximal size 
  * `max-width: 20em;`
  * `max-height: 50em;`
* Minimal size 
  * `min-width: 20em;`
  * `min-height: 50em;`
* Application order 
  * `width` -> `max-width` -> `min-width`

---

# Margin

  * For individual sides 
    * `margin-top:`, `margin-bottom:`
    * `margin-left:`, `margin-right:`
  * At once 
    * `margin: 2em 1em 3em 2em` \- top, right, bottom, left
    * `margin: 2em 1em 1em` \- top, right&left, bottom
    * `margin: 2em 1.5em` \- top&bottom, right&left
    * `margin: 1em` \- all

---

# Padding

  * For individual sides 
    * `padding-top:`, `padding-bottom:`
    * `padding-left:`, `padding-right:`
  * At once 
    * `padding: 2em 1em 3em 2em` \- top, right, bottom, left
    * `padding: 2em 1em 1em` \- top, right&left, bottom
    * `padding: 2em 1.5em` \- top&bottom, right&left
    * `padding: 1em` \- all

---

# `auto` Values

  * The `margin`, `width` and `height` properties may have the value of `auto`
    * `width` and `height` are set to `auto` by default
    * For `margin` the default is 0 but `auto` can be used
  * The real values for the `auto` properties are computed automatically
  * The algorithm depends on the layout mode

---

# Layout Modes

* **Normal flow** (default)
  * So called _in-flow_ elements
  * Elements are laid out in the document order
  * Inline elements on the lines, block elements below each other
* Other layout modes
  * Floating blocks
  * Positioned elements
  * Flexbox, Grid layout
  * ... will be explained later

---

# Block Width in Normal Flow

  * _The block always occupies the whole width of its containing block (roughly its parent block)_
    * The whole viewport width for the root element
  * We may define:  
margin-left + border-left-width +  
\+ padding-left + width + padding-right +  
\+ border-right-width + margin-right = _containing_block_width_
  * This allows computing the eventual `auto` values
  * If none of the values is `auto`, the _right margin_ specfication is ignored and computed automatically

=--

# Box model

<pre class="code-render" default-style="" resizable="false" style="height: 20em;">
<div class="textbox" style="border-style: dashed; box-shadow: none; text-align: center; font-family: sans-serif; padding: 2em">
	<span title="Outer margin, always transparent">Margin</span>
	<div style="background-color: gray; border: 10px solid green; padding: 0.5em 2em; margin-top: 1em">
		<span title="Inner padding, background color (image)">Padding</span>
		<div style="background-color: white; color: black; padding: 3em 0em; margin: 1em;">
			Element content
			<br/><br/>
			<code style="color: red;">&lt;-----------------&nbsp;width&nbsp;-----------------&gt;</code>
		</div>		
		<div style="width: 4em; background-color: #057205ff; color: white; position: relative; left: -1.5em; top: 1.1em;">border</div>
	</div>
</div>
</pre>

---

# Computation of `auto` values

  * When a single value is `auto`, it is computed from the equation
  * If the width is not set (`width=auto`), the `auto` values of margins are interpreted as `0`
  * If both the left and right margins are `auto` and the width is set, their final values are equal (`margin-left = margin-right`) => _block centering_

---

# Block height

  * When `height=auto`, the height is computed automatically so that all the content fits the block 
    * Normally, only in-flow content is considered
    * This may be changed by setting the `overflow` property
  * For `margin-top` and `margin-bottom`, the `auto` value is always interpreted as `0`

---

# Margin Collapsing

* **Horizontal** margins are **never collapsed**
* **Vertical** adjacent margins are collapsed 
    * For two **non-floating** blocks placed below each other
    * For two nested blocks (top or bottom margin) 
        * Top margin only if the nested object has `clear: none`
    * Empty blocks (top and bottom margin)
* The resulting margin is the **maximum** of the margins being collapsed
* [Example](data/collapse1.html)

---

# Content trimming

  * The `overflow` property - what to do when the content doesn't fit. 
    * `overflow: visible` \- let overflow (default)
    * `overflow: hidden` \- trims the rest
    * `overflow: scroll` \- display scrollbars
    * `overflow: auto` \- display scrollbars if needed 

```html
@HTML@
<div style="width: 5em; height: 6em;@@            border: 2px solid white;">@@
A box containing a very long text.@@
</div>
@/HTML@
```

---

# Trimming example

`overflow: visible` |  A box containing a looooooooooooong text.   
---|---  
`overflow: hidden` |  A box containing a looooooooooooong text.   
`overflow: scroll` |  A box containing a looooooooooooong text.   
`overflow: auto` |  A box containing a looooooooooooong text.

