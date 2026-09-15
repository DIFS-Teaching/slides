<!-- .slide: class="section" -->

<header>
	<h1>SPARQL</h1>
	<p>Dotazování nad grafem &#8211; a splacení prvního dluhu</p>
</header>

---

# SPARQL je hledání vzoru v grafu

- Dotaz je **graf s proměnnými**; hledá se, čím je lze nahradit
- Proměnná začíná `?`; každý řádek vzoru je jedna trojice

```sparql
SELECT ?mesto ?pocet WHERE {
  ?mesto  wdt:P31    wd:Q5153359 .   # ?mesto je obec v Česku
  ?mesto  wdt:P1082  ?pocet .        # ?mesto má počet obyvatel ?pocet
}
```

- Databáze najde všechna přiřazení, pro která vzor v grafu existuje
- ??Žádné tabulky, žádné JOINy -- spojení vzniká **opakováním proměnné**

---

# Čtyři formy dotazu

<div class="small">

| Forma | Výsledek | K čemu v pipeline |
|---|---|---|
| `SELECT` | tabulka (CSV, JSON) | načtu do pandas a pracuji dál |
| `CONSTRUCT` | **nový graf** | transformace: cizí slovník na vlastní |
| `ASK` | `true` / `false` | kontrola kvality, test v CI |
| `DESCRIBE` | graf okolo zdroje | průzkum neznámých dat |

</div>

- ??Navíc **SPARQL UPDATE**: `INSERT DATA`, `DELETE WHERE`, `LOAD`
- ??SPARQL není jen pro čtení -- je to plnohodnotný dotazovací i aktualizační jazyk

---

# Ten dotaz z minulé přednášky

<div class="small">

```sparql
SELECT ?mestoLabel ?obyvatel WHERE {
  ?mesto wdt:P31 wd:Q5153359 ;       # je obec v Česku
         wdt:P1082 ?obyvatel .       # má počet obyvatel
  SERVICE wikibase:label { bd:serviceParam wikibase:language "cs". }
}
ORDER BY DESC(?obyvatel)
```

- `wd:Q5153359` -- **entita** &bdquo;obec v Česku&ldquo;
- `wdt:P31` -- **vlastnost** &bdquo;instance čeho&ldquo;
- `wdt:P1082` -- vlastnost &bdquo;počet obyvatel&ldquo;
- `?mestoLabel` -- proměnná, kterou **nikde nedeklaruji**; doplní ji `SERVICE wikibase:label`

<p class="fragment" style="text-align: center; font-size: 130%;"><strong>Dluh č. 1 a 2 splacen.</strong></p>

</div>

Note:
Na minulé přednášce byl u Q5153359 komentář &bdquo;statutární město&ldquo; -- to bylo
špatně, je to &bdquo;obec v Česku&ldquo;. Výsledky vyšly správně jen proto, že Praha,
Brno, Ostrava a Plzeň jsou největší obce. Dobrá ukázka toho, jak snadno se
u cizího slovníku splete význam identifikátoru.

---

# Jak je postavená Wikidata

<div class="col small">

**Prefixy**

- `wd:` -- entity (`wd:Q14960` = Brno)
- `wdt:` -- vlastnost, *zkratka*
- `p:` -- vlastnost jako **celé tvrzení**
- `ps:` -- hodnota uvnitř tvrzení
- `pq:` -- **kvalifikátor** tvrzení

</div>
<div class="col small">

**Proč to není jedno**

`wdt:` je předpočítaná ``truthy'' zkratka: vrátí jen tu hodnotu, která
platí teď. Je rychlá a pro devět z deseti dotazů stačí.

`p:`/`ps:`/`pq:` vrátí tvrzení celé -- i s časovou platností a zdrojem.

</div>

@@div style="clear:both"@@@@/div@@


- Každý dotaz na Wikidata je tedy volba mezi **pohodlím** a **úplností**

---

# Kvalifikátory: kdo je primátor Brna?

```sparql
SELECT ?xLabel WHERE {
  wd:Q14960 wdt:P6 ?x .
  SERVICE wikibase:label { bd:serviceParam wikibase:language "cs". }
}
```

```
Markéta Vaňková
```

Jeden řádek. **Kde je historie?**

Note:
Tady se zastavit a nechat sál chvíli přemýšlet. Odpověď není chyba v datech --
data jsou kompletní, jen se na ně ptám zkratkou, která historii mlčky zahodí.

---

# Kvalifikátory: celé tvrzení

<div style="font-size: 88%">

```sparql
SELECT ?xLabel ?od ?do WHERE {
  wd:Q14960 p:P6 ?st .          # celé tvrzení o funkci
  ?st ps:P6 ?x .                # kdo
  OPTIONAL { ?st pq:P580 ?od }  # od kdy
  OPTIONAL { ?st pq:P582 ?do }  # do kdy
  SERVICE wikibase:label { bd:serviceParam wikibase:language "cs". }
} ORDER BY DESC(?od)
```

<div class="small">

| | od | do |
|---|---|---|
| Markéta Vaňková | 2018-11-20 | |
| Petr Vokřál | 2014-11-25 | 2018-11-20 |
| dalších šest, až do roku 1990 | | |

</div>

- ??`wdt:` je zkratka, která **mlčky zahodí časovou platnost**; tvrzení o tvrzení = *reifikace* (v RDF 1.2 na to budou *triple terms*)

</div>

---

# SPARQL 1.1: co použijete nejčastěji

<div class="col small">

**Cesty ve vzoru** (*property paths*)

```sparql
wd:Q14960 wdt:P131+ ?nadrazenyCelek .
```
`+` jedenkrát a více &middot; `*` nula a více &middot; `/` zřetězení &middot; `^` obráceně

**Agregace**

```sparql
SELECT ?okres (COUNT(*) AS ?pocet)
WHERE { ?obec wdt:P31 wd:Q5153359 ;
              wdt:P131 ?okres . }
GROUP BY ?okres HAVING (?pocet > 100)
```

</div>
<div class="col small">

**`VALUES`** -- vložím vlastní sloupec dat

```sparql
VALUES ?ico { "00216305" "45274649" }
```

**Další**

`OPTIONAL` (levé spojení) · `FILTER` · `MINUS` · `UNION` · poddotazy · `LIMIT` / `OFFSET`

</div>

@@div style="clear:both"@@@@/div@@


<p class="fragment" style="text-align: center; font-size: 130%; margin-top: 0.4em;">Zkuste <code>wdt:P131+</code> napsat v SQL.</p>

Note:
Tranzitivní uzávěr na jednom znaku. V SQL je to rekurzivní CTE na osm řádků.
Tohle je nejlepší jednořádkový argument pro grafové dotazovací jazyky --
a vrátíme se k němu v desáté přednášce.

---

# Kde to spustit

- Veřejné endpointy: [query.wikidata.org](https://query.wikidata.org) · [dbpedia.org/sparql](https://dbpedia.org/sparql) · [data.gov.cz/sparql](https://data.gov.cz/sparql) · [qlever.dev](https://qlever.dev/)
- Editor [YASGUI](https://yasgui.triply.cc/) -- zvýrazňování, našeptávání, export
- Z programu: HTTP GET/POST na endpoint, výsledek jako JSON nebo CSV

```python
import requests

r = requests.get("https://query.wikidata.org/sparql",
                 params={"query": open("dotaz.rq").read()},
                 headers={"Accept": "text/csv"})
open("obce.csv", "w").write(r.text)
```

- ??Vždy začínejte s `LIMIT` -- endpointy mají **timeout i rate limit**
- ??Na velký objem stáhnout dump a nahrát lokálně (Fuseki, Oxigraph, QLever)

Note:
Ten curl je záměrně tentýž tvar jako minulý týden u ARES a ČNB. Jediný rozdíl
je, že se neptám na soubor, ale na graf.
