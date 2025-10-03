# Cascade of Rules

* For every *HTML element*, the browser takes **all CSS rules** whose selector matches the element.
    - Each rule defines the values of some CSS properties.
* The rules are *ordered* to a *cascade*.
* The *cascaded values* are used for computing the final visual properties of the element.

**Ordering criteria:**

<div>

1. Rule origin 
    * Author rules override the user agent styles.
2. **Rule selector specificity**
    * The more specific is the selector, the more important is the value
3. Order of specification 
    * If the rule has **equal origin and specificity**, the _latest_ specified value is used.

</div>

---

# Specificity

  * Specificity is a number `abcd`, where 
    * `a=1` in case of inline style, `a=0` otherwise
    * `b` is the number of `id` attributes in selector
    * `c` is the number of classes in selector
    * `d` is the number of element names in selector
  * `p.intro span { .... }`: 0 - 0 - 1 - 2 ~ **12**
  * `p span { .... }`: 0 - 0 - 0 - 2 ~ **2**

---

# Back to the Question

  * What color will have the text „important” ?

```html
@HTML@
<p class="intro">Following text is@@
    <span class="imp">important</span></p>@@
@/HTML@
``` ```html
@CSS@
p.intro span { @/color: red;/@ } @@
p span { @/color: blue;/@ font-weight: bold; } @@
@/CSS@
``` 
  * More specific rule wins => ?

---

# Back to the question (II)

  * What color will have the text „important” ?

```html
@HTML@
<p class="concl">Following text is@@
    <span class="imp">important</span></p>@@
@/HTML@
``` ```html
@CSS@
p.intro span { @/color: red;/@ } @@
p span { @/color: blue;/@ font-weight: bold; } @@
@/CSS@
``` 
  * Only one candidate => ?

---

# Back to the question (III)

  * What color will have the text „important” ?

```html
@HTML@
<p class="intro concl">Following text is@@
    <span class="imp">important</span></p>@@
@/HTML@
``` ```html
@CSS@
p.intro span { @/color: red;/@ } @@
p.concl span { @/color: blue;/@ font-weight: bold; } @@
@/CSS@
``` 
  * Definition order decides => ?

