<!-- .slide: class="section" -->

<header>
	<h1>Sémantická integrace dat</h1>
	<p>Ontologie jako základ pro porozumění mezi systémy</p>
</header>

---

# Proč nestačí technická integrace?
- Technická integrace řeší **připojení** a **přenos** dat
- Sémantická heterogenita přetrvává:
	- Pojmy mají různé názvy (`customer` vs. `client` vs. `Person`)
	- Pojmy mají různý rozsah (`product` zahrnuje i služby vs. jen fyzické zboží)
	- Stejný název má různý obsah (`status`, `type`, …)
- Výsledek: integrace je **křehká**, závislá na ručně psaném kódu

---

# Sémantická integrace
- Cíl: zajistit, aby systémy **rozuměly** datům, ne jen aby je přenášely
- Přístupy:
	- **Sdílené schéma** – všechny systémy hovoří stejným jazykem
	- **Kanonický datový model** – společný formát pro transformace
	- **Ontologie** – formální sdílená konceptualizace domény

---

# Ontologie pro integraci
- Ontologie definuje **slovník** (pojmy, vlastnosti, vztahy) sdílený všemi účastníky
- Každý systém mapuje svá lokální data na pojmy ontologie
- Výhody:
	- Formalizovaná sémantika (ne jen dokumentace)
	- **Strojově zpracovatelné** mapování
	- Možnost logického odvozování (inference)
- Viz UPA – Sémantický web: pojmy tříd, vlastností, hierarchie

---

# Schéma integrace pomocí ontologie

```
  Systém A                    Sdílená ontologie          Systém B
  ─────────                   ─────────────────          ────────
  customer                ──▶  foaf:Person          ◀──  klient
  customer.email          ──▶  foaf:mbox            ◀──  kontakt.mail
  customer.address.city   ──▶  schema:addressLocality◀── bydliste.mesto
```

- Místo přímého mapování A→B se obě strany mapují na ontologii
- **N mapování** místo N² přímých mapování

---

# Typy mapování schémat

- **Ekvivalence**: `local:Customer` ≡ `foaf:Person`
- **Subsumpce**: `local:Employee` je podtřídou `foaf:Person`
- **Transformace**: `price_with_vat` = `net_price × 1.21`
- **Přejmenování atributů**: `fname` → `foaf:firstName`
- **Rozdělení/sloučení**: `fullname` → `foaf:firstName` + `foaf:lastName`
- **Podmíněné mapování**: `type = "F"` → instance `foaf:Person`

---

# Doménové ontologie pro integraci

- **Schema.org** – obecné entity (Person, Organization, Product, Event, …)
	- Široce adopté, podporuje Google, Bing, …
- **Dublin Core** – metadata dokumentů a datových sad
- **Good Relations** – e-commerce (produkty, nabídky, obchody)
- **HL7 FHIR** – zdravotnictví (pacienti, diagnózy, léky, …)
- **PROV-O** – provenance dat (původ, transformace, agenti)
- **DCAT** – popis datových katalogů a datasetů

---

# Příklad: Healthcare integrace

- Nemocniční systémy: různí dodavatelé, různé terminologie
	- ICD-10 (diagnózy), SNOMED CT (klinické pojmy), LOINC (laboratorní výsledky)
- Integrace přes sdílenou ontologii (HL7 FHIR):
	- Každý systém mapuje lokální kódy na standardní koncepty
	- Dotazy se pokládají v termínech FHIR
- **Výsledek**: přenositelnost dat mezi nemocnicemi, klinickými studiemi, pojišťovnami

---

# Problémy sémantického mapování

- Mapování je pracné a vyžaduje znalost domény
- **Nejednoznačnosti**: jeden pojem může být namapován různě
- **Neúplná ontologie**: doménová ontologie nemusí pokrýt vše
- **Evolvující schémata**: zdrojové systémy se mění → mapování zastarávají
- Možné řešení: **strojové učení** pro (polo)automatické mapování
	- Schema matching, entity alignment, …

---

# Linked Data principy (Tim Berners-Lee)
1. Používej **URI** jako identifikátory věcí
2. Používej **HTTP URI** – aby šly vyhledat
3. Při přístupu na URI poskytni **užitečné informace** (v RDF)
4. Zahrň **odkazy** na jiné URI – propojení s jinými zdroji

- Linked Data = RDF + HTTP + URI + propojení
- Základ pro globální **web dat** (Web of Data)

---

# Linked Data a integrace
- Různé datové zdroje jsou propojeny přes **sdílené URI**
- Příklad: DBpedia, Wikidata, GeoNames jsou navzájem propojeny
- Integrační dotaz může procházet **federovaně** napříč datasety
- Klíčový predikát: `owl:sameAs` – stejný subjekt v různých zdrojích

```turtle
<http://dbpedia.org/resource/Prague>
    owl:sameAs <http://www.wikidata.org/entity/Q1085> ;
    owl:sameAs <http://sws.geonames.org/3067696/> .
```
