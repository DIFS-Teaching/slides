# Sémantický web

- Představa *webu dat* (*web of data* oproti *web of documents*)
	- Publikování strojově srozumitelných dat
- Základní prvky vize z roku 2001:
	- Reprezentace znalostí -- Resource Description Framework (RDF)
	- Sdílená konceptualizace (``model světa'') -- ontologie
	- Agenti -- producenti a konzumenti služeb

<p class="cite">Berners-Lee, Tim, Hendler, James, et al. &ldquo;The Semantic Web : a new form of Web content that is meaningful to computers will unleash a revolution of new possibilities&rdquo; <em><span class="journal">Scientific American</span></em> 284 (2001) : 34-43</p>

Note:
Zdůraznit, že je to vize stará čtvrt století. Na dalším slajdu se podíváme,
co z ní skutečně vzniklo. Ten článek si dnes ještě vytáhneme SPARQL dotazem
-- je to Q29164671.

---

# 25 let poté

- ??**Nepřišlo:** autonomní agenti vyjednávající mezi sebou, důkazy, vrstva důvěry
- ??**Přišlo:** RDF, SPARQL, JSON-LD, schema.org
- ??**Přežilo pod jiným jménem:** *znalostní graf* (Google 2012, dnes každý větší podnik)

<div class="small">

| Anotace na webu | 2015 | 2024 |
|---|---|---|
| Průměrný počet trojic na stránku | 10 | **57** |

</div>

- Z webů, které vůbec něco anotují: JSON-LD ≈ 70 %, Microdata ≈ 46 %, RDFa ≈ 3 %

<p class="cite" style="font-size: 85%">Web Data Commons: Microdata, RDFa, JSON-LD and Microformat data sets, vydání leden 2025 (extrakce z Common Crawl 10/2024). <a href="https://webdatacommons.org/structureddata/">webdatacommons.org/structureddata</a></p>

Note:
Poctivá odpověď na otázku ``stalo se to, nebo ne''. Vize v původní podobě
neuspěla, ale datový model a dotazovací jazyk se nasadily široce -- a nejvíc
právě tam, kde na tom někdo vydělá (e-shopy a Google).

---

# Web dokumentů vs. web dat

<div class="col small">

**World Wide Web**

- Základní jednotkou je dokument
- Odkaz vede z dokumentu na dokument
- Význam obsahu je v textu, pro člověka
- Technologie: HTTP, URI, HTML

</div>
<div class="col small">

**Sémantický web**

- Základní jednotkou je **tvrzení o zdroji**
- Odkaz vede z věci na věc
- Význam je zapsaný explicitně, pro stroj
- Technologie: HTTP, IRI, RDF, ontologie

</div>

@@div style="clear:both"@@@@/div@@


<p class="fragment" style="font-size: 130%; text-align: center; margin-top: 0.5em;">Stejná infrastruktura, jiná jednotka obsahu.</p>

---

# Z čeho se to skládá

<!-- .slide: class="normal centered fullspace" -->
![Zásobník technologií](assets/stack.svg) <!-- .element: style="height:700px;margin:0;" -->

Note:
Původní ``layer cake'' z prvních let W3C měl nahoře ještě Unifying Logic,
Proof a Trust. Ty vrstvy nikdy nedostaly standard ani nasazení -- proto jsou
tady čárkovaně stranou. Zbytek zásobníku je dnes běžná praxe.

---

# Stav standardů (2026)

<div class="small">

| Standard | Stav |
|---|---|
| RDF 1.1 | W3C Recommendation 2014 -- **tohle běží v praxi** |
| RDF 1.2 Concepts | Candidate Recommendation (duben 2026), *triple terms* |
| Turtle, N-Triples, TriG | W3C Recommendation 2014 |
| JSON-LD 1.1 | W3C Recommendation 2020 |
| SPARQL 1.1 | W3C Recommendation 2013 -- **tohle se učíme** |
| SPARQL 1.2 | zatím jen Working Draft |
| SHACL 1.0 | W3C Recommendation 2017 |

</div>

<p class="fragment">Standardy se tu hýbou v desetiletích, ne ve verzích za rok.</p>

Note:
Jedna z mála oblastí, kde se vyplatí učit dvanáct let starý standard --
protože je pořád ten platný a implementovaný všude. To samo o sobě něco
říká o zralosti té technologie.
