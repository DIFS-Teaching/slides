<!-- .slide: class="section" -->

<header>
	<h1>Návrh a implementace informačních systémů</h1>
	<p>Shrnutí</p>
</header>

---

# Model
- Stav modelu je uchováván v databázi podle zvoleného datového modelu, např.:
	- **_relační model_** (nejčastěji),
	- dokumentový, grafový a další modely (NoSQL),
	- objektový model, případně jinak.

---

# Databáze
- Databáze pro modelování stavu není podmínkou, specializované IS např. pro řízení výroby v reálném čase používají i jiné typy uchování dat, nicméně databáze jako sídlo stavu modelu je nejčastější.
- Realizace databázového modelu je technologickou a provozní otázkou a může být např.:
	- **_monolitický_** (lokalizovaný na jediném místě, s jednou databází),
	- **_distribuovaný_** (s více lokálními databázemi, zde pak vznikají problémy s konzistencí)

---

# Procesy
- Modelovacím prostředím **_procesů modelu_** je nejčastěji nějaký univerzální programovací jazyk kompilovaný nebo i interpretovaný. 
- Snahy o modelování formálnějšími prostředky jako jsou např. různé modifikace automatů, **_Petriho_** **_sítě_** nebo dnes nejčastěji notace **_BPMN_**. Při modelování procesů se musíme zabývat zejména:
	- udržováním **_konzistence_** systému,
	- **_paralelním během procesů (vícenásobným přístupem)_** a vzájemným ovlivňováním a
	- **_transakčním zpracováním_**_._

---

# Nezbytné znalosti technologie
- Chceme-li se tedy zabývat informačními systémy musíme se zabývat:
- Způsobem vytváření modelů, **_modelovacími technikami_** a to zejména:
	- **_konceptuálním modelováním_** jako výchozím prostředkem pro modelování dat (tj. definicí modelu stavu fyzického systému na jisté úrovni abstrakce), převodem konceptuálního modelu na model databázový,
	- **_modelováním procesů_** a tedy i
	- **_univerzálními modelovacími prostředky_**, jako je např. UML nebo BPMN.

---

# Nezbytné znalosti technologie
- **_Databázovými systémy_** a jejich použitím a to zejména:
	- různými **_typy databázových modelů_** a jejich univerzálním rozhraním a ovládáním
	- **_transakčním zpracováním_** a pojmem transakce,
	- **_konzistencí dat_**
- **_Modelováním procesů_** a jejich případnou formalizací a to zejména:
	- **_programovacími jazyky_** vhodnými pro definici procesů,
	- **_formálními metodami definice procesů_** a workflow systémy,
	- souvislosti procesů s transakcemi a integritou,
	- metodami **_spouštění procesů_**.
- **_Bezpečností_** – autentizace, autorizace, ochrana osobních údajů (GDPR).

---

# Nezbytné znalosti technologie
- **_Počítačovými sítěmi_** a to zejména:
	- technologií **_klient-server_** a vytváření klientské a serverové části informačního systému
	- **_webovými službami_** a API (REST)
- **_Vizualizací_** **_dat_** a to zejména:
	- hypertextovou prezentací v _HTML_ a pokročilejšími technikami (skripty, DOM),
	- prezentací pro dolování dat, **_OLAP_** a business intelligence.
- **_Mnohé z těchto témat pokrývají jeden nebo více samostatných povinných nebo volitelných předmětů. Zde se zabýváme jejich základy, zopakováním, doplněním a zejména spoluprací při vytváření komplexního systému_**.

