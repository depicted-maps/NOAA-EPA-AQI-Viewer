NOAA Hourly PM₂.₅ Forecast Animation
An independent, browser-based viewer for animating NOAA/National Weather Service hourly PM₂.₅ forecast guidance across the northeastern United States and southern Canada, with an optional contiguous United States view.
The viewer prioritizes scientific accuracy, smooth hourly playback, fixed-location numerical inspection, and geographic consistency. It uses NOAA's operational forecast imagery rather than synthetic or hand-drawn forecast maps.
> **Project status — development / validation prototype (v1.07.0).** This project is **not an official NOAA application**, has not been certified by NOAA, and has not completed end-to-end cartographic or scientific validation. It displays current operational forecasts, **not archived July 15–17, 2026 conditions**.
NOAA references
NOAA OSTI — Air Quality Modeling
NWS National Air Quality Forecast Guidance viewer
NOAA/NWS hourly PM₂.₅ ImageServer
ImageServer service metadata (JSON)
NOAA operational GRIB2 air-quality directory
NOAA's ImageServer metadata identifies the data as numerical hourly average fine particulate matter (PM₂.₅) concentration, in µg/m³. Guidance is issued twice daily from 06Z and 12Z model runs, with hourly guidance covering approximately the following 48 hours. The published image service is time-enabled and offers the NOAA `apm25_color` rendering function.
Features
Authentic NOAA imagery: Displays forecast frames from the time-enabled NOAA/NWS ImageServer using its `apm25_color` renderer.
Hourly animation: Plays available forecast hours in chronological order; does not interpolate invented concentrations or manufacture missing frames.
Two map extents: Northeast (Rhode Island centered) and contiguous United States.
International coverage: Preserves forecast imagery across the U.S.–Canada border where the source service contains data.
Administrative outlines: Optional U.S. state and Canadian provincial/territorial boundaries, projected into the map display and drawn without opaque land fills. Boundary retrieval is dependent on external services.
Click to inspect: Numbers are hidden during playback. Click the map or pause to hold the current frame and request PM₂.₅ values at fixed geographic sample locations. Resume to hide the numbers again.
Playback controls: Load, play/pause, advance one hour, scrub the timeline, and adjust playback interval.
NOAA-style cartography: Retains NOAA's forecast colors, with a dark navy page interface outside the map.
Playing versus paused
Mode	Map behavior
Playing	The NOAA forecast image advances through actual available hourly frames; numerical labels remain hidden.
Paused / inspecting	The frame is fixed and numeric PM₂.₅ values are requested at stationary map coordinates.
Resumed	The values disappear and the hourly animation continues.
The numerical label locations are independent sampling positions, not a verified reproduction of NOAA's exact annotation lattice. Each displayed number must come from the NOAA service for the selected time; unsuccessful requests remain blank. Numbers represent model forecasts, not observations or EPA AQI values.
Getting started
Download or clone the repository.
Open `NOAA_PM25_Forecast_v1.07.0_Canada_Outline_Only.html` in a modern browser (Chrome or Edge), or rename that file to `index.html` to serve it as the site's home page.
Choose Map coverage and Frames, then select Load NOAA frames.
Select Play to animate. Click the map to pause and reveal stationary values; click again to resume.
Use the timeline slider and playback interval selector to inspect individual forecast hours.
An internet connection is required. Browser security settings may restrict remote requests from an HTML file opened using `file://`. For more reliable operation, host the HTML on GitHub Pages or serve it locally:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000/` and select the HTML filename if it has not been renamed to `index.html`.
GitHub Pages
The viewer is a self-contained HTML application but depends on live external NOAA and boundary services.
Place the HTML file in the repository root and rename a copy to `index.html`.
In Settings → Pages, configure deployment from the intended branch and root folder (or use a Pages workflow).
Open the URL GitHub Pages provides. The forecast depends on live NOAA service availability and browser access permissions.
GitHub Pages hosts the viewer; it does not store, backfill, or archive NOAA forecast data.
Data, projection, and accuracy
Property	Implementation
Variable	Hourly mean forecast PM₂.₅ concentration
Units	Micrograms per cubic meter (`µg/m³`)
Forecast source	NOAA/NWS NDGD PM₂.₅ ImageServer
Source image renderer	`apm25_color`
Display projection	Web Mercator, EPSG:3857 (NOAA service metadata also reports WKID 102100)
Native atmospheric-model grid	Separate from the published map; not recreated by this viewer
Forecast timing	Service-advertised valid times; current operational forecast
Geographic overlays	Independently retrieved U.S. and Canadian boundary geometry
Numeric labels	Fixed-position queries for the selected valid time; blank on failed/no-data query
Projection matters: NOAA's published service advertises EPSG:3857. The animation requests forecast imagery and positions boundaries against a common projected display extent. This is distinct from the atmospheric and chemical model's computational grid, which may use a different projection and resolution. Requesting a shared map projection is necessary for alignment, but does not itself certify positional or scientific accuracy.
Canadian data versus Canadian boundaries: The NOAA forecast is allowed to extend north of the border. Administrative overlay layers are outlines only, not land-colored basemaps; if a boundary service fails, the weather field should remain visible without replacement or invented data.
Validation status
Test	Status
NOAA's official PM₂.₅ ImageServer and units identified	Confirmed from NOAA service metadata
NOAA `apm25_color` raster function advertised	Confirmed from NOAA service metadata
Published service Web Mercator spatial reference	Confirmed from NOAA service metadata
Source HTML and projection/interaction logic incorporated	Implemented in v1.07.0
Full browser playback against a live forecast	Not certified
U.S. state and Canadian provincial overlay alignment	Not certified
All paused numerical values versus source forecast rasters	Not certified
Frame-by-frame visual equivalence to NOAA's original website	Not certified
Archived July 15–17, 2026 forecast support	Not implemented; archive not verified
For formal validation, check representative forecast valid times, compare returned raster values against NOAA's own source, inspect border/coastline alignment at multiple zooms and extents, and confirm that frame order contains no unexpected gaps or duplicates. Document any deviations before publishing the viewer as a validated GIS product.
Limitations and responsible interpretation
PM₂.₅ concentration is not the Air Quality Index (AQI). The viewer does not compute or display EPA AQI categories.
Forecast concentrations are model guidance, not verified measurements at ground monitoring stations.
The NOAA operational service refreshes; it is not a persistent historical archive. Historical July 2026 replay will require archived geospatial data verified for the requested dates and hours.
Playback smoothness depends on network conditions and successful download of frames. No scientific interpolation is introduced solely for visual smoothness.
Numeric sample positions approximate NOAA's labeling style but are not guaranteed to equal the coordinates NOAA uses for its map annotations.
Boundary geometry may originate from separately hosted geospatial sources and has not been fully certified against NOAA's map.
This application requires network availability, and remote servers may impose access limits or cross-origin restrictions.
Source attribution and disclaimer
Forecast data: National Oceanic and Atmospheric Administration (NOAA), National Weather Service (NWS).
Application: Independently developed demonstration; not produced, sponsored, validated, or endorsed by NOAA or NWS. All forecast values and colors are intended to originate from NOAA's published services. Third-party boundary data have their own source terms and attribution requirements.
For authoritative forecast context, model documentation, and the original presentation, refer to NOAA OSTI Air Quality Modeling and the NWS Air Quality Forecast Guidance viewer.
Next milestone
Complete independent validation of the operational viewer, especially the boundary overlays and stationary PM₂.₅ values. After validation, research and verify a suitable archive for July 15–17, 2026, and adapt the same animation controls to genuine archived forecast frames without changing their scientific meaning.
