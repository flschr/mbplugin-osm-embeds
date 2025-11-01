# Privacy-Friendly OSM Maps for Micro.blog

![Privacy-Friendly Maps hero](docs/hero.svg)

Embed OpenStreetMap views in your Micro.blog posts with optional privacy protection. Readers see a static preview first, then can opt-in to load the interactive map.

## Usage

```markdown
{{< map loc="48.1351,11.5820" >}}
{{< map loc="48.1351,11.5820" zoom="17" >}}
```

## Configuration

Install the plugin and configure optional settings under **Design → Edit Plugins**:

- **API Key**: Add a free [Geoapify](https://www.geoapify.com/) key for static map previews
- **Zoom Level**: Default zoom (0–19, default: 14)
- **Styles & Markers**: Customize appearance in light/dark mode

## Author

Created by **René Fischer**.
