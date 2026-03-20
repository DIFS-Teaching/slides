<!-- .slide: class="section" -->

<header>
	<h1>Datová integrace</h1>
	<p>Co to je a proč ji potřebujeme</p>
</header>

---

# Datová integrace
- Proces **slučování dat z více heterogenních zdrojů** do jednotného pohledu
- Cílem je poskytnout uživatelům nebo aplikacím **konzistentní, ucelený přístup** k datům bez ohledu na jejich umístění a formát
- Klíčová oblast v podnikových IS, analytice, výzkumu i na webu

---

# Proč integrovat data?
- Reálné organizace mají **mnoho různých systémů**
	- ERP, CRM, skladové systémy, účetnictví, webové aplikace, …
	- Historicky pořizované nezávisle, různí dodavatelé
- Potřeba **kombinovat** data pro rozhodování, reporting, analytiku
- Nárůst **externích datových zdrojů**
	- Open data, partnerské systémy, API třetích stran, …

---

# Příklad: situace v podniku

- Zákaznická data v CRM
- Objednávky v ERP
- Sklad v samostatném WMS systému
- Fakturace v účetním softwaru
- Webová analytika v Google Analytics
- Každý systém má **vlastní datový model, formát, identifikátory**

Jak zjistit celkový přehled o zákazníkovi? <!-- .element: class="cite" -->

---

# Typy heterogenity

- **Systémová heterogenita**
	- Různé databázové systémy (MySQL, Oracle, MongoDB, …)
	- Různá rozhraní (SQL, REST, SOAP, soubory, …)
- **Strukturální (schématická) heterogenita**
	- Různé datové modely (relační, dokumentový, grafový, …)
	- Různá schémata pro stejná data
- **Sémantická heterogenita**
	- Stejná data mají různý název nebo různý význam
	- Různé datové typy, jednotky, kódování, konvence

---

# Příklad schématické heterogenity

Zákazník v systému A:
```
customer(id, first_name, last_name, email, phone)
```

Zákazník v systému B:
```json
{ "clientId": "…", "fullName": "…", "contacts": { "mail": "…" } }
```

Zákazník v systému C:
```xml
<Person><Name>…</Name><Surname>…</Surname></Person>
```

---

# Příklad sémantické heterogenity

- `price` – cena s DPH nebo bez DPH?
- `status = 1` – aktivní, nebo vyřízený?
- `customer_id` v systému A ≠ `customer_id` v systému B (různé číselníky)
- Datum ve formátu `DD.MM.YYYY` vs. `YYYY-MM-DD` vs. Unix timestamp
- „Produkt" v obchodním systému ≠ „Produkt" ve výrobním systému

---

# Základní přístupy k integraci

- **Fyzická integrace** – data se přesunou (zkopírují) na jedno místo
	- Datový sklad, data lake
	- ETL procesy
- **Virtuální integrace** – data zůstávají na místě, integrační vrstva je zpřístupňuje
	- Federated database, data virtualization
	- API gateways
- **Hybridní přístupy** – kombinace obou

---

# Dimenze integrace

| | **Batch** | **Real-time** |
|---|---|---|
| **Fyzická** | ETL, datový sklad | CDC, streaming |
| **Virtuální** | Reportovací dotazy | API Gateway, ESB |

- **Batch** – data se zpracovávají dávkově (periodicky)
- **Real-time** – data se zpracovávají okamžitě nebo s minimálním zpožděním
- **CDC** – Change Data Capture

---

<!-- .slide: class="section" -->

<header>
	<h1>Klíčové problémy integrace</h1>
</header>

---

# Identifikace entit (Entity Resolution)
- Jak poznat, že zákazník v systému A je tentýž jako v systému B?
	- Různé identifikátory, různá jména (zkratky, překlepy)
- Techniky:
	- **Deterministické**: shoda klíčových atributů (rodné číslo, IČO, e-mail)
	- **Probabilistické**: váhovaná podobnost více atributů
	- **Strojové učení**: klasifikace dvojic záznamů (match / no-match)

---

# Čištění a transformace dat
- Data ze zdrojových systémů bývají **nekonzistentní, neúplná, chybná**
- Nutné kroky:
	- Normalizace formátů (data, adresy, telefonní čísla)
	- Deduplikace záznamů
	- Doplnění chybějících hodnot
	- Převod kódovníků a číselníků
- Nástrojová podpora: Talend, dbt, Great Expectations, …

---

# Správa metadat
- Aby integrace fungovala dlouhodobě, je třeba dokumentovat **co, odkud a jak**
- **Data katalog** – inventář datových zdrojů, jejich schémat a obsahu
- **Data lineage** – původ a transformace dat (odkud pochází, co se s nimi stalo)
- **Data governance** – pravidla a procesy pro správu dat v organizaci
- Nástroje: Apache Atlas, Collibra, Alation, DataHub

---

# Konzistence a transakce
- Při fyzické integraci: **jak zajistit konzistenci** mezi zdrojem a cílem?
	- Zdrojová data se mění, cílová jsou snapshot
- **CAP teorém** – v distribuovaném systému nelze mít současně:
	- Konzistenci (Consistency)
	- Dostupnost (Availability)
	- Odolnost vůči rozdělení sítě (Partition tolerance)
- Integrace musí explicitně řešit volbu mezi těmito vlastnostmi
