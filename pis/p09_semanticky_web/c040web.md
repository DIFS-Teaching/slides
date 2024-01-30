
# RDF a Webové stránky

Web of Documents vs. Web of Data

---

# Jednoduchá anotace dokumentu

<html xmlns:html=“…”>

<head>

<rdf:RDF

    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"

    xmlns:dc="http://purl.org/dc/elements/1.1/">

  <rdf:Description rdf:about="http://www.moje.cz/"

    dc:creator="Jan Novak"

    dc:title="Titulek dokumentu"

    dc:description="Popis"

    dc:date="1999-09-10"/>

</rdf:RDF>

</head>

---

# Anotace částí obsahu
- Současnost – mikroformáty – **není RDF** 
- Doplnění sémantiky kombinaci existujících značek a atributů
- Příklad: hCalendar



<ol class="schedule">

<li>**2006**

    <ol>

    <li class="vevent">

    <strong class="summary">**Fashion Expo**</strong> in 

    <span class="location">**Paris, France**</span>:

    <abbr class="dtstart" title="2006-10-20">
		**Oct 20**</abbr> to 

    <abbr class="dtend" title="2006-10-23">**22**</abbr>                              </li>

---

# Integrace RDF a HTML
- HTML 5 – Microdata 
- W3C standard – RDFa 
- JSON notace – JSON-LD
- Viz např.
https://schema.org/Person#examples
- 



---

# Jiný příklad – RDFa 

<p xmlns:dc="http://purl.org/dc/elements/1.1/"

   about="http://www.example.com/books/wikinomics">

  In his latest book

  <cite property="dc:title">Wikinomics</cite>,

  <span property="dc:creator">Don Tapscott</span>

  explains deep changes in technology,

  demographics and business.

  The book is due to be published in

  <span property="dc:date" content="2006-10-01">October 2006</span>.

</p>
