# Privacy-Friendly Maps for Micro.blog

![Privacy-Friendly Maps hero](docs/hero.svg)

Embed OpenStreetMap views in a Micro.blog post without ever forcing your readers to run JavaScript or leak browsing data. The shortcode renders a progressive enhancement flow: a static preview (optional) with a privacy notice, followed by the official OpenStreetMap iframe once readers opt in.

## Quick Start

1. Install the plugin from Micro.blog and configure the optional Geoapify API key under **Design → Edit Plugins**.
2. Drop the shortcode into any post:

   ```markdown
   {{< map loc="48.1351,11.5820" >}}
   ```

3. Optional: add a custom zoom level (0–19) to highlight a smaller area.

   ```markdown
   {{< map loc="48.1351,11.5820" zoom="17" >}}
   ```

## Parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `loc` | Required. Latitude and longitude separated by a comma (e.g. `48.1351,11.5820`). | – |
| `zoom` | Optional. Zoom level `0` (world) to `19` (buildings). | Site default (`params.default_map_zoom`, defaults to `14`). |

Invalid or missing coordinates trigger a clearly styled error box with guidance.

## Example Output

The flow on a typical Micro.blog page:

1. Static preview image (generated with Geoapify when a key is present) tailored to light/dark mode.
2. Privacy notice overlay with a keyboard-accessible toggle.
3. Lazy-loaded OpenStreetMap iframe with `no-referrer` policy and fullscreen support.

In feeds (RSS/JSON/Atom) the shortcode degrades gracefully and renders only a linked static image or, if no preview key is configured, a simple OpenStreetMap link.

## Testing & Geoapify Style Reference

Use the in-browser playground to assemble shortcodes and preview maps: [`docs/index.html`](docs/index.html).

For the complete list of available map styles, see the [Geoapify Static Maps API documentation](https://www.geoapify.com/static-maps-api/).

## Plugin Settings

All plugin options live under `params` in `plugin.json` and are exposed in Micro.blog's plugin editor:

- `map_preview_api_key` – Optional Geoapify key for static preview images.
- `default_map_zoom` – Fallback zoom level used when the shortcode omits `zoom`.
- `map_preview_style_light`, `map_preview_style_dark` – Static map styles (defaults to `osm-carto`, see Geoapify style catalogue).
- `map_marker_params` – Custom marker parameters in semicolon-separated format (default: `type:awesome;color:red;size:60;shadow:no`). Customize your map markers using Geoapify's [Icon API Playground](https://apidocs.geoapify.com/playground/icon/).
- `show_privacy_notice` – Toggle to hide the privacy overlay text while keeping the interactive toggle.
- `map_privacy_notice_text` – Custom copy for the overlay and accessibility hint.

## Geoapify Setup Guide

1. Create an account at [Geoapify](https://www.geoapify.com/).
2. Generate an API key (the free tier covers 3,000 static map requests/day).
3. Paste the key into the Micro.blog plugin configuration.
4. Optional: customise the light/dark styles using any Geoapify static map style slug. Available styles include:
   - **Raster style**: `osm-carto` (default, classic OpenStreetMap look)
   - **Vector styles** (customizable): `osm-bright`, `osm-bright-grey`, `osm-bright-smooth`, `osm-liberty`, `klokantech-basic`, `positron`, `dark-matter`, `toner`, `toner-grey`

   See the [Geoapify Static Maps API documentation](https://www.geoapify.com/static-maps-api/) for the complete list.

## Custom Markers

You can customize the map markers by adjusting the `map_marker_params` setting. Use the [Geoapify Icon API Playground](https://apidocs.geoapify.com/playground/icon/) to experiment with different marker styles and generate custom parameters.

The format is semicolon-separated key:value pairs, for example:
- `type:awesome;color:red;size:60;shadow:no` (default)
- `type:material;color:blue;size:80;shadow:yes`

Common parameters include:
- `type` – Icon type (`awesome`, `material`, etc.)
- `color` – Marker color (hex color or name like `red`, `blue`)
- `size` – Marker size (numeric value like `60`, `80`)
- `shadow` – Whether to show shadow (`yes` or `no`)

## Zoom Level Cheatsheet

- **0–9**: Continents and countries
- **10–13**: Cities and large regions
- **14–16**: Neighbourhoods (plugin default)
- **17–19**: Streets and individual buildings

## Notes & Best Practices

- The shortcode never injects JavaScript into your site output.
- Static images and iframes both use `loading="lazy"` for performance.
- The OpenStreetMap iframe uses `referrerpolicy="no-referrer"` to minimise data leakage.
- Multiple maps per page share the same inline CSS and receive unique toggle IDs for accessibility.

## Author

Created by **René Fischer**. Contributions and suggestions are welcome via pull request.

## Changelog

- **1.0.0** – Initial release with static previews, privacy overlay, feed-safe output, and browser playground.
