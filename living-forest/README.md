# Living Forest Ecosystems Project

Three screens, built on the ArcGIS Maps SDK for JavaScript:

1. **Welcome map** - click a territory (Lummi, Klallam, Skokomish).
2. **Forest screen** - a muted panorama video loops, forest sounds play from a separate audio file, and "Listen to stories" fades in at the center. It opens a large window with one story at a time (arrows and dots at the bottom); the forest video pauses while it is open.
3. **Risk map** - timber sales for that territory.

## Edit content (no code): content.json

`territories` - one entry per territory; the key must match the `name` in territories.geojson exactly:
- `panoramaVideo` - e.g. "videos/klallam-forest.mp4" (keep files under 25 MB for GitHub uploads)
- `ambientAudio` - optional forest-sounds file for this territory, e.g. "audio/forest.mp3"
- `timberSalesMatch` - the value in the timber sales layer's `Slug` column for this tribe ("klallam", "twana-skokomish"). Leave it out if the layer has no sales for that tribe (Lummi currently).
- `riskNote` - text on the risk screen
- `stories` - list of:
  - `speaker` - shown as the big heading, e.g. "Talesha Francis, Lower Elwha Klallam" (keep the word `speaker`; only the text after it is the name)
  - `title` - smaller line under the heading
  - `youtube` - video link or ID (or `video` for a small .mp4 file)
  - `captions` - optional .vtt file for `video` files
  - `description` - text under the video

`settings`:
- `ambientAudio` - one forest-sounds file used for every territory (a territory's own `ambientAudio` overrides it)
- `ambientVolume` (0 to 1) and `ambientDuckVolume` - volume normally, and while a story window is open
- `timberSalesLayer`, `timberSalesNameField`, `timberSalesPopup` - the timber sales layer and which columns the popup shows

Browsers only allow sound after a visitor has interacted with the page; the "Sound on" button covers cases where they block it.

## Placeholder data

`territories.geojson` holds three general-area circles (around Port Angeles, Ferndale and Skokomish), not boundaries. Replace them with boundaries the tribes provide or approve before any public launch.

## Maps

Background maps are Esri's classic public tile services (World Topo Map and World Imagery). If they ever stop loading, change `basemapUrl` / `riskBasemapUrl` in content.json to the free USGS tiles:
- https://basemap.nationalmap.gov/arcgis/rest/services/USGSTopo/MapServer
- https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer
