# conqueryourtown
Explore the real world and expand your kingdom - a GPS based game 

Development note: This project was developed using AI-assisted coding (often referred to as "vibe coding"). I designed the features and iterated on the application, using AI tools to help generate and modify the code.

## Setup

The Street basemap requires a CARTO API key.

1. Obtain a CARTO basemap key.
2. Replace `YOUR_CARTO_API_KEY` in the code with your key.
3. Restrict the key to your deployment domain where possible.

## Version History

### V1: Original App

* **Leaflet map:** Set a "capital" at your current GPS position, then track a walking or cycling trail as a polyline.
* **GPS visualisation:** Each GPS fix is drawn as a semi-transparent 20 m circle.
* **Local storage:** The capital and trail are saved to `localStorage`.
* **Known issues:** Tracking could freeze permanently after a single GPS jump of more than 100 m because all subsequent fixes were rejected. Stopping and restarting tracking could also draw a straight line across the gap. No basemap options were available.

### V2: Freeze Fix, Fog of War, Basemap Options

* **Fixed tracking freeze:** A GPS jump of more than 100 m is held as a candidate and only accepted when a second fix confirms it within 60 seconds. A single bad GPS fix can therefore no longer stall tracking permanently.
* **Segmented trail:** Each Start press and each confirmed relocation begins a new line segment. Stopping and restarting, or travelling by bus, no longer draws a straight line between unrelated points. Distance is calculated only from steps within each segment.
* **Fog of war:** Replaced the per-point circles with a full-map dark overlay. A 30 m radius is cleared along the trail and a 120 m radius around the capital.
* **Basemap switch:** Toggle between a street map using CARTO Voyager and satellite imagery using Esri World Imagery.
* **Label toggle:** Show or hide place-name labels independently of the selected basemap.
* **GPS filtering:** Fixes less than 8 m apart are dropped, as are fixes with GPS accuracy worse than 50 m, reducing GPS noise and unnecessary storage.

### V3: Fog Thickness Control, CARTO API Key

* **Fog opacity:** Added a 0–100% opacity slider in 5% increments. The setting is saved between visits and defaults to fully opaque. The slider is disabled when Fog is turned off.
* **CARTO API key:** Added a CARTO API key to the raster tile URLs used by the Street map after CARTO introduced key requirements. The key is supplied client-side for the deployed application and should be restricted to the project's domain.

