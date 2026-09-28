# Streamline Cards
My personal collection of [Streamline Card](https://github.com/brunosabot/streamline-card) templates for Home Assistant Lovelace dashboards.
Each card is defined in its own YAML file under `templates/`. The main `streamline_templates.yaml` simply references them using Streamline's native `!include` support.

## How Templates Work
- `streamline_templates.yaml` maps each template name to its file:
  ```yaml
  homelab_node: !include templates/homelab_node.yaml
  homelab_service: !include templates/homelab_service.yaml
  ```
- Include paths are resolved relative to the main file, so the `templates/` folder must sit next to `streamline_templates.yaml`.
- Variables containing `entity` trigger Home Assistant's entity picker; variables containing `icon` trigger the icon picker.

## Usage / Deployment
1. Copy the whole folder to your Home Assistant configuration directory:
   `/config/www/community/streamline-card/`
   (keep `streamline_templates.yaml` and `templates/` together so `!include` paths resolve).
2. Refresh your browser and clear the cache once so the card re-reads the templates.
3. Reference a template in your dashboard with a `custom:streamline-card` entry.

## Cards
| Card | Purpose |
|---|---|
| [`homelab_node`](#homelab_node) | Node tile with status-aware icon, plus CPU/RAM/disk usage badges |
| [`homelab_service`](#homelab_service) | Service tile with an explicit Online/Offline status badge, plus CPU/RAM/disk usage badges |

### homelab_node
<img src="assets/homelab_node.png" alt="homelab_node screenshot" width="400">

A dashboard tile for a homelab node (e.g. a server or VM). Shows a clickable heading with icon and name that opens a URL. When `status_entity` is `on`, the icon turns green and the card renders at full opacity; when `off`, the icon turns grey and the card dims to 0.4 opacity. CPU, RAM, and disk badges show usage color-coded by threshold (green ≤ 50%, yellow ≤ 70%, orange ≤ 80%, red > 80%).

**Editable variables:**
| Variable | Description |
|---|---|
| `icon` | Heading icon (mdi icon). |
| `name` | Heading text shown on the card. |
| `url` | URL opened when the card is tapped. |
| `status_entity` | Binary entity that controls opacity and icon color (e.g. a ping sensor). |
| `cpu_entity` | Sensor entity for the CPU usage badge. |
| `ram_entity` | Sensor entity for the RAM usage badge. |
| `disk_entity` | Sensor entity for the disk usage badge. |

### homelab_service
<img src="assets/homelab_service.png" alt="homelab_service screenshot" width="400">

A dashboard tile for a homelab service (e.g. a web app or container). Shows a clickable heading with icon and name that opens a URL, plus an explicit Online/Offline status badge driven by `status_entity`. CPU, RAM, and disk badges show usage color-coded by the same thresholds as `homelab_node`. When the service is offline, the card dims to 0.3 opacity.

**Editable variables:**
| Variable | Description |
|---|---|
| `icon` | Heading icon (mdi icon). |
| `name` | Heading text shown on the card. |
| `url` | URL opened when the card is tapped. |
| `status_entity` | Binary entity that drives the Online/Offline badge and card opacity. |
| `cpu_entity` | Sensor entity for the CPU usage badge. |
| `ram_entity` | Sensor entity for the RAM usage badge. |
| `disk_entity` | Sensor entity for the disk usage badge. |