<!-- .slide: class="section" -->

<header>
	<h1>Integrita a konzistence</h1>
	<p>Databázová integrita, konzistence, OLTP jako model</p>
</header>

---

# Databázová integrita
- Databáze vyhovuje zadaným pravidlům – **integritním omezením (IO)**
	- Za jejich splnění zodpovídá **systém řízení báze dat (SŘBD)**
- IO mohou být zadána výrazem (*deklarativně*) nebo programem (*procedurálně*)
- IO se mohou týkat:
	- *jednotlivých hodnot* – např. známka musí být 1–5
	- *kombinace hodnot* v záznamu – datum narození < datum úmrtí
	- *celé množiny záznamů* – unikátnost čísla průkazu

---

# Konzistence
- Databáze splňuje všechna **integritní omezení**
- Udržování **interní konzistence** – redundantní, replikovaná data v distribuovaných systémech
- Dodržování **pravidel daných modelovaným systémem**

---

# OLTP jako model

![OLTP jako model](assets/oltp-model.svg) <!-- .element: style="height:500px;margin:0.5em auto;display:block" -->

- Mezi OLTP a jeho fyzickým vzorem existuje **izomorfismus** *j*
- Každé funkci fyzického systému odpovídá její obraz v IS a naopak

---

# Nezbytnost abstrakce
- Není možné modelovat všechny zdroje a procesy fyzického systému
- Vždy se vybírají jen ty podstatné pro danou úroveň řízení – **abstrakce**
- OLTP je proto vždy modelem jisté **abstrakce původního fyzického vzoru**

---

# Příklad OLTP systému
- Ve fyzickém systému se pracuje se **skutečnými penězi** → v IS s jejich **virtuálním obrazem**
- Fyzická funkce „vytvoření faktury na základě objednávky" → v IS je vytvořen její obraz
- Bankovní operace: převod peněz mezi účty = transakce v IS

---

# Procesy ve schématu IS

![Schéma informačního systému](assets/is-schema.svg) <!-- .element: style="height:450px;margin:0.5em auto;display:block" -->

- IS se skládá z **dat** uchovávajících *stav* systému a **procesů** realizujících transformace
- Transformace jsou často implementovány ve formě **transakcí**
