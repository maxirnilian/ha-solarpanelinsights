# Solar Panel Insights

Home Assistant custom integration that calculates detailed solar panel metrics using panel geometry, the built-in [sun](https://www.home-assistant.io/integrations/sun/) integration, and a linked power sensor.

## Features

- Calculates the angle between incoming sunlight and your panel surface
- Estimates absolute plane-of-array irradiation from measured power
- Estimates relative irradiation vs clear-sky potential at the current sun angle
- Uses elevation and azimuth from the built-in `sun.sun` entity
- Configurable panel dimensions, tilt, azimuth, efficiency, and linked power sensor

## Installation

### HACS (recommended)

1. Open **HACS** → **Integrations**
2. Click the three-dot menu → **Custom repositories**
3. Add `https://github.com/maxirnilian/ha-solarpanelinsights` with category **Integration**
4. Search for **Solar Panel Insights**, install, and restart Home Assistant

### Manual

Copy the `custom_components/solar_panel_insights` folder into your Home Assistant `config/custom_components/` directory and restart Home Assistant.

## Configuration

Add the integration via **Settings** → **Devices & services** → **Add integration** → **Solar Panel Insights**.

| Field | Description |
| --- | --- |
| Panel height (mm) | Height of a single panel |
| Panel width (mm) | Width of a single panel |
| Amount of panels | Number of panels in the array |
| Panel tilt (°) | Tilt angle from horizontal (0° = flat, 90° = vertical) |
| Panel azimuth (°) | Compass direction the panels face (180° = south in the northern hemisphere) |
| Efficiency (%) | Panel efficiency percentage |
| Maximum power per panel (Wp) | Rated peak power per panel |
| Input power sensor | Power sensor for your installation |

Settings can be updated later via **Configure** on the integration entry.

## Entities

| Entity | Unit | Description |
| --- | --- | --- |
| Incidence angle | ° | Angle between sunlight and the panel surface |
| Absolute irradiation | W/m² | Effective plane-of-array irradiance implied by measured power |
| Relative irradiation | % | Measured power vs clear-sky potential at the current sun angle |

### Calculations

- **Absolute irradiation:** `P / (A × η)` where `P` is input power (W), `A` is total panel area (m²), and `η` is module efficiency
- **Relative irradiation:** `(P / (P_rated × cos θ)) × 100` where `P_rated` is total rated power (Wp) and `cos θ` is the sun-to-panel-normal geometry factor

Both irradiation sensors are unavailable when the sun is behind the panel (`cos θ ≤ 0`) or required inputs are missing.

## Requirements

- Home Assistant 2023.1.0 or newer
- The [sun](https://www.home-assistant.io/integrations/sun/) integration (installed automatically as a dependency)

## License

MIT — see [LICENSE](LICENSE).
