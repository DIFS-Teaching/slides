<!-- .slide: class="section" -->

<header>
    <h1>4. Tutoriál</h1>
    <span>Leaflet, clustering, choropleth, heatmap<span>
</header>

---

# Tutoriál: mapa středních škol

- datová sada: [schools.json](assets/data/schools-viewer.html) -- střední školy v ČR s počtem studentů (`value`)
- vyjdeme z prázdné kostry a funkcionalitu budeme přidávat postupně, krok za krokem

<pre class="code-render" src="assets/tutorial/06-heatmap.html" resizable="true" style="height: 650px;"></pre>

<div class="note">Ukázka výsledného stavu (krok 6), zdroj: <a href="assets/tutorial/06-heatmap.html">zde</a></div>

---

# Tutoriál: postup

0. [Prázdná mapa](assets/tutorial/00-prazdna-mapa.html) -- výchozí kostra
1. [Bodová mapa](assets/tutorial/01-body-mapa.html) -- marker pro každou školu
2. [Hodnota na markeru](assets/tutorial/02-hodnoty.html) -- kruh s číslem `value`
3. [Clustering](assets/tutorial/03-clustering.html) -- shlukování pomocí Leaflet.markercluster
4. [Vrstva krajů](assets/tutorial/04-kraje.html) -- GeoJSON hranice krajů
5. [Choropleth](assets/tutorial/05-choropleth.html) -- obarvení krajů dle agregované hodnoty
6. [Heatmap](assets/tutorial/06-heatmap.html) -- teplotní mapa pomocí Leaflet.heat

---

<!-- .slide: class="editor" -->

# Tutoriál -- 0. prázdná mapa

<div data-iframe="assets/tutorial/00-prazdna-mapa.html"></div>

<div class="note">Výchozí kostra ke stažení, zdroj příkladu: <a href="assets/tutorial/00-prazdna-mapa.html">zde</a></div>

---

# Krok 1: bodová mapa

- načteme data škol z [`schools.json`](assets/data/schools-viewer.html)
- pro každou školu vytvoříme *`L.marker`* s popupem (název, počet studentů)
- mapu přiblížíme na hranice všech škol (*`fitBounds`*)

```js
fetch('assets/data/schools.json')
  .then(response => response.json())
  .then(data => {
    const schools = data.schools.filter(s => s.lat && s.lon);

    const markers = schools.map(s =>
      L.marker([s.lat, s.lon])
        .bindPopup(`<b>${s.schoolName}</b><br>Počet studentů: ${s.value}`)
    );

    const layer = L.featureGroup(markers).addTo(map);
    map.fitBounds(layer.getBounds(), { padding: [20, 20] });
  });
```

---

<!-- .slide: class="editor" -->

# Tutoriál -- 1. bodová mapa

<div data-iframe="assets/tutorial/01-body-mapa.html"></div>

<div class="note">Data škol z <a href="assets/data/schools-viewer.html">schools.json</a>, zdroj příkladu: <a href="assets/tutorial/01-body-mapa.html">zde</a></div>

---

# Krok 2: hodnota na markeru

- výchozí špendlíkovou ikonu nahradíme vlastní ikonou -- barevný kruh
- do kruhu vypíšeme hodnotu *`value`* pomocí *`L.divIcon`*

```js
function valueIcon(value) {
  return L.divIcon({
    className: '',
    html: `<div class="value-marker">${value}</div>`,
    iconSize: [30, 30]
  });
}

L.marker([s.lat, s.lon], { icon: valueIcon(s.value) })
  .bindPopup(`<b>${s.schoolName}</b><br>Počet studentů: ${s.value}`);
```

<span class="note">vzhled kruhu (*`.value-marker`*) definuje CSS -- viz zdroj příkladu</span>

---

<!-- .slide: class="editor" -->

# Tutoriál -- 2. hodnota na markeru

<div data-iframe="assets/tutorial/02-hodnoty.html"></div>

<div class="note">Marker jako <code>L.divIcon</code> s hodnotou "value", zdroj příkladu: <a href="assets/tutorial/02-hodnoty.html">zde</a></div>

---

# Krok 3: clustering

- přidáme plugin [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster)
- markery zabalíme do *`L.markerClusterGroup`* -- blízké školy se spojí do jedné bubliny
- přes *`L.control.layers`* přidáme přepínač mezi vrstvou bez shlukování a se shlukováním

```js
const clusterLayer = L.markerClusterGroup();
clusterLayer.addLayers(createMarkers(schools));

L.control.layers({
  "Bez shlukování": plainLayer,
  "Se shlukováním": clusterLayer
}).addTo(map);
```

---

<!-- .slide: class="editor" -->

# Tutoriál -- 3. clustering

<div data-iframe="assets/tutorial/03-clustering.html"></div>

<div class="note">Plugin <a href="https://github.com/Leaflet/Leaflet.markercluster">Leaflet.markercluster</a>, přepínání pomocí <code>L.control.layers</code>, zdroj příkladu: <a href="assets/tutorial/03-clustering.html">zde</a></div>

---

# Krok 4: vrstva krajů

- kromě *`schools.json`* načteme i *`kraje.json`* (přes *`Promise.all`*)
- hranice krajů vykreslíme jako *`L.geoJSON`* vrstvu
- přidáme ji do ovládacího prvku jako ***překryvnou*** vrstvu -- lze ji zapnout/vypnout nezávisle na markerech

```js
const krajeLayer = L.geoJSON(null, {
  style: { color: '#2a6f97', weight: 2, fillOpacity: 0 },
  onEachFeature: (feature, layer) => layer.bindPopup(feature.properties.name)
});

Promise.all([
  fetch('assets/data/schools.json').then(r => r.json()),
  fetch('assets/data/kraje.json').then(r => r.json())
]).then(([schoolsData, krajeData]) => {
  krajeLayer.addData(krajeData);

  L.control.layers(
    { "Bez shlukování": plainLayer, "Se shlukováním": clusterLayer },
    { "Kraje ČR": krajeLayer }
  ).addTo(map);
});
```

---

<!-- .slide: class="editor" -->

# Tutoriál -- 4. vrstva krajů

<div data-iframe="assets/tutorial/04-kraje.html"></div>

<div class="note">GeoJSON hranic krajů z <a href="assets/data/kraje-viewer.html">kraje.json</a>, zdroj příkladu: <a href="assets/tutorial/04-kraje.html">zde</a></div>

---

# Krok 5: choropleth

- sečteme hodnotu *`value`* všech škol podle kraje
  - klíč *`ISO3166-2-lvl4`*, stejný jako `id` v `kraje.json`
- podle součtu obarvíme jednotlivé kraje (choropleth)
- přidáme legendu barevné škály

```js
const sumsByKraj = {};
schools.forEach(s => {
  const id = s.address && s.address['ISO3166-2-lvl4'];
  if (!id) return;
  sumsByKraj[id] = (sumsByKraj[id] ?? 0) + s.value;
});

const krajeLayer = L.geoJSON(krajeData, {
  style: feature => ({
    color: '#555',
    weight: 1,
    fillColor: getColor(sumsByKraj[feature.properties.id] ?? 0),
    fillOpacity: 0.7
  })
});
```

---

<!-- .slide: class="editor" -->

# Tutoriál -- 5. choropleth

<div data-iframe="assets/tutorial/05-choropleth.html"></div>

<div class="note">Agregace hodnoty *`value`* po krajích a jejich vybarvení dle součtu, zdroj příkladu: <a href="assets/tutorial/05-choropleth.html">zde</a></div>

---

# Krok 6: heatmap

- přidáme plugin [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat)
- vytvoříme teplotní mapu, kde intenzita bodu odpovídá hodnotě *`value`*
- heatmapa bude ve výchozím stavu zapnutá místo choroplethu

```js
const heatPoints = schools.map(s => [s.lat, s.lon, s.value]);
const heatLayer = L.heatLayer(heatPoints, {
  radius: 30, blur: 20, max: 8, minOpacity: 0.4
});

heatLayer.addTo(map);
```

- "max" je nízké schválně -- většina škol má "value" v jednotkách (medián 2), skutečné maximum 67 je ojedinělý extrém

---

<!-- .slide: class="editor" -->

# Tutoriál -- 6. heatmap

<div data-iframe="assets/tutorial/06-heatmap.html"></div>

<div class="note">Plugin <a href="https://github.com/Leaflet/Leaflet.heat">Leaflet.heat</a>, zdroj příkladu: <a href="assets/tutorial/06-heatmap.html">zde</a></div>
