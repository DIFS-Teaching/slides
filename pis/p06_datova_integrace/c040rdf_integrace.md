<!-- .slide: class="section" -->

<header>
	<h1>RDF jako základ integrace</h1>
	<p>Jednotný datový model, knowledge grafy a propojená data</p>
</header>

---

# RDF jako integrační model
- RDF trojice (subjekt – predikát – objekt) jsou **nejmenší jednotka dat**
- Každý zdroj, každá vlastnost má **globální URI** → žádné kolize názvů
- RDF grafy z různých zdrojů lze **přímo sloučit** (merge)
	- Trojice ze zdroje A a zdroje B tvoří společný graf
	- Sdílené URI jsou automaticky propojeny
- Technická integrace = sjednocení grafů

---

# Sloučení RDF grafů – příklad

Graf ze zdroje A (CRM):
```turtle
<http://myfirm.cz/customer/42>
    foaf:name "Jan Novák" ;
    foaf:mbox <mailto:jan@novak.cz> .
```

Graf ze zdroje B (objednávkový systém):
```turtle
<http://myfirm.cz/customer/42>
    ex:hasOrder <http://orders.myfirm.cz/order/99> .

<http://orders.myfirm.cz/order/99>
    ex:totalPrice "1500"^^xsd:decimal .
```

Po sloučení: jeden graf propojující zákazníka i s jeho objednávkami <!-- .element: class="cite" -->

---

# Identita přes `owl:sameAs`
- Různé zdroje mohou mít různé URI pro totéž
- `owl:sameAs` deklaruje, že dvě URI označují **totéž individuum**

```turtle
<http://crm.myfirm.cz/person/42>
    owl:sameAs <http://erp.myfirm.cz/employee/E007> .
```

- RDF reasoner pak zachází s oběma URI jako s jedním objektem
- Propojení může být i na externí knowledge base:

```turtle
<http://myfirm.cz/city/Brno>
    owl:sameAs <http://dbpedia.org/resource/Brno> .
```

---

# Knowledge Graph
- Rozsáhlý RDF graf reprezentující znalosti o určité doméně nebo organizaci
- Obsahuje **entity**, jejich **vlastnosti** a **vztahy** mezi nimi
- Podložen ontologií (schéma grafu)
- Příklady:
	- **Google Knowledge Graph** – fakta o světě
	- **Wikidata** – strukturovaná data z Wikipedie
	- **Enterprise Knowledge Graph** – interní podniková data

---

# Enterprise Knowledge Graph
- Firemní knowledge graph integruje data z mnoha interních systémů
- Entity: zákazníci, produkty, zaměstnanci, projekty, dodavatelé, …
- Vztahy: koupil, pracuje na, dodává, vlastní, …
- Přínosy:
	- Jednotný pohled na firemní data
	- Dotazování přes hranice systémů
	- Základ pro AI aplikace (doporučování, predikce, chatboty)
- Adoptoři: Google, Amazon, LinkedIn, Airbnb, eBay

---

# Mapování relačních dat do RDF

- Standard **R2RML** (W3C) – deklarativní mapování SQL tabulek na RDF trojice
- **Direct Mapping** – automatické mapování bez konfigurace

```turtle
# R2RML příklad
<#CustomerMapping>
    rr:logicalTable [ rr:tableName "CUSTOMER" ] ;
    rr:subjectMap [
        rr:template "http://myfirm.cz/customer/{ID}" ;
        rr:class foaf:Person
    ] ;
    rr:predicateObjectMap [
        rr:predicate foaf:name ;
        rr:objectMap [ rr:column "FULL_NAME" ]
    ] .
```

---

# Nástroje pro R2RML mapování

- **Ontop** – virtuální RDF vrstva nad SQL databází
	- Přepisuje SPARQL dotazy na SQL
	- Data zůstávají v DB, RDF je virtuální
- **D2RQ** – přístup k relační DB jako k RDF grafu
- **RMLMapper** – RML (rozšíření R2RML i pro JSON, CSV, XML)
- **Apache Jena** – Java knihovna pro práci s RDF a mapováním

---

# Mapování JSON a XML dat do RDF

- **RML** (RDF Mapping Language) – rozšíření R2RML
	- Podporuje JSON, CSV, XML, relační DB
- JSON-LD context – přidání sémantiky k existujícím JSON datům

```json
{
  "@context": {
    "name": "http://xmlns.com/foaf/0.1/name",
    "email": "http://xmlns.com/foaf/0.1/mbox"
  },
  "name": "Jan Novák",
  "email": "mailto:jan@novak.cz"
}
```

---

# RDF Triple Store jako integrační hub
- Centrální úložiště RDF trojic ze všech zdrojů
- Zdrojová data jsou **transformována na RDF** (ETL do triple store)
- Výhody:
	- Jednotný přístupový bod (SPARQL endpoint)
	- Schéma definováno ontologií
	- Snadné přidání nového zdroje (stačí nové mapování)
- Příklady nástrojů: **Apache Jena/Fuseki**, **Virtuoso**, **Stardog**, **GraphDB**

---

# Architektura s RDF hubem

```
  Zdroj A (SQL) ─── R2RML Mapper ─┐
                                   │
  Zdroj B (JSON) ── RML Mapper ───▶│  Triple Store   ──▶  SPARQL
                                   │  (Fuseki, Stardog)     Endpoint
  Zdroj C (API) ─── RDF konvertor ─┘
                                         │
                              ontologie (OWL/RDFS)
```

---

# Inference (odvozování)
- Reasoner může z existujících trojic **odvodit nové** na základě ontologie
- Příklad: pokud `Student rdfs:subClassOf Person`, pak každý student je i Person
- Příklad: pokud `A owl:sameAs B`, pak vlastnosti A platí i pro B
- Přínosy pro integraci:
	- Automatické doplnění chybějících informací
	- Detekce nekonzistencí (inconsistency detection)
	- Klasifikace entit podle popisu vlastností

---

# Příklad odvozování při integraci

```turtle
# Ontologie
ex:Employee  rdfs:subClassOf  foaf:Person .
ex:hasManager  rdfs:domain  ex:Employee .

# Data ze zdroje A
ex:emp123  ex:hasManager  ex:emp456 .

# Odvozeno (reasonerem):
ex:emp123  rdf:type  ex:Employee .
ex:emp123  rdf:type  foaf:Person .   # díky subClassOf
```

---

# Provenance – původ dat
- Při integraci dat je důležité vědět **odkud data pochází**
- Standard **PROV-O** (W3C) pro zachycení provenance v RDF
- Pojmy: `prov:Entity`, `prov:Activity`, `prov:Agent`, `prov:wasDerivedFrom`

```turtle
ex:report2024
    prov:wasDerivedFrom ex:salesData ;
    prov:wasGeneratedBy ex:etlProcess ;
    prov:generatedAtTime "2024-03-01T08:00:00"^^xsd:dateTime .
```

- Umožňuje audit, reprodukovatelnost, trasování chyb
