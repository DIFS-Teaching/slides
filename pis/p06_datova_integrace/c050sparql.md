<!-- .slide: class="section" -->

<header>
	<h1>SPARQL a federovaná integrace</h1>
	<p>Dotazování napříč heterogenními datovými zdroji</p>
</header>

---

# SPARQL jako integrační jazyk
- SPARQL umožňuje dotazovat **RDF data z různých zdrojů** v jednom dotazu
- Princip **graph pattern matching** – vzory trojic se porovnávají s grafem
- Klíčové vlastnosti pro integraci:
	- **OPTIONAL** – levé vnější spojení (chybějící data)
	- **UNION** – sloučení výsledků z různých grafů
	- **FILTER** – podmínky a transformace hodnot
	- **SERVICE** – federované dotazování na vzdálené endpointy

---

# Federated SPARQL – `SERVICE`
- Klauzule `SERVICE` umožňuje **dotazovat vzdálený SPARQL endpoint** v rámci jednoho dotazu
- Lokální a vzdálená data jsou automaticky spojena

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/>

SELECT ?person ?name ?birthPlace WHERE {
    # Lokální data
    ?person foaf:name ?name .
    ?person owl:sameAs ?dbpPerson .

    # Vzdálená DBpedia
    SERVICE <http://dbpedia.org/sparql> {
        ?dbpPerson dbo:birthPlace ?birthPlace .
    }
}
```

---

# Příklad: integrace firemních dat s veřejnými zdroji

```sparql
PREFIX ex: <http://myfirm.cz/ns#>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX schema: <https://schema.org/>

SELECT ?company ?name ?employees ?countryPopulation WHERE {
    # Interní data (lokální endpoint)
    ?company ex:companyName ?name ;
             ex:headQuarters ?city .
    ?city owl:sameAs ?dbpCity .

    # Veřejná data o zemi sídla (DBpedia)
    SERVICE <http://dbpedia.org/sparql> {
        ?dbpCity dbo:country ?country .
        ?country dbo:populationTotal ?countryPopulation .
    }
}
```

---

# Named Graphs pro správu zdrojů
- RDF dataset může obsahovat více **pojmenovaných grafů** (named graphs)
- Každý zdroj dat uložen do vlastního grafu
- Umožňuje dotazovat specifický zdroj nebo všechny najednou

```sparql
# Data pouze z CRM grafu
SELECT ?person ?name WHERE {
    GRAPH <http://myfirm.cz/graphs/crm> {
        ?person foaf:name ?name .
    }
}

# Data ze všech grafů
SELECT ?person ?name ?graph WHERE {
    GRAPH ?graph {
        ?person foaf:name ?name .
    }
}
```

---

# OPTIONAL – integrace neúplných dat

- Různé zdroje mají různé atributy pro totéž entity
- `OPTIONAL` vrátí data i tehdy, když část chybí

```sparql
SELECT ?person ?name ?phone ?email WHERE {
    ?person foaf:name ?name .
    OPTIONAL { ?person schema:telephone ?phone . }
    OPTIONAL { ?person foaf:mbox ?email . }
}
```

- Výsledek: osoby i s chybějícím telefonem nebo e-mailem

---

# UNION – integrace různých schémat

- Různé zdroje používají různé predikáty pro stejný koncept
- `UNION` sjednotí výsledky obou větví

```sparql
SELECT ?person ?name WHERE {
    { ?person foaf:name ?name . }
    UNION
    { ?person schema:name ?name . }
    UNION
    { ?person rdfs:label ?name . }
}
```

---

# CONSTRUCT – transformace a integrace

- Dotaz `CONSTRUCT` vytvoří **nový RDF graf** z výsledků
- Vhodné pro transformaci schématu nebo integraci dat

```sparql
CONSTRUCT {
    ?person foaf:name ?name ;
            foaf:mbox ?email .
}
WHERE {
    ?customer ex:customerName ?name ;
              ex:emailAddress ?email .
    BIND(IRI(CONCAT("http://persons.example.org/", STR(?customer))) AS ?person)
}
```

---

# SPARQL Update – zápis integrovaných dat

- SPARQL 1.1 Update umožňuje **vkládání a mazání trojic**
- Vhodné pro ETL pipeline transformující data do triple store

```sparql
INSERT {
    GRAPH <http://integrated/>  {
        ?person foaf:name ?name ;
                schema:email ?email .
    }
}
WHERE {
    GRAPH <http://source/crm/> {
        ?cust ex:name ?name ; ex:mail ?email .
        BIND(IRI(CONCAT("http://persons/", STR(?cust))) AS ?person)
    }
}
```

---

# Veřejné SPARQL endpointy pro integraci

| Zdroj | Endpoint |
|---|---|
| Wikidata | https://query.wikidata.org/sparql |
| DBpedia | https://dbpedia.org/sparql |
| EU data | https://data.europa.eu/sparql |
| Linked Geo Data | http://linkedgeodata.org/sparql |
| Bio2RDF | https://bio2rdf.org/sparql |

- Lze kombinovat v jednom federovaném SPARQL dotazu

---

# Výzvy federovaného SPARQL
- **Výkon**: vzdálené endpointy mohou být pomalé nebo nedostupné
- **Limity**: veřejné endpointy mají omezení délky dotazu a počtu výsledků
- **Bezpečnost**: federovaný dotaz může prozradit lokální data
- **Optimalizace**: pořadí vzorů a `SERVICE` klauzulí ovlivňuje výkon
- Doporučení: nejdříve redukovat lokální data, pak volat vzdálené

---

# Alternativa: SPARQL Anything

- Nástroj pro **dotazování non-RDF formátů** pomocí SPARQL
- Podporuje JSON, CSV, XML, HTML, soubory, REST API
- Data se virtuálně zobrazí jako RDF `xyz:` namespace

```sparql
PREFIX xyz: <http://sparql.xyz/facade-x/data/>
PREFIX fx:  <http://sparql.xyz/facade-x/ns/>

SELECT * WHERE {
    SERVICE <x-sparql-anything:https://api.example.com/users> {
        ?user xyz:name ?name ; xyz:email ?email .
    }
}
```

---

# Praktický příklad: integrace otevřených dat

- Zdroj: [data.europa.eu](https://data.europa.eu) – RDF datasety EU
- Stáhneme dataset o firmách (Turtle/RDF/XML)
- Importujeme do lokálního triple store (Apache Fuseki)
- Propojíme s interními daty pomocí `owl:sameAs` (IČO, název)
- Výsledek: dotazování kombinující interní a veřejná data v SPARQL

```bash
# Spuštění Fuseki
java -jar fuseki-server.jar --update --mem /ds

# Import datasetu
curl -X POST http://localhost:3030/ds/data \
     --data-binary @companies_eu.ttl \
     -H "Content-Type: text/turtle"
```

---

<!-- .slide: class="section" -->

<header>
	<h1>Shrnutí a nástroje</h1>
</header>

---

# Kdy použít RDF/SPARQL integraci?
- Vhodné pro:
	- Heterogenní zdroje s různou sémantikou
	- Potřeba sdílené ontologie (standardizovaný slovník)
	- Integrace s veřejnými linked data zdroji
	- Dlouhodobě udržitelná integrace (schéma v ontologii)
- Méně vhodné pro:
	- Jednoduché integrace stejnorodých dat
	- Vysoký throughput / nízká latence (SPARQL není optimalizovaný jako SQL)
	- Týmy bez zkušeností s RDF

---

# Klíčové nástroje

| Kategorie | Nástroje |
|---|---|
| Triple store | Apache Jena/Fuseki, Virtuoso, Stardog, GraphDB |
| Mapování | Ontop, RMLMapper, D2RQ |
| Editace ontologií | Protégé, TopBraid Composer |
| SPARQL klient | YASGUI, Blazegraph workbench |
| Linked Data | Linked Data Fu, LodView |

---

# Srovnání integračních přístupů

| Přístup | Sémantika | Flexibilita | Výkon | Složitost |
|---|---|---|---|---|
| ETL + SQL DWH | Nízká | Nízká | Vysoký | Střední |
| ESB / API | Nízká | Střední | Střední | Střední |
| RDF + SPARQL | Vysoká | Vysoká | Střední | Vysoká |
| Knowledge Graph | Vysoká | Vysoká | Střední | Velmi vysoká |

---

# Trendy v datové integraci
- **Data Mesh** – decentralizovaná architektura, data jako produkt
- **Lakehouse** – kombinace data lake a data warehouse (Delta Lake, Iceberg)
- **AI-assisted integration** – LLM pro automatické mapování schémat
- **Knowledge Graphs + AI** – retrieval-augmented generation (RAG) nad KG
- **Semantic Layer** – sdílené business definice nad datovými sklady (dbt Semantic Layer, AtScale)
