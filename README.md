# Geo-JSON Plugin for Fylr

This plugin enables support for the GeoJSON format within the Fylr application. It provides views and editors for fields of type GeoJSON, along with additional utilities to work with geographic data.

---

## Disclaimer

This plugin is actively maintained, there may still be bugs or unexpected behavior.

We welcome all feedback, suggestions, and issue reports as we continue improving the plugin. Thank you for your support!

---

## Installation

1. **Via ZIP:**
   - Download the latest version from [this link](https://github.com/programmfabrik/fylr-plugin-geo-json-public/releases/latest/download/geo-json.zip).
   - Use the Plugin Manager in Fylr to install the downloaded plugin package.

2. **Via URL:**
   - Use the following URL to install the plugin and **receive automatic updates** in your instance:  
     [https://github.com/programmfabrik/fylr-plugin-geo-json-public/releases/latest/download/geo-json.zip](https://github.com/programmfabrik/fylr-plugin-geo-json-public/releases/latest/download/geo-json.zip)
     
---

## Licensed vs Unlicensed Version

This plugin operates in two modes depending on the capabilities of your Fylr instance. If your instance includes a valid license with the `geo_support` feature enabled, all plugin functionalities will be available. Otherwise, the plugin will run in basic mode with limited features.

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

---

Enjoy working with geographic data in Fylr!

---

