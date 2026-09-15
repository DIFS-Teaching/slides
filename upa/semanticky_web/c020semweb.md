<!-- .slide: class="section" -->

<header>
	<h1>Datový model – RDF</h1>
	<p>Reprezentace a výměna faktů v rámci sémantického webu</p>
</header>

---

# Cíle a prostředky

- Cíle
	- Reprezentace strukturovaných dat **a jejich významu**
	- Možnost sdílet data i sémantiku napříč aplikacemi
- Běžná reprezentace dat v IS:
	- Relační/objektové/NoSQL databáze -- vázané na aplikaci
	- Veřejné API + serializace (JSON, XML) -- není definována sémantika

---

# Serializace -- příklad

```xml
<polozka>
	<velikost>3+1</velikost>
	<lokalita>Brno-střed</lokalita>
	<cena mena="czk">8 450 000</cena>
</polozka>
<polozka>
	<velikost>2+1</velikost>
	<lokalita>Kuřim</lokalita>
	<cena mena="czk">5 200 000</cena>
</polozka>
```

Strojově čitelné. Ale co přesně znamená `velikost`?

---

# Problémy

- Význam elementů je specifický pro danou aplikaci
	- Je definován v programovém kódu, který data generuje nebo čte
	- Obdobně jako sloupce v relační databázi
- Jiná aplikace přiřadí týmž značkám jiný význam:

<div class="small">

| Zdroj A | Zdroj B | Zdroj C |
|---|---|---|
| `<velikost>3+1</velikost>` | `<velikost>75</velikost>` | `<velikost>75 m2</velikost>` |
| dispozice | plocha v m², číslo | plocha i s jednotkou |

</div>

- ??Data jsou strojově **čitelná** (*machine readable*), ale ne **srozumitelná** (*machine understandable*)
- ??Tohle je doslova schema matching a normalizace jednotek z přednášky 4

---

# Reprezentace sémantiky

- Odlišení značek v různých aplikacích
	- Např. XML namespaces
	- Řeší kolize značek -- syntaktický problém
- Oddělená definice významu značek
	- Např. doprovodný dokument vysvětlující význam a případy použití
	- Čte ho ale člověk, ne program
- Navíc potřebujeme definovat **sémantické vztahy**
	- Byt je věc, která má umístění, velikost a cenu
	- Pokud možno formálně ⇒ **ontologie**

---

# Reprezentace faktů: RDF

- RDF: Resource Description Framework
	- Reprezentuje elementární *tvrzení* (fakta)
- Základním prvkem je **RDF trojice**: **subjekt** -- **predikát** -- **objekt**
- Grafová struktura
	- Tvrzení jsou propojena přes IRI, tvoří orientovaný graf
- Serializace pro uložení a přenos
	- Turtle, JSON-LD, N-Triples, RDF/XML...

<p class="fragment" style="font-size: 130%; text-align: center; margin-top: 0.5em;">Jeden datový model, více zápisů &ndash; jako relace vs. CSV/SQL dump.</p>

---

# RDF trojice -- tvrzení (statement)

![RDF trojice](assets/triple.svg) <!-- .element: style="height:420px;margin:0 auto;display:block" -->

- Subjekt a predikát jsou vždy **IRI**
- Objekt je **IRI** nebo **literál** (jen objekt může být literál)

Note:
Pozor na směr čtení: subjekt je to, o čem mluvím. ``Článek má autora Nováka.''
Predikát se čte od subjektu k objektu, ne naopak.

---

# Kde vzít IRI?

- Vlastní data -- vlastní IRI
	- Např. `https://www.fit.vut.cz/student/938272`
	- Obvykle společný *prefix*
- Existující data -- veřejné znalostní báze
	- `https://dbpedia.org/resource/Berlin`, `http://www.wikidata.org/entity/Q42`
- Strukturované slovníky -- ontologie
	- IRI pro predikáty a pro typy (třídy) objektů
- Zabudované: `rdf:type`

**Pravidla Linked Data:** používej IRI · používej *HTTP* IRI, aby se daly dereferencovat · po dereferencování vrať užitečná data · odkazuj na cizí IRI

Note:
Ta čtyři pravidla jsou Berners-Leeho ``Linked Data principles'' z roku 2006.
Třetí je ten, na kterém se to nejčastěji láme: IRI existuje, ale nic se pod ním
nevrátí.

---

# RDF graf

![RDF graf](assets/rdf-graf.svg) <!-- .element: style="height:520px;margin:0 auto;display:block" -->

- Literál může nést **jazykovou značku** (`@cs`) nebo **datový typ** (`^^xsd:date`)

Note:
Jazyková značka a datový typ jsou v praxi to, co dělá rozdíl mezi použitelnými
a nepoužitelnými daty. Bez jazykové značky nevíte, ve kterém jazyce je název;
bez datového typu je datum jen řetězec a nejde podle něj řadit.

---

# Schéma -- ontologie

![RDF a schéma](assets/rdf-schema.svg) <!-- .element: style="height:520px;margin:0 auto;display:block" -->

- Propojení přes `rdf:type`; schéma je psané opět v RDF
- Data a schéma mohou, ale nemusí být v jednom grafu

---

# Serializace do Turtle

```turtle
@prefix doc: <https://dokumenty.cz/> .
@prefix dct: <http://purl.org/dc/terms/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

doc:clanek42  dct:title   "Propojená data"@cs ;
              dct:issued  "2026-03-01"^^xsd:date ;
              dct:creator doc:jan-novak .

doc:jan-novak  a  foaf:Person ;
               foaf:name "Jan Novák" .
```

- `a` je zkratka za `rdf:type`, `;` opakuje subjekt, `,` opakuje predikát
- Výchozí volba, když má zápis číst člověk

---

# Ostatní serializace

<div class="col small">

**N-Triples** -- jeden řádek = jedna trojice, bez prefixů. Pro dumpy a streamy.

```
<https://dokumenty.cz/clanek42>
  <http://purl.org/dc/terms/title>
  "Propojená data"@cs .
```

</div>
<div class="col small">

**JSON-LD** -- RDF zapsané jako obyčejný JSON. Nejrozšířenější na webu.

```json
{ "@context": "https://schema.org",
  "@type": "Article",
  "name": "Propojená data" }
```

</div>

@@div style="clear:both"@@@@/div@@


- **RDF/XML** -- původní zápis z roku 1999, `<rdf:Description rdf:about="...">`. Existuje, psát to nebudete.
- **TriG / N-Quads** -- totéž co Turtle / N-Triples plus pojmenované grafy (viz další slajd)

Turtle, N-Triples, TriG i JSON-LD jsou **W3C Recommendation** -- žádný z nich není ten ``pravý''.

---

# Pojmenované grafy

<div class="small">

- Trojice + identifikátor grafu = **kvadrupl** (*quad*)
- Serializace: TriG, N-Quads

```turtle
@prefix wd: <http://www.wikidata.org/entity/> .
@prefix ex: <https://upa.fit.vut.cz/def#> .

ex:import-wikidata-2026-03 {
	wd:Q14960 ex:pocetObyvatel 402739 .
}
```

- ??**Provenience** -- ze kterého zdroje ta trojice je
- ??**Verzování** -- který import ji přinesl a kdy
- ??**Oddělení dat a schématu** -- ontologie zvlášť, instance zvlášť

<p class="fragment">Bez toho nejde u integrovaných dat říct, komu vlastně nevěřit.</p>

</div>

Note:
Přesně ten problém, který ve čtvrté přednášce nastane: spojíte tři zdroje,
vyjde nesmysl a nevíte, ze kterého zdroje ten nesmysl přišel. Pojmenované
grafy jsou levná odpověď; formálně se to řeší slovníkem PROV-O.

---

# RDF jako databáze

- Repozitář (*triplestore*) -- úložiště RDF trojic, dotazování přes SPARQL
- Lokální úložiště:
	- [Apache Jena / Fuseki](https://jena.apache.org/), [RDF4J](https://rdf4j.org/) (dříve Sesame)
	- [Oxigraph](https://github.com/oxigraph/oxigraph), [GraphDB](https://graphdb.ontotext.com/), [Virtuoso](https://virtuoso.openlinksw.com/)
	- [QLever](https://qlever.dev/) -- zvládne bilion trojic na jednom stroji
	- Amazon Neptune, Stardog
- Globální *znalostní báze*:
	- [DBpedia](https://www.dbpedia.org/), [Wikidata](https://www.wikidata.org/)

Tohle je **grafová databáze**. Druhou rodinu (*property graphs*, Neo4j) potkáte v 9. přednášce.

---

# Veřejné znalostní báze

- **Wikidata** -- `http://www.wikidata.org/entity/Q42`
	- SPARQL: [query.wikidata.org](https://query.wikidata.org)
	- ⚠ 9. 5. 2025 **rozdělena na dva grafy**: hlavní a vědecké články
	  ([query-scholarly.wikidata.org](https://query-scholarly.wikidata.org)) -- nevešla se na jeden stroj
- **DBpedia** -- `https://dbpedia.org/resource/Berlin`
	- SPARQL: [dbpedia.org/sparql](https://dbpedia.org/sparql)
	- Strukturovaná data vytěžená z infoboxů Wikipedie
- **Mnoho dalších**, vzájemně propojených přes IRI
	- *Linked Open Data* -- [lod-cloud.net](https://lod-cloud.net/)

Note:
To rozdělení Wikidat je hezká historka: vědecké články byly přes polovinu všech
trojic. Partitioning z přednášky 7 dorazil o pět přednášek dřív.

---

# Otevřená data

- Serializované RDF jako prostředek pro publikování otevřených (propojených) dat
- **Česko:** [data.gov.cz](https://data.gov.cz/) -- Národní katalog otevřených dat
	- Má i [SPARQL endpoint](https://data.gov.cz/sparql) -- za chvíli se v něm budeme ptát
	- Slovník DCAT-AP-CZ, [otevřené formální normy](https://ofn.gov.cz/)
- **EU:** [data.europa.eu](https://data.europa.eu/) -- i zde [SPARQL endpoint](https://data.europa.eu/data/sparql)
- Možno importovat do lokálního úložiště a dotazovat se spolu s vlastními daty
