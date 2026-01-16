IMPORTANT: This is a public repository for the Geo-JSON Plugin for Fylr. Use the instructions below to install the plugin in your Fylr instance. Dont use the release section of this repository as its outdated and is not used for distribution any more.

# Geo-JSON Plugin for Fylr

This plugin enables support for the GeoJSON format within the Fylr application. It provides views and editors for fields of type GeoJSON, along with additional utilities to work with geographic data.

---

## Disclaimer

This plugin is actively maintained, there may still be bugs or unexpected behavior.

We welcome all feedback, suggestions, and issue reports as we continue improving the plugin. Thank you for your support!

---

## Installation

1. **Via ZIP:**
   - Download the latest version from [this link](https://programmfabrik.github.io/fylr-plugin-geo-json/fylr-plugin-geo-json-618be833-e568-4198-9132-29a90eb3803d-latest.zip).
   - Use the Plugin Manager in Fylr to install the downloaded plugin package.

2. **Via URL:**
   - Use the following URL to install the plugin and **receive automatic updates** in your instance:  
     [https://programmfabrik.github.io/fylr-plugin-geo-json/fylr-plugin-geo-json-618be833-e568-4198-9132-29a90eb3803d-latest.zip](https://programmfabrik.github.io/fylr-plugin-geo-json/fylr-plugin-geo-json-618be833-e568-4198-9132-29a90eb3803d-latest.zip)
     
---

## Licensed vs Unlicensed Version

This plugin operates in two modes depending on the capabilities of your Fylr instance. If your instance includes a valid license with the `geo_support` feature enabled, all plugin functionalities will be available. Otherwise, the plugin will run in basic mode with limited features.

From the Fylr API’s perspective, the differences between having a license and not are:
- **Read & write operations** for geo-json columns are available in basic mode.
- **Search operations** for geo-json columns are available only in licensed mode.

### Features Available Without `geo_support`

- **Geo-JSON Columns**: You can use geo-json columns to add geographic points on the map. An interactive map will be displayed allowing you to place a single point. However, lines and shapes cannot be added interactively through the map editor in this mode.
- **Data Display**: While you can store detailed geo-json data in the column, the interactive map will only support point-based editing.
- **Detail Map**: The detail map will still be visible and will render all available geo-json data.
- **Map Search Manager**: This feature will be disabled, as it requires geo-data search capabilities provided only by instances with `geo_support`.

### Additional Features with `geo_support` Enabled

- **Map Editor Enhancements**: The editor will support both individual features and feature collections.
- **Supported Geometry Types**: Points, lines, and polygons can be added and edited interactively.
- **Geocoder Tool**: You will be able to search for real-world locations and generate geographic data using the integrated geocoder.
- **Expert Search**: Enables advanced searching using geo-data criteria.
- **Search Manager Integration**: The geo-based search manager will be available in the main search interface.

---

## Getting Started

Once installed, Fylr will automatically use this plugin to render fields of type `geographic`.  
Additionally, it adds functionality for filtering and searching records using geo-data.

### Detail View

- Fields of type `GeoJSON` will display all included geographic components (known as "features").
- Features are shown as a list for easy navigation and inspection.
- The detail view can display a map with all available features in the currently opened record. This includes:
  - Assets with geo metadata
  - Geo-JSON fields
  - Custom data types that support the geo standard

### Editor View

- Users can create and edit features interactively using the built-in map editor.
- The GeoJSON input field supports several text formats, which are automatically parsed:
  - Latitude and longitude coordinates, e.g., `lat:23.423, lon:32.423`
  - Direct Google Maps links:  
    - If the link refers to a "place", it will be used as the name of the point.  
    - If not, the center of the linked map will be used as the point location.
  - Raw GeoJSON data can also be pasted directly into the text field. The field will parse it and prompt the user to import the data.
- Additionally, through the field’s schema options in the data model, you can:
  - Restrict which types of features are supported in the map
  - Limit the field to accept only one feature, if desired

### Expert Search

This plugin enables geographic record searches via the `geo-json` column in Fylr’s expert search. Available options include:

- Searching for all records within a custom area drawn on the map
- Searching for records inside a circle defined by the user on the map
- Searching using a defined point and radius
- Searching within real-world areas using geo-coding  
  _Example: Find all records located within the area defined by "Berlin"._

### Additional Functionality

- A new button, **"Show Map"**, will appear in the main search interface.
- Clicking this button opens the **Map Search Manager**, allowing users to filter the current search using an interactive map.

  ---

## Map Editor

The map editor is a powerful tool included with this plugin that allows users to create GeoJSON data interactively. The types of features currently supported are:

- **Points:** Draw geographic points on the map; each point is a separate feature.
- **Lines:** Draw lines interactively. Press `Enter` once the line is complete.
- **Areas:** Create areas by selecting points on the map. After closing an area, you can edit its points. Press `Enter` when finished.
- **Geocoder:** Use this utility to search for real-world locations and add them directly to the map. Please use this feature with caution—some features like areas can generate a large amount of geometric data. We are still fine-tuning this functionality.

Once features are created, they appear in a list in the right-hand panel. From here, users can edit the GeoJSON content by adding or removing features.

Additionally, users can:

- Select a feature and assign it a custom name.
- Use the reverse geocoding option to attempt to retrieve the real-world name of the location.

> Note: The language used for reverse geocoding will be the first language configured in your `db-locale` settings.

---

## Map Search Manager

The Map Search Manager, introduces a new way to filter and explore search results using geographic data.

- This functionality can be activated via the **"Show Map"** button located next to the **"Filter"** button in the main search interface.
- When activated, an interactive map appears alongside the search results, displaying all objects that have `geo-standard` configured.
- The search results will be filtered based on the visible area in the map. This means that zooming or panning in the map will dynamically update the results to show only the objects located within the visible region.

This provides a powerful and intuitive way to navigate and narrow down search results using spatial information.

## Custom Map Configuration

This plugin supports the [Mapbox Style Specification](https://docs.mapbox.com/style-spec/guides/), which allows you to fully define the visual appearance of maps.  
Using this specification, you can add custom tiles or even vector data to create highly customized map styles. Custom maps can be configured in the config panel of the geo-json plugin. Additionally, any custom map can be set as the **default map**, ensuring it is loaded by default in all map views.

---

### Example: Using Mapbox Tiles

You can configure a Mapbox style by providing the following JSON in the **Value** field of the custom maps configuration:

```json
{
  "properties": {
    "accessToken": "<your_api_key>"
  },
  "url": "mapbox://styles/mapbox/satellite-streets-v12"
}
```

This will enable the use of the **satellite-streets-v12** map style across the application.  

---

### Basic Example: Custom Style with OSM Tiles

The following example shows how to define a custom style using free OpenStreetMap tiles:

```json
{
  "version": 8,
  "name": "OSM Free Style",
  "sources": {
    "osm-tiles": {
      "type": "raster",
      "tiles": [
        "https://tile.openstreetmap.org/{z}/{x}/{y}.png"
      ],
      "tileSize": 256,
      "attribution": "© OpenStreetMap contributors"
    }
  },
  "layers": [
    {
      "id": "osm-background",
      "type": "raster",
      "source": "osm-tiles",
      "minzoom": 0,
      "maxzoom": 19
    }
  ]
}
```

---

### Example with Custom Shapes

Custom shapes allow you to draw additional layers on the map.  
Unlike dynamic data, these shapes become part of the map style itself, making them useful for highlighting areas or regions.  

In this example, we define polygon layers for **Comunidad de Madrid** and **Cataluña**:

```json
{
  "version": 8,
  "name": "OSM Free with Polygons",
  "sources": {
    "osm-tiles": {
      "type": "raster",
      "tiles": [
        "https://tile.openstreetmap.org/{z}/{x}/{y}.png"
      ],
      "tileSize": 256,
      "attribution": "© OpenStreetMap contributors"
    },
    "regions": {
      "type": "geojson",
      "data": {
        "type": "FeatureCollection",
        "features": [
          {
            "type": "Feature",
            "properties": { "name": "Comunidad de Madrid" },
            "geometry": {
              "type": "Polygon",
              "coordinates": [
                [
                  [-4.6, 41.2],
                  [-3.0, 41.2],
                  [-3.0, 39.9],
                  [-4.6, 39.9],
                  [-4.6, 41.2]
                ]
              ]
            }
          },
          {
            "type": "Feature",
            "properties": { "name": "Cataluña" },
            "geometry": {
              "type": "Polygon",
              "coordinates": [
                [
                  [0.0, 42.9],
                  [3.5, 42.9],
                  [3.5, 40.9],
                  [0.0, 40.9],
                  [0.0, 42.9]
                ]
              ]
            }
          }
        ]
      }
    }
  },
  "layers": [
    {
      "id": "osm-background",
      "type": "raster",
      "source": "osm-tiles",
      "minzoom": 0,
      "maxzoom": 19
    },
    {
      "id": "regions-fill",
      "type": "fill",
      "source": "regions",
      "paint": {
        "fill-color": "#ff6600",
        "fill-opacity": 0.4
      }
    },
    {
      "id": "regions-outline",
      "type": "line",
      "source": "regions",
      "paint": {
        "line-color": "#ff0000",
        "line-width": 2
      }
    },
    {
      "id": "regions-labels",
      "type": "symbol",
      "source": "regions",
      "layout": {
        "text-field": "{name}",
        "text-font": ["Open Sans Regular"],
        "text-offset": [0, 1.2],
        "text-anchor": "top"
      },
      "paint": {
        "text-color": "#000000",
        "text-halo-color": "#ffffff",
        "text-halo-width": 1
      }
    }
  ]
}
```


---

Enjoy working with geographic data in Fylr!

---

