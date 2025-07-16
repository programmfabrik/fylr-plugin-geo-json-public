# Geo-JSON Plugin for Fylr

This plugin enables support for the GeoJSON format within the Fylr application. It provides views and editors for fields of type GeoJSON, along with additional utilities to work with geographic data.

---

## Disclaimer

This plugin is actively maintained, there may still be bugs or unexpected behavior.

We welcome all feedback, suggestions, and issue reports as we continue improving the plugin. Thank you for your support!

---

## Installation

1. **Via Releases Page:**

   - Download the latest version from the [Releases](./releases) page.
   - Use the Plugin Manager in Fylr to install the downloaded plugin package.

---

## Getting Started

Once installed, Fylr will automatically use this plugin to render fields of type `geographic`.

### Detail View

- Fields of type GeoJSON will display all included geographic components (called "features").
- Features will be shown as a list for easy navigation and inspection.

### Editor View

- Users will be able to create and edit features interactively using the built-in map editor.

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

## Search Manager

The Search Manager, also known as the Map Companion, introduces a new way to filter and explore search results using geographic data.

- This functionality can be activated via the **"Show Map"** button located next to the **"Filter"** button in the main search interface.
- When activated, an interactive map appears alongside the search results, displaying all objects that have `geo-standard` configured.
- The search results will be filtered based on the visible area in the map. This means that zooming or panning in the map will dynamically update the results to show only the objects located within the visible region.

This provides a powerful and intuitive way to navigate and narrow down search results using spatial information.

---

Enjoy working with geographic data in Fylr!

---

