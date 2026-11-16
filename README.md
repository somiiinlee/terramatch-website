# TerraMatch — Interactive Web Edition

This is a first browser-based website edition of the InterSESHllar OpenSpace project. It reuses the repository's existing `TEAM_DATA` (including site coordinates and precomputed category similarity scores) and GeoJSON boundaries, and adds a browser-rendered interactive 3D Earth/Mars globe.

## Run locally

Because the page loads GeoJSON with `fetch()`, serve the folder over HTTP rather than opening `index.html` directly.

```bash
cd website
python -m http.server 8000
```

Then open http://localhost:8000.

## Publish

The `website/` folder is a static site and can be deployed with GitHub Pages, Netlify, or Vercel. For GitHub Pages, set the publishing source to the `/website` folder if your repository settings support it, or move the contents of this folder to the repository root / a `docs/` folder.

## What works in this first web edition

- Browser-based 3D globe for Earth and Mars (Globe.gl / Three.js).
- Clickable analog-site markers and site selector.
- Earth analog and Gale Crater boundary overlays from the repository GeoJSON.
- Site coordinates and descriptions from `TEAM_DATA`.
- Category similarity bars and adjustable weighted score using the existing precomputed category scores.
- A guided flythrough that cycles through the five sites.
- Responsive dashboard layout.

## Important scope notes

- This is a web edition, not an OpenSpace runtime. It does not use the OpenSpace WebSocket at `localhost:4682`, OpenSpace Lua assets, native OpenSpace camera controls, or OpenSpace's high-resolution planetary terrain layers.
- The globe textures are loaded from public third-party URLs; an internet connection is required. Globe.gl is loaded from unpkg CDN.
- The category scores are the existing precomputed values in `user/webpanels/mars_earth_analogs/js/team-data.js`. The sliders recompute the weighted aggregate from those category scores; they do not rerun the original full data-processing pipeline.
- The original Gemini service is not connected in this static build. Do not put a shared Gemini API key in client-side JavaScript. A public AI optimizer should be connected through a server-side function that keeps the key private.
- The current implementation is a deployable starting point. The original dashboard's remaining detailed modals, live SoilGrids query, AI optimizer, detailed time-series charts, and high-resolution 3D terrain still need to be ported and tested as separate work.

## Source mapping

- `js/team-data.js`: copied from `user/webpanels/mars_earth_analogs/js/team-data.js`.
- `geojson/`: copied from the repository's `geojson/` directory.
- All other files in this folder are the new browser website layer.
