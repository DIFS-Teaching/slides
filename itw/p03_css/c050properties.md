<!-- .slide: class="section" -->

<header>
	<h1>Vlastnosti</h1>
	<p>úvod, principy</p>
</header>

---

# Vlastnost

- určuje jak se vybrané elementy zobrazí (barva, rozměry, rozložení, písmo, animace atd.)
  - např. `color`, `font-size`, `margin`, `display`, ...
- množina vlastností je definována ve **[W3C CSS specifikaci](https://www.w3.org/Style/CSS/current-work)**

```css
color: blue;
font-size: 12pt;
```

- vlastnosti mají různé jednotky a formáty hodnot, někdy i experimentální varianty s prefixy
  - `-webkit-` Chrome, Safari (WebKit)
  - `-moz-` Firefox (Mozilla)
  - `-ms-` Internet Explorer, Edge (Trident/EdgeHTML)
  - `-o-` Opera (starý Presto engine)

---

# Typy vlastností

  - ***typografie a text*** -- ovlivňují písmo a textový obsah
    - `font-family`, `font-size`, `font-weight`, `color`, `text-align`, `line-height`, ...
  - ***barvy a pozadí*** -- řídí vzhled pozadí a barevné schéma
    - `background-color`, `background-image`, `background-position`, `opacity`, ...
  - ***box model (rozměry a okraje)*** - určují velikost, vnější a vnitřní odsazení, rámečky
    - `width`, `height`, `margin`, `padding`, `border`, `box-sizing`, ...
  - ***rozložení a pozicování (layout)*** -- ovlivňují, jak se elementy skládají a zarovnávají
    - `display`, `position`, `float`, `z-index`, ...
    - Flexbox
    - CSS Grid

---

# Typy vlastností

  - ***seznamy a tabulky*** -- vlastnosti pro speciální elementy
    - `list-style-type`, `list-style-image`, `border-collapse`, `caption-side`, ...
  - ***transformace, přechody a animace*** -- umožňují pohyb, efekty a interaktivitu.
    - `transform`, `transition`, `animation`, ...
  - ***filtry a efekty***
    - `filter`, `backdrop-filter`, `mask`, ...
  - ***interaktivita a kurzor***
    - `cursor`, `pointer-events`, `user-select`, ...
  - ***obsah a generované prvky*** -- přidávají nebo mění obsah vygenerovaný CSS.
    - `content`, `quotes`, `counter-reset`, `counter-increment`, ...

---

# Vlastnosti písma

- **styl písma -- *`font-style`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="font-style: normal">normal</span>
<span style="font-style: italic">italic</span>
<span style="font-style: oblique">oblique</span>

</pre>

- **váha písma -- *`font-weight`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="font-weight: normal">normal</span>
<span style="font-weight: lighter">lighter</span>
<span style="font-weight: bold">bold</span>
<span style="font-weight: bolder">bolder</span>
<span style="font-weight: 100">100</span>
<span style="font-weight: 900">900</span>

</pre>

- **varianta písma -- *`font-variant`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="font-variant: normal">normal</span>
<span style="font-variant: small-caps">small-caps</span>

</pre>

---

# Velikost písma

- ***`font-size`***

<pre class="code-render" default-style="
html {
  font-size: 16px;
}

body {
  transform: scale(2);
  transform-origin: 0 0;
  width: 49%;
}
" resizable="true" style="height: 300px;">

<span style="font-size: 16px">16px</span>
<span style="font-size: 32px">32px</span>
<span style="font-size: 1rem">1rem</span>
<span style="font-size: 2rem">2rem</span>
<span style="font-size: 100%">100%</span>
<span style="font-size: 200%">200%</span>
<br>
<br>
<span style="font-size: small">small</span>
<span style="font-size: x-small">x-small</span>
<span style="font-size: xx-small">xx-small</span>
<span style="font-size: medium">medium</span>
<span style="font-size: large">large</span>
<span style="font-size: x-large">x-large</span>
<span style="font-size: xx-large">xx-large</span>

</pre>

```css
html {
  /* nastavení velikosti 1rem */
  font-size: 16px;
}
```

---

# Druh písma

- ***`font-family`***

- generické druhy písem:

<pre class="code-render" default-style="
html {
  font-size: 32px;
}

body {
  transform: scale(2);
  transform-origin: 0 0;
  width: 49%;
}
" resizable="true" style="height: 130px;">

<span style="font-family: serif">serif</span>
<span style="font-family: sans-serif">sans-serif</span>
<span style="font-family: monotype">monotype</span>

</pre>

- nainstalovaná písma:

<pre class="code-render" default-style="
html {
  font-size: 32px;
}

body {
  transform: scale(2);
  transform-origin: 0 0;
  width: 49%;
}
" resizable="true" style="height: 300px; float: right; width: 35%; z-index: 1;">

<span style="font-family: Verdana Arial">Verdana</span><br>
<span style="font-family: 'Times New Roman'">Times New Roman</span>

</pre>

```css
span.verdana {
  font-family: Verdana, Arial, sans-serif;
}

span.times {
  font-family: "Times New Roman", sans-serif;
}
```

- je nutné vždy specifikovat ***alternativy*** (*poslední musí být generická*)
- pokud název obsahuje mezery, musí být v úvozovkách

---

# Externí fonty

- [Google Fonts](https://fonts.google.com/share?selection.family=Ubuntu)

- import CSS obsahující definici fontu v HTML:

```html
<head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Ubuntu:ital,
    wght@0,300;0,400;0,500;0,700;1,300;1,400;1,500;1,700&display=swap" rel="stylesheet">
</head>

```

- použití fontu v CSS:

<pre class="code-render" default-style="
html {
  font-size: 64px;
}

body {
}
" resizable="true" style="height: 150px; float: right; width: 35%; z-index: 1;">

<span style="font-family: 'Ubuntu'">Ubuntu</span>

</pre>


```css
span.ubuntu {
  font-family: "Ubuntu", sans-serif;
  /* dle podpory fontu */
  font-weight: 400;
  font-style: normal;
}
```

---

# Vlastní font

- pravidlo ***@font-face*** umožňuje načíst vlastní font (např. z .woff2 nebo .ttf souboru) a používat ho v dokumentu

```css
@font-face { 
  font-family: 'NovyFont';
  src: url('newFontFile.woff') format('woff'),
       url('newFontFile.ttf') format('truetype'),
       url('newFontFile.svg') format('svg'); 
  font-weight: bold; 
  font-style: italic;
  font-stretch: normal; /* řez písma */
}


h1 {
  font-family: 'NovyFont', sans-serif;
  font-weight: bold;
  font-style: italic;
} 
```

---

# Vlastnosti textu

- **dekorace textu -- *`text-decoration`*** (`-style`, `-color`, `-thickness`)

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="text-decoration: none">none</span>
<span style="text-decoration: overline 2px">overline</span>
<span style="text-decoration: underline 2px">underline</span>
<span style="text-decoration: line-through 2px">line-through</span>
<span style="text-decoration: underline red 6px">underline red 6px</span>

</pre>

- **transformace textu -- *`text-transform`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="text-transform: none">none</span>
<span style="text-transform: capitalize">capitalize</span>
<span style="text-transform: uppercase">uppercase</span>
<span style="text-transform: lowercase">lowercase</span>

</pre>

- **mezera mezi písmeny -- *`letter-spacing`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="letter-spacing: normal">normal</span>&nbsp;&nbsp;&nbsp;&nbsp;
<span style="letter-spacing: .5rem">.5rem</span>

</pre>

- **mezera mezi slovy -- *`word-spacing`***

<pre class="code-render" default-style="" resizable="true" style="height: 100px;">

<span style="word-spacing: normal">normal word spacing</span>&nbsp;&nbsp;&nbsp;&nbsp;
<span style="word-spacing: .5rem">.5rem word spacing</span>

</pre>

---

# Zarovnání textu


- **horizontální zarovnání -- *`text-align`***
  - aplikuje se na blokový element, který obsahuje text (např. `<p>`)

<pre class="code-render" default-style="" resizable="true" style="height: 250px;">

<div style="text-align: left">left</div>
<div style="text-align: center">center</div>
<div style="text-align: right">right</div>
<div style="text-align: justify">justify</div>

</pre>

- **vertikální zarovnání -- *`vertical-align`***

<pre class="code-render" default-style="" resizable="true" style="height: 120px;">

<span style="vertical-align: baseline">baseline</span>
<span style="vertical-align: sub">sub</span>
<span style="vertical-align: super">super</span>
<span style="vertical-align: top">top</span>
<span style="vertical-align: bottom">bottom</span>
<span style="vertical-align: 30%">30%</span>

</pre>

---

# Mezery

<pre class="code-render" default-style="
p {
  text-align: justify;
  line-height: 1.8;       /* výška řádku */
  text-indent: 50px;      /* odsazení prvního řádku */
  overflow-wrap: break-word; /* zalomení dlouhých slov */
  word-break: break-word; /* láme při nutnosti */
  hyphens: auto;          /* dělení slov pomlčkami */
}" resizable="true" style="height: 800px; width: 30%; float: right; z-index: 1; margin-left: 1rem">

<p>
  Tento odstavec ukazuje, jak CSS vlastnosti pro rozvržení řádků fungují.
  Všimni si větší výšky řádků, odsazeného prvního řádku i toho, že dlouhá
  slova se v případě potřeby zalamují a mohou se rozdělit pomlčkou na konci.
  SlovoSuperExtraMegaUltraDlouhéSlovoBezMezer by jinak přetékalo ven z boxu.
</p>

</pre>

```css
p {
  text-align: justify;
  line-height: 2;       /* výška řádku */
  text-indent: 50px;      /* odsazení prvního řádku */
  overflow-wrap: break-word; /* zalomení dlouhých slov */
  word-break: break-word; /* láme při nutnosti */
  hyphens: auto;          /* dělení slov pomlčkami */
}
```

---

# Barva textu

---

# Pozadí

---

# Rámečky

---

# Zobrazení
