# Custom Base Maps for the Map Component

**Last updated:** 2025-08-28\
**Audience:** Form designers using the CHEFS Map Component\
**Purpose:** Show how to add **custom base map layers** via `availableBaseLayersCustom`, with tested examples and troubleshooting.

---

## Overview

The Map Component supports adding custom base map layers so you can use OpenStreetMap, ESRI imagery, or the BC Government basemap in your forms. Custom layers are defined in the JSON property `availableBaseLayersCustom`.

---

## Configuration Schema

Add entries to the `availableBaseLayersCustom` array. Each entry controls one base layer.

```json
"availableBaseLayersCustom": [
  {
    "label": "",
    "url": "",
    "attribution": "",
    "enabled": true
  }
]
```

### Field Definitions

| Field           | Description                                                                                                | Requirements / Examples                                                                                                                                                                                          |
| --------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **label**       | Name shown in the base map selector dropdown.                                                              | Keep it short and descriptive. Examples: `"ESRI World Imagery"`, `"BC Gov Basemap"`                                                                                                                              |
| **url**         | XYZ tile URL template for fetching tiles. Must include `{z}/{x}/{y}` (or `{z}/{y}/{x}` for some services). | Examples:` ``https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}``https://maps.gov.bc.ca/arcgis/rest/services/province/web_mercator_cache/MapServer/tile/{z}/{y}/{x} ` |
| **attribution** | Required provider credit shown on the map.                                                                 | Examples ESRI: `Tiles © Esri — Source: Esri, Maxar, Earthstar Geographics, and others`BC Gov: `© GeoBC, DataBC, TomTom, © OpenStreetMap contributors`                        |
| **enabled**     | Whether the base map appears by default on load.                                                           | Set the layers to `true` that you wish for your users to be able to switch to or set to `false` if you want to have the configuration available but hide it from the users.                                                                                                                                                        |

---

## Ready‑to‑Use Examples

> You can copy these directly into your form's configuration. Adjust the `enabled` flag (true or false) to show or hide it for the people using your form.

```json
"availableBaseLayersCustom": [
  {
    "label": "ESRI World Imagery",
    "url": "https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}",
    "attribution": "Tiles © Esri — Source: Esri, Maxar, Earthstar Geographics, and the GIS User Community",
    "enabled": true
  },
  {
    "label": "BC Gov Basemap",
    "url": "https://maps.gov.bc.ca/arcgis/rest/services/province/web_mercator_cache/MapServer/tile/{z}/{y}/{x}",
    "attribution": "© GeoBC, DataBC, TomTom, © OpenStreetMap contributors",
    "enabled": true
  }
]
```

---

## Provider Catalogue (Quick Reference)

| Provider                                | URL Template (XYZ)                                                                                   | Attribution                                                             | Notes                                                                                       |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **ESRI World Imagery**                  | `https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}`      | `Tiles © Esri — Source: Esri, Maxar, Earthstar Geographics, and others` | High‑quality satellite imagery. Check Esri terms for usage limits.                          |
| **BC Gov Basemap (Web Mercator Cache)** | `https://maps.gov.bc.ca/arcgis/rest/services/province/web_mercator_cache/MapServer/tile/{z}/{y}/{x}` | `© GeoBC, DataBC, TomTom, © OpenStreetMap contributors`                 | Production endpoint; good coverage for BC.                                                  |

> If you add other providers (e.g., Mapbox, Google), they may require API keys and different URLs. Ensure licensing and attributions are compliant.

---

## Best Practices

- **Always include attribution.** Many providers legally require it.
- **Use official/production endpoints.** Avoid third‑party mirrors that may break or violate terms.
- **Keep labels concise.** Long labels clutter the selector.
- **Enable one default.** Only one `enabled: true` layer is recommended at a time.
- **Test across zoom levels.** Verify at low (z≈3–5), mid (z≈8–12), and high (z≈15–18) zooms.

### Performance & Cost Tips

- Prefer **raster caches** (like the BC Web Mercator Cache) for fast loads and fewer tile requests.
- Consider **tile request throttling** or client‑side caching if embedding on high‑traffic forms.
- If you anticipate heavy traffic, evaluate a **paid/hosted tile service** with SLAs to avoid downtime and rate‑limits.
- For OSM, be a good citizen: keep requests modest; consider a **self‑hosted tile cache** if volume grows (saves money vs. per‑request vendors over time).

---

## Troubleshooting

**Blank map**

- The URL might not be an XYZ tile endpoint. Ensure the path ends with `/tile/{z}/{y}/{x}` (ArcGIS) or includes `{z}/{x}/{y}` (OSM‑style).
- For BC Gov, use the `province/web_mercator_cache` service path on the **production** domain.

**Tiles fail only at certain zoom levels**

- The service may not support those zooms. Try zooms known to be available (e.g., z=0–19 for many caches).
- Check for typos in `{x}/{y}` ordering.

**Slow loading**

- Network/CDN hiccups or rate limits. Try again, or pick a closer endpoint/CDN‑backed service.

**Attribution not showing**

- Ensure the `attribution` field has text and the Map Component is configured to display attributions (it is by default in CHEFS).

---

## Appendix: Custom Base Map Template Syntax

```json
"availableBaseLayersCustom": [
  {
    "label": "<Your Label>",
    "url": "<https://.../{z}/{x}/{y} or /{z}/{y}/{x}>",
    "attribution": "<Required provider credit>",
    "enabled": true
  }
]
```
