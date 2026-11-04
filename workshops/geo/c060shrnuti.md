<!-- .slide: class="section" -->

<header>
    <h1>5. Shrnutí</h1>
    <span>co jsme se naučili, odkazy<span>
</header>

---

# Co jsme si ukázali

- **data** -- geodata jako speciální případ vícedimenzionálních dat
- **lokace** -- souřadnice (`lat`/`lon`, EPSG:4326) vs. reference (kódy regionů), geocoding, **GeoJSON**
- **prezentace** -- tematická mapa, mapové projekce, JS mapové knihovny
  - Leaflet, OpenLayers, MapLibre GL JS, ...
- **tutoriál** -- vlastní interaktivní mapa v Leafletu, krok za krokem:
  - body → hodnoty → clustering → vrstva krajů → choropleth → heatmap

---

# Podstatné pojmy

- **EPSG:4326** -- souřadnicový systém používaný GPS a webovými mapami
- **GeoJSON** (RFC 7946) -- formát pro zápis geografických dat v JSON
- **choropleth** -- tematická mapa vybarvující oblasti podle agregované hodnoty
- **clustering** -- shlukování blízkých bodů do jedné bubliny při menším přiblížení
- **heatmap** -- teplotní mapa vyjadřující hustotu/intenzitu bodů

---

# Zdroje a odkazy

- dokumentace: [leafletjs.com](https://leafletjs.com/), [openlayers.org](https://openlayers.org/), [maplibre.org](https://maplibre.org/maplibre-gl-js/docs/)
- formát dat: [geojson.org](https://geojson.org/), editor [geojson.io](https://geojson.io/)
- data z OpenStreetMap: [Overpass Turbo](https://overpass-turbo.eu/), [Nominatim](https://nominatim.openstreetmap.org/)
- pluginy použité v tutoriálu: [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster), [Leaflet.heat](https://github.com/Leaflet/Leaflet.heat)

<br>

- vlastní kód z tutoriálu ke stažení: [kostra](assets/tutorial/00-prazdna-mapa.html) a hotové kroky v sekci "4. Tutoriál"
