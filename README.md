# NOAA Hourly PM₂.₅ Forecast Animation

**Interactive NOAA/NWS forecast guidance for the northeastern United States and southern Canada.**  
Current operational forecast · Hourly modeled PM₂.₅ concentrations (µg/m³) · Independent viewer

**[Open the animated forecast viewer](https://depicted-maps.github.io/NOAA-EPA-AQI-Viewer/)**

## Overview

This project animates **actual hourly NOAA/National Weather Service PM₂.₅ model forecast imagery** using NOAA's time-enabled image service. The northeastern view is centered near Rhode Island, and a broader contiguous U.S. view is also available. Where the NOAA raster includes Canadian territory, its modeled values are displayed across the international border.

> **Scientific distinction:** This is a **PM₂.₅ concentration forecast**, measured in **micrograms per cubic meter (µg/m³)**. It is **not EPA Air Quality Index (AQI)** and is **not a ground-monitor observation**. The current viewer does not replay July 2026 archived forecasts.

## How to use the viewer

1. Open the [live viewer](https://depicted-maps.github.io/NOAA-EPA-AQI-Viewer/).
2. Wait while the latest available NOAA hourly frames load; the animation starts automatically.
3. **Click the map to pause.** Geographically fixed numerical PM₂.₅ values are requested for that forecast hour.
4. **Click again to resume.** Numeric labels disappear while the forecast animates.
5. Use the region, frame count, speed, timeline, or **Next hour** controls for a more detailed look.

### Display behavior

| Mode | Behavior |
| --- | --- |
| Playing | Actual NOAA hourly raster images animate; numerical values are hidden. |
| Paused | The current frame remains still; PM₂.₅ values appear at stationary locations as the source responds. |
| Resumed | Numbers disappear; hourly animation continues. |

## Data and geographic reference

| Element | Source or specification |
| --- | --- |
| Forecast variable | Hourly mean PM₂.₅ concentration |
| Units | µg/m³ |
| Forecast imagery | [NOAA/NWS PM₂.₅ ImageServer](https://mapservices.weather.noaa.gov/raster/rest/services/air_quality/ndgd_apm25_hr01/ImageServer) |
| Forecast colors | NOAA image service `apm25_color` function |
| Published display projection | Web Mercator (EPSG:3857 / WKID 102100) |
| Model calculation grid | Separate from the projected web display; not reconstructed here |
| Boundaries | U.S. state / Canadian provincial outlines requested from external services; still subject to geographic validation |
| Valid times | Forecast hours advertised by NOAA's current operational service |

The viewer uses the NOAA service's existing colors and displays available hourly frames without inventing intermediate forecasts. Sample values use fixed geographic positions; these positions **have not been verified as NOAA's exact annotation locations**.

## Use in ArcGIS StoryMaps

In **ArcGIS StoryMaps**, add an **Embed** block and paste:

`https://depicted-maps.github.io/NOAA-EPA-AQI-Viewer/`

Use the **interactive** website option, not a static image preview. Allow enough height to show the controls and map. The viewer uses live NOAA services and requires a network connection. The embedded version starts the animation after its forecast frames have loaded, subject to browser and service availability.

## Publish with GitHub Pages

- Keep **`index.html`** and **`README.md`** in the root of the `main` branch.
- In **Settings → Pages**, select **Deploy from a branch → main → /(root)**.
- After publication, the application URL is `https://depicted-maps.github.io/NOAA-EPA-AQI-Viewer/`.

For updates, **upload `README.md` as a file** rather than pasting the entire document into one line of GitHub's web editor. GitHub displays Markdown correctly when its line breaks, headings (`##`), and tables are preserved.

## Official NOAA references

- [NOAA OSTI — Air Quality Modeling](https://vlab.noaa.gov/web/osti-modeling/air-quality)
- [NWS National Air Quality Forecast Guidance](https://airquality.weather.gov/?element=apm25h01&mapcenter=-72.66%2C42.65&mapzoom=6.63570673334827&subregion=CONUS&region=CONUS)
- [NOAA PM₂.₅ service metadata](https://mapservices.weather.noaa.gov/raster/rest/services/air_quality/ndgd_apm25_hr01/ImageServer?f=pjson)

## Validation and limitations

**Status: development / validation prototype (v1.08.0).** The JavaScript viewer implements official NOAA image requests, an hourly playback sequence, and fixed-location value inspection. The following require further live testing: completeness of the operational hourly series; raster-value agreement for selected frames; exact U.S. and Canada boundary alignment; and visual comparison against NOAA's official viewer. Availability of Canadian outlines depends on their source service.

This repository is **independently developed** and is **not an official NOAA application** or an EPA AQI product. Forecast source credit: **NOAA / National Weather Service**. Historical July 15–17, 2026 replay would require independently verified archived model data.
