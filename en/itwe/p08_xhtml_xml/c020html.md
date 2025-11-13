# Multimedia `<audio>`

  - The `controls` attribute displays the controls (play, stop, pause)
  - JavaScript API for controlling the playback

```html
<audio controls="">
   <source src="sound.ogg" type="audio/ogg"/>
   <source src="sound.mp3" type="audio/mpeg"/>
   Audio is not supported.
</audio>
``` 

  - Different supported formats and codecs (MP3, WAW, OGG, ...)
  - Browser-dependent 

---

# Multimedia `<video>`

```html
<video controls="" height="240" width="320">
   <source src="file.mp4" type="video/mp4"/>
   <source src="file.ogg" type="video/ogg"/>
   Video is not supported.
 </video>
``` 

  - Different supported formats and codecs (MP4, WebM, OGG, ...)
  - Browser-dependent 

---

# Graphics

  - SVG a MathML included directly in the document 

```html
<svg ="" height="120" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" fill="red" r="50"></circle>
  <rect ="" height="60" style="stroke:none; fill:#00ff00;        fill-opacity: 0.5;" width="60" x="80" y="20"></rect>
</svg>
``` 
  - Drawing canvas `<canvas>`
    - Drawing using a JavaScript API

---

# Inline frame

```html
<iframe height="100" src="frames_c5.html" width="150">
Inline frames are not supported.
</iframe>
```

---

# Link relations

  - Adds _semantics_ to links -- the purpose of the link
  - Applicable to the _link_ , _a_ and _area_ elements
  - Two kinkds of links: 
    - a link to an external resource – adding related contents to a document

```html
<link href="style.css" rel="stylesheet" type="text/css"/>
``` 
    - hyperlink – navigation to another document 
    
```html
<a href="slide010.html" rel="next">next</a>
```

---

# Link relations (II)

  - Some interesting _rel_ values: 
    - **author**
    - **alternate** \-- alternative version (RSS, mobile, etc.)
    - **external** \-- external resources
    - **licence** \-- content license
    - **tag** \-- tag page (e.g. blogs)
    - **search** \-- search page
    - **first, last** \-- first, last document in a set
    - **prev, next** \-- previous, next document in a set
    - **up, down** \-- hierarchical navigation

---

# Page icon

  - Displayed in the URL field, in bookmarks, ...
  - A file in ICO format stored on server
  - Specification in document header:
  
```html
<link ="" href="http://my.web.com/favicon.ico" rel="shortcut icon" type="image/x-icon"/>
``` 

  - Most browsers automaticaly look for a file **favicon.ico** in the server root directory even without this specification
  - Some browsers support other image formats (PNG, GIF) but this has certain drawbacks

---

# RSS and ATOM export

  - XML languages for content syndication
  - Allows to subscribe to new content via a client software

```html

<link ="" href="/feeds" rel="alternate" title="Feed of recent questions" type="application/atom+xml"/>

<link ="" href="http://my-web.com/rss/index.php" rel="alternate" title="Top News" type="application/rss+xml"/>

```

---

# Microdata

  - A possible way of adding semantics to the elements
  - For futher automated processing
  - Attributes: 
    - **itemscope** – item set container
    - **itemprop** – a property
    - **itemtype** – element type denoted as URL
    - **itemid** – a global identifier (e.g. ISBN for books)
    - **itemref** – global identifier reference

---

# Microdata (II)

  - Example
  
```html
<div itemscope="" itemtype="http://example.org/person">
 <p>My name is <span itemprop="name">John</span>.</p>
 <p>My surname is <span itemprop="surname">Smith</span>.</p>
 <p>I was born in <span itemprop="born-city">Brně</span>.</p>
</div>
```

---

# Additional information in header

  - Meta information -- additional information about the document
  - Always in the document header
  - Two possible variants: 
    - User information ```html

<meta content="..." name="..."/>

```

    - HTTP header equivalent
    
```html
<meta content="..." http-equiv="..."/>
```

---

# User information

  - Document description 

```html
<meta content="Short description" name="description"/>
```
  - Keywords 
  
```html
<meta content="WWW, HTML, pages, design" name="keywords"/>
```

  - Document author 
  
```html
<meta content="John Smith, john@smith.org" name="author"/>
```

---

# User information (II)

  - Generator (software)
  
```html

<meta content="Mozilla Composer" name="generator"/>

```
  - Information for indexing robots
  
```html

<meta content="index,follow" name="robots"/>
<meta content="noindex,nofollow" name="robots"/>

```

---

# Custom meta tags

  - The _name_ a _content_ may contain any user information
  - Suitable for adding information for different applications
  - E.g. specific browser settings (tablets, mobile phones) 
  
```html

<meta content="width=device-width" name="viewport"/>
<meta content="user-scalable=no, initial-scale=1" name="viewport"/>

```

---

# Facebook meta tags

  - Tags for the Facebook Open Graph Protocol
  - Allows to specify metadata for page sharing 
  
```html

<meta content="Page Title" property="og:title"/>
<meta content="Page description" property="og:description"/>
<meta content="my-website.com" property="og:site_name"/>
<meta content="http://my-website.com/info/" property="og:url"/>
<meta ="" content="http://my-website.com/thumbnail.jpg" property="og:image"/>
<meta content="article" property="og:type"/>

```

---

# HTTP equivalents

  - The same iformation as in HTTP headers
  - No access to the server configuration needed
  - Content type = MIME type + encoding ```html

<meta ="" content="text/html; charset=utf-8" http-equiv="content-type"/>

```
  - Content language ```html

<meta ="" content="en" http-equiv="content-language"/>

```

---

# Redirect

  - After displaying a page, another document is automaticaly displayed after the specified time
  - E.g. redirect to Google after 6 seconds ```html

<meta ="" content="6;URL=http://www.google.com/" http-equiv="refresh"/>

```

---

# Cache control

  - Controls whether to store or not to store the document in cache
  - Influences just the browser cache
  - E.g. ```html

<meta ="" content="cache" http-equiv="cache-control"/>

<meta ="" content="no-cache" http-equiv="cache-control"/>

```

---

# Expiration

  - Defines the date of the document expiration
  - After this date, it should be removed from cache
  - E.g. ```html

<meta ="" content="Wed 14 Nov 2005 16:10:00" http-equiv="expires"/>

```
