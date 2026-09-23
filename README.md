# conqueryourtown
Explore the real world and expand your kingdom - a GPS based game 

Development note: This project was developed using AI-assisted coding (often referred to as "vibe coding"). I designed the features and iterated on the application, using AI tools to help generate and modify the code.

## Changelog

### v1 — Original app
- Leaflet map: set a "capital" at your current GPS position, then track a walking/cycling trail as a polyline.
- Each GPS fix drawn as a semi-transparent 20 m circle.
- Trail and capital saved to `localStorage`.
- Known issues: tracking could freeze permanently after a single GPS jump >100 m (all later fixes were also rejected); stop/restart drew a straight line across the gap; no basemap options.

### v2 — Freeze fix, fog of war, basemap options
- **Fixed tracking freeze:** a jump >100 m is now held as a candidate and only accepted once a second fix confirms it within 60 s, so one bad GPS fix can no longer stall tracking permanently.
- **Segmented trail:** each Start press, and each confirmed relocation, begins a new line segment, so stopping/restarting or a bus ride no longer draws a straight line between unrelated points. Distance stat only sums steps within a segment.
- **Fog of war:** replaced the per-point circles with a full-map dark overlay; a 30 m radius is cleared along the trail and 120 m around the capital.
- **Basemap switch:** toggle between a street map (CARTO Voyager) and satellite imagery (Esri World Imagery).
- **Label toggle:** show/hide place-name labels independently of the basemap choice.
- Dropped fixes closer than 8 m apart, and fixes with GPS accuracy worse than 50 m, to reduce noise and storage use.

### v3 — Fog thickness control, CARTO API key
- **Fog opacity slider:** 0–100% in 5% steps, saved between visits, defaults to fully opaque (100%). Disabled while Fog is off.
- **CARTO API key added:** CARTO's raster basemap tiles (used for the Street map) now require a key; added as a `?key=` query parameter on the tile URLs so the Street layer loads without the "API key required" watermark. The key is public in the page source, as is normal for this kind of key — restrict it to your domain in CARTO's key settings if you haven't already.
