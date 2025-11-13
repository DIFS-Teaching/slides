
---

# XML and XHTML

---

# XML and XHTML

  - XML 
    - A general standard for data and document exchange
    - Syntactically similar to HTML, does not define the meaining of the tags (it depends on the particular application)
  - XHTML 
    - The application of XML for web pages
    - Tag names and their meaning equal to HTML, syntax is XML

---

# Advantages of XML

  - Simple implementation 
    - The language is not so complex
    - Quite easy to process
  - It is possible to store, index and search in documents 
    - Native XML databases
  - Many tools for XML processing 
    - Document parsing (DOM, SAX parsers)
    - Transformations (XSLT)
    - ...
  - Many applications already use XML

---

# HTML and XHTML

  - Common features 
    - The same meaning of most the tags and attributes
    - Tags and attributes are written the same way
  - Differences 
    - Strict syntax
    - Formatting tags and attributes removed, replaced by CSS
    - It has to respect the XML rules

---

# Header

  - Each XML document should start with a header ```html
@HTML@
<?xml version="1.0" encoding="windows-1250"?>
@/HTML@
``` 
  - If no encoding is specified, UTF-8 (Unicode) is used

---

# Document type (DTD)

  - Transitional ```html
@HTML@
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0@@ Transitional//EN"@@ "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

@/HTML@
``` 
  - Strict ```html
@HTML@
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0@@ Strict//EN"@@ "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
 
@/HTML@
```

---

# Root element `<html>`

  - The root element `<html>` should have the attributes `xmlns` and `xml:lang`: ```html
@HTML@
<html @@="" lang="en" xml:lang="en" xmlns="http://www.w3.org/1999/xhtml">
@/HTML@
</html>
``` 
  - It should contain the `<head>` and `<body>` elements
  - The `<head>` element should contain title `<title>`

---

# Writing tags

  - All the tag names must be entered in **lowercase**
  - All non-empty tags must have an end tag
  - The tags empty **from definition** (`<br>`) must have an end tag too `<br></br>` or they can be written as `<br/>`
  - E.g. 
    - `<img src="..." alt="..." />`
    - `<input type="..." name="..." />`
but 
    - `<script type="text/javascript"></script>`

---

# Tag nesting

  - All tags must be properly nested
  - Overlapping is not allowed in HTML neither but the end tags may be optional
  - XML strictly requires a _well-formed document_
  - Element overlapping ```html
@HTML@
<p>This is word is <em>highlighted.</em></p>
@/HTML@
``` 
  - Well-formed document: ```html
@HTML@
<p>This word is <em>highlighted.</em></p>
@/HTML@
```

---

# Attributes

  - The attribute values **must** be quoted
  - Each attribute should have a value 
    - HTML:  
` @HTML@ ... @/HTML@ `
    - XHTML:  
` @HTML@ ... @/HTML@ `
  - The attribute values that are an enumeration must be written in lowercase 
    - ` @HTML@  @/HTML@ `
    - ` @HTML@  @/HTML@ `
  - All the **&** characters in attribute values must be written using `&amp;`

---

# Scripts and styles

  - Scripts that contain & and < must be marked as CDATA: ```html
@HTML@
<script type="text/javascript">@@
   @/<![CDATA[@@     ... script text ...@@     ]]>/@ @@
</script>@@
@/HTML@
```

---

# XHTML 1.1

  - The XHTML 1.0 has been split to _modules_
    - Basic modules (XHTML Basic), forms, tables, ...
    - Allows creating an appropriate language for an application - a **build**
  - XHTML 1.1 is a build designed to correspond to XHTML 1.0 Strict
  - Changes to XHTML 1.0 Strict 
    - The `lang` attribute is removed (`xml:lang` remains)
    - For elements `<a>` and `<map>` the `name` attribute has been replaced with `id`

---

# XHTML 1.1 Document

  - Document skeleton:

```html
@HTML@
<?xml version="1.0" encoding="UTF-8"?>@@
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"@@    "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
@@
<html xml:lang="en" xmlns="http://www.w3.org/1999/xhtml">@@
  <head>@@
    <title>...</title>@@
  </head>@@
  <body>@@
    ...@@
  </body>@@
</html>@@
@/HTML@
```

---

# XHTML and the Transfer Protocol

  - XHTML should be processed by a XML parser in the browser 
    - Which is different from the default HTML parser
  - This must be indicated by the MIME type during the HTTP transfer 
    - Type `text/html` for HTML documents
    - Type `application/xhtml+xml` for XHTML documents
  - Practical issues 
    - A server side configuration necessary
    - MSIE does not accept `application/xhtml+xml` (it tries to save to disk)
  - Currently acceptable solution 
    - XHTML dokument + `text/html` MIME typ

---

# Consequences of the Solution

  - The browser processes an XML document with the HTML parser 
    - XHTML 1.0 specification [allows this](http://www.w3.org/TR/2009/NOTE-xhtml-media-types-20090116/#text-html)
    - It recommends [additional syntactic limitations](http://www.w3.org/TR/2009/NOTE-xhtml-media-types-20090116/#compatGuidelines) in order not to confuse the browser
  - HTML parser is fault-tolerant 
    - The document is processed as a „tag soup”
    - But it cannot process advanced XML features 
      - Namespaces, custom entities, ...
    - [Examples](http://www.fit.vutbr.cz/~burgetr/itw/)
  - XML prolog `<?xml version="1.0" encodign="utf-8"?>`
    - May confuse older browsers (MSIE 6)
    - May be omited for UTF-8 documents

---

# Future of XHTML

  - XHTML 1.1 the last stable version
  - Successor versions have been started 
    - XHTML 1.2 (evolution)
    - XHTML 2 (revolution)
  - Problems of XHTML 2 
    - Modernized with focus on semantics
    - Not backward compatible
    - Too long to finish
    - Negative feedback from browser developers and web designers

---

# (X)HTML 5

  - A W3C-independent initiative in reaction to the XHTML2 problems 
    - Alternative group [WHATWG](http://www.whatwg.org/ "Web Hypertext Application Technology Working Group")
    - Accepted by W3C by 2007
  - Based on HTML 4, many new features 
    - Semantic tags, audio, video and more
  - Defines the meaning of tags and attributes in a **syntax-independent** way
  - The syntax may be chosen 
    - HTML serialization
    - XML serialization (sometimes called XHTML 5)

---

# HTML5 Syntax

  - HTML syntax 
    - MIME type `text/html`
    - Parsing rules are defined including error handling
  - XHTML syntax 
    - MIME type `application/xhtml+xml` or `application/xml`
    - Parsed by a standard XML parser

---

# Doctype

  - New generic document type `html` ```html
@HTML@
<!DOCTYPE html>

@/HTML@
``` (for activating the browser standards mode) 
  - XHTML with no DOCTYPE but with a namespace definition ```html
@HTML@
<?xml version="1.0" encoding="UTF-8"?>@@
<html xmlns="http://www.w3.org/1999/xhtml">@@
...@@
</html>
@/HTML@
```

---

# General XML

  - The browsers allows general XML processing (which is not XHTML)
  - No built-in style is defined 
    - But it is possible to define the author style sheet
    - The `xml-stylesheet` directive
  - Style definition 
    - **CSS**
      - Style for the individual elements
    - **XSLT**
      - Internal transformation to an HTML document
      - May include JavaScript etc.
  - [Examples](http://www.fit.vutbr.cz/~burgetr/itw/)

---

# Links

  - HTML 4 and 5 differences (official)  
<http://dev.w3.org/html5/html4-differences/>
  - Browser test for HTML 5 + current charts <http://html5test.com/>
  - Feature compatibility  
<http://html5please.com/#html>
  - Element meaning explanation <http://html5doctor.com/element-index/>
  - [](http://caniuse.com)http://caniuse.com/ -- compatibility test

---

To be continued...