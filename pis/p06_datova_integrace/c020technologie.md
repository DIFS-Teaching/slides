<!-- .slide: class="section" -->

<header>
	<h1>Technologie datové integrace</h1>
	<p>ETL, EAI, API, streaming a další</p>
</header>

---

# ETL – Extract, Transform, Load
- Klasický přístup pro **dávkovou integraci** do datového skladu
- Tři fáze:
	1. **Extract** – extrakce dat ze zdrojových systémů
	2. **Transform** – transformace, čištění, normalizace
	3. **Load** – načtení do cílového úložiště (datový sklad, data lake)
- Varianta **ELT** (Extract, Load, Transform) – transformace až v cílovém systému

---

# ETL – architektura

```
 ┌──────────┐    ┌──────────────────┐    ┌─────────────┐
 │  Zdroj A │───▶│                  │───▶│             │
 ├──────────┤    │  ETL / Staging   │    │  Datový     │
 │  Zdroj B │───▶│  Area            │    │  sklad /    │
 ├──────────┤    │  (transformace,  │    │  Data Lake  │
 │  Zdroj C │───▶│  čištění)        │───▶│             │
 └──────────┘    └──────────────────┘    └─────────────┘
```

- Nástroje: **Apache Spark**, dbt, Talend, Informatica, Azure Data Factory

---

# Datový sklad (Data Warehouse)
- Centrální úložiště **historických** analytických dat
- Optimalizováno pro **čtení a analytiku** (OLAP)
- Schéma definováno předem (schema-on-write)
- Typická schémata: **hvězda** (star schema), **sněhová vločka** (snowflake)
- Příklady: Snowflake, Amazon Redshift, Google BigQuery, Microsoft Synapse

---

# Data Lake
- Úložiště **surových** dat v jejich nativním formátu
- Schéma se aplikuje až při čtení (schema-on-read)
- Podporuje strukturovaná, semi-strukturovaná i nestrukturovaná data
- Výhodné pro datovou vědu a experimentální analytiku
- Riziko: **„data swamp"** – bez metadat a governance rychle degeneruje

---

# EAI – Enterprise Application Integration
- Integrace **aplikací v rámci organizace** (ne datová analýza, ale operativní propojení)
- Dva základní modely:
	- **Point-to-point** – přímé propojení aplikací (N² spojení = chaos)
	- **Hub-and-spoke / ESB** – prostřednická sběrnice

---

# Enterprise Service Bus (ESB)
- Centrální integritní sběrnice propojující aplikace
- Zajišťuje:
	- Směrování zpráv
	- Transformaci formátů (XML, JSON, EDI, …)
	- Orchestraci procesů
	- Monitoring a logování
- Příklady: MuleSoft, WSO2, Apache Camel, IBM Integration Bus
- Trend: ESB ustupuje ve prospěch mikroslužeb a API

---

# Message Brokers a Event Streaming
- **Asynchronní** předávání zpráv mezi aplikacemi
- Decoupling producenta a konzumenta
- **Message broker**: RabbitMQ, ActiveMQ
	- Zprávy jsou doručeny a smazány
- **Event streaming**: Apache Kafka, AWS Kinesis
	- Události jsou trvale uloženy, konsumovány opakovaně
	- Vhodné pro real-time integraci a event sourcing

---

# Apache Kafka – základní koncepty
- **Topic** – kategorie/kanál pro události
- **Producer** – aplikace produkující události
- **Consumer** – aplikace čtoucí události
- **Consumer group** – skupina konsumentů sdílejících zátěž
- Události jsou **trvale uloženy** a přehratelné
- Použití: CDC, log aggregation, event-driven architektura

---

# API integrace
- Integrace přes **veřejná nebo interní API**
- Principy:
	- **REST API** – přenos dat přes HTTP, JSON/XML formáty
	- **GraphQL** – flexibilní dotazovací jazyk nad API
	- **gRPC** – binární protokol pro efektivní komunikaci (mikroslužby)
- Výhody: standardizované, verzovatelné, monitorovatelné
- Problém: **proliferace API** – stovky různých API bez jednotné sémantiky

---

# API Gateway
- Vstupní bod pro všechna API
- Zajišťuje: autentizaci, rate limiting, logování, směrování, transformaci
- Příklady: Kong, AWS API Gateway, Azure API Management
- Umožňuje vystavit **jednotné API** nad heterogenními backend systémy

---

# Change Data Capture (CDC)
- Sledování a zachycení **změn v databázi** v reálném čase
- Nevyžaduje modifikaci aplikace (čte transakční log DB)
- Použití: synchronizace datového skladu, invalidace cache, event sourcing
- Příklady nástrojů: **Debezium**, Oracle GoldenGate, AWS DMS
- Integruje se s Kafka pro streamování změn downstream systémům

---

# Data Virtualization
- Virtuální integrační vrstva – **data zůstávají na místě**
- Umožňuje dotazovat heterogenní zdroje jako jeden logický zdroj
- Transformace a spojování probíhá za běhu dotazu
- Výhody: žádná duplikace dat, vždy aktuální data
- Nevýhody: výkon (závisí na zdrojových systémech)
- Příklady: Denodo, Starburst (Trino), Dremio

---

# Master Data Management (MDM)
- Správa **klíčových (master) dat** sdílených napříč systémy
	- Zákazníci, produkty, zaměstnanci, lokace, …
- Cíl: jediná verze pravdy (Single Source of Truth)
- Procesy: identifikace, deduplikace, obohacování, distribuce
- MDM hub slouží jako autoritativní zdroj pro ostatní systémy
- Příklady: Informatica MDM, IBM InfoSphere MDM, Talend MDM

---

# Srovnání přístupů

| Přístup | Latence | Integrita | Složitost |
|---|---|---|---|
| ETL batch | Hodiny/dny | Vysoká | Střední |
| CDC / streaming | Sekundy | Střední | Vysoká |
| API integrace | Real-time | Nízká-střední | Střední |
| Data virtualization | Real-time | Střední | Nízká |
| ESB | Nízká | Střední | Vysoká |

---

# Integrace v praxi – příklad architektury

```
 Zdrojové systémy        Integrační vrstva        Konzumenti
 ┌───────────┐          ┌──────────────────┐      ┌──────────┐
 │ ERP (SQL) │──CDC────▶│                  │─────▶│ DWH /BI  │
 ├───────────┤          │  Apache Kafka    │      ├──────────┤
 │ CRM (API) │──REST───▶│  +               │─────▶│ ML model │
 ├───────────┤          │  ETL (Spark/dbt) │      ├──────────┤
 │ E-shop    │──events─▶│                  │─────▶│ Reporting│
 └───────────┘          └──────────────────┘      └──────────┘
```
