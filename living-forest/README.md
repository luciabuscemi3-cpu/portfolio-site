# Living Forest Ecosystems Project - prototype

Three screens, built on the ArcGIS Maps SDK for JavaScript:

1. **Welcome map** - click a territory (Lummi, Klallam, Skokomish). Where two overlap you get a chooser.
2. **Forest screen** - a muted looping panorama video autoplays; "Listen to stories" fades in at the center of the screen; "Learn what is at risk" appears once stories are opened.
3. **Risk map** - the territory outline plus only the timber sales inside it.

## Run it

You need Python. Unzip this folder, then in Terminal (Mac) or Command Prompt (Windows):

    cd path/to/living-forest
    python3 -m http.server 8000      (Windows: python -m http.server 8000)

Open http://localhost:8000. Keep that window open while you use the app.

## Edit content (no code): content.json

- `settings` - welcome text, map start position, delay before the stories button appears
- `territories` - one entry per territory; the key must match the `name` in territories.geojson exactly
  - `panoramaVideo` - e.g. "videos/lummi-forest.mp4"
  - `stories` - list of {title, speaker, video, captions (.vtt), description}
  - `riskNote` - text on the risk screen

Put video files in a `videos` folder next to index.html.

## IMPORTANT: placeholder data

- `territories.geojson` holds three **general-area circles** (around Port Angeles, Ferndale and Skokomish), not boundaries. Replace them with boundaries the tribes provide or approve before any public launch.
- `timber_sales.geojson` holds **made-up sample polygons**. Replace with real WA DNR / USFS timber sale data.

To replace either one, overwrite the .geojson file and keep the `name` attribute (territories) matching the keys in content.json.

## Maps

The background maps are Esri's classic public tile services (World Topo Map and World Imagery), loaded without a key or sign-in.
If they ever stop loading, change `basemapUrl` / `riskBasemapUrl` in content.json to the free USGS tiles instead:
- https://basemap.nationalmap.gov/arcgis/rest/services/USGSTopo/MapServer
- https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer
