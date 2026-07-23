<!-- .slide: class="section" -->

<header>
    <h1>Data</h1>
    <span>geografická data, informace, znalosti<span>
</header>

---

# Data, informace, znalosti

<br>

- **data** -- surová fakta, čísla bez kontextu
  - např. *`31000`*
- **informace** -- data v kontextu, s významem
  - např. *"V Brně je 31 000 studentů."*
- **znalosti** -- pochopení souvislostí, umožňují rozhodování
  - např. *"Brno má hodně studentů, tak je to nejspíš univerzitní město a má hodně univerzit."*

<div class="block-center"><img src="assets/cat.jpg" style="max-width: 30%;"></div>

---

# Cíl

<!-- .slide: class="quote" -->

> Naším cílem vizualizovat data tak, aby ***vynikly znalosti užitečné pro člověka***

---

# Příklad: Jízdní řád -- Je možné snadno odvodit znalosti?

<div class="block-center"><img src="assets/jr.png" style="max-width: 80%;"></div>

<div class="note">Zdroj: přednáška <a href="https://gitshow.net/https/difs-teaching.github.io/slides/iis/p01_informacni_systemy#/19">Informační systémy</a> -- doc. Ing. Radek Burget, Ph.D.</div>

---

# Geografická data

<br>

- data, která navíc obsahují ***informaci o poloze***
- souřadnice, hranice, tvar geografického objektu
- ***data*** (co) + ***místo*** (kde) = geografická data

<p class="fragment">V další části si ukážeme, jak takové místo <strong>definovat</strong>.</p>

=--

# Geografická data -- souřadnice

<br>

- poloha jako přímý atribut záznamu -- ***lat***, ***lon***

```json
{
  "school": "108047792",
  "schoolName": "Gymnázium Jihlava",
  "lat": 49.3961,
  "lon": 15.5854,
  "value": 12
}
```

<br>

- souřadnice se udávají v souřadnicovém systému **WGS 84** -- celosvětový standard používaný GPS i webovými mapami
- v dokumentaci se často značí jako ***EPSG:4326***

=--

# Geografická data -- reference

<br>

- poloha jako ***odkaz/kód*** na geografický celek -- stát, kraj, město...
- samotný záznam souřadnice neobsahuje

```json
{
  "kraj_kod": "CZ064",
  "kraj": "Jihomoravský",
  "value": 31000
}
```

<br>

<p class="fragment">Kód se pak <strong>spojí</strong> s definicí místa (hranicemi kraje) -- to uvidíme v sekci <strong>Zobrazení</strong>.</p>
