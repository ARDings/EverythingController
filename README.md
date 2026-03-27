# EverythingController

Hosted: https://xrchris.com/webxr/evc.html

A single-file WebXR Mixed Reality experience that turns your body into a controller — no app download, no install, runs directly in the browser.

Spheres spawn in your physical space. Use your feet and hands to hit them using real depth-sensor data as collision geometry.

---

## Live Demo

Open `evc.html` in a WebXR-capable browser (e.g. Galaxy XR) and tap **Enter XR**.

---

## How It Works

EverythingController uses the **WebXR Depth Sensing API** to reconstruct your physical environment as a live 30×30 point cloud every frame. Each point is tested against all active targets as a physical collider — what you see is exactly what collides. No controller needed.

```
Depth Sensor → 3D Point Cloud → Per-Frame Collision → Hit Detection → 8-bit Sound
```

---

## Game Modes

| Mode | Description |
|------|-------------|
| **Air** | Spheres float at kick height. Hit them with your foot. |
| **Defense** | Spheres fly toward you from a distance. Deflect them. |

Switch modes via the in-world panel.

---

## Settings Panel

All settings are adjustable live inside the XR environment via the floating panel.

| Setting | Description | Default |
|---------|-------------|---------|
| **Cam Offset X** | Horizontal correction for depth sensor misalignment | -20 cm |
| **Floor Filter** | Ignore depth points below this height (removes floor noise) | 8 cm |
| **Hit Radius** | Extra collision radius added around each sphere | 10 cm |
| **Ground Offset** | Vertical position of the shadow-receiving ground plane | -20 cm |
| **Cube Size** | Size of each debug/occlusion cube (smaller = more detail) | 5 cm |
| **Debug** | Visualize the depth point cloud as colored cubes (green = leg, red = floor) | OFF |
| **Occlusion** | Apply occlusion material to depth cubes — virtual objects disappear behind real ones | OFF |

---

## Debug & Occlusion

### Debug Mode
Renders the live depth point cloud as small colored cubes:
- **Green** — above floor threshold (active collider)
- **Red** — below floor threshold (ignored)

### Occlusion Mode
Applies a depth-write-only material to the point cloud mesh. Virtual content positioned behind real-world geometry is occluded correctly — the cubes are invisible but block the renderer's depth buffer.

### Cube Size & Detail
Reducing cube size automatically increases grid density (up to 120×120 = 14,400 points) for higher spatial resolution near close objects. Minimum size: 0.1 cm.

| Cube Size | Grid | Points |
|-----------|------|--------|
| 5 cm | 30×30 | 900 |
| 2 cm | 75×75 | 5,625 |
| 1 cm | 120×120 | 14,400 |
| 0.1 cm | 120×120 | 14,400 (cap) |

---

## Tech Stack

| Library | Version | Role |
|---------|---------|------|
| [Three.js](https://threejs.org) | 0.182.0 | 3D rendering |
| [XR Blocks](https://github.com/xrblocks) | 0.11.0 | WebXR framework, Spatial UI, Depth API |
| [Troika Three Text](https://github.com/protectwise/troika) | latest | 3D text rendering |

All dependencies are loaded via CDN — no build step required.

---

## Requirements

- A WebXR-capable headset with **depth sensing support** (e.g. Meta Quest 3)
- Meta Quest Browser or equivalent
- No installation, no server needed — serve the single HTML file

---

## Project Structure

```
webxr/
└── evc.html    # Entire app — self-contained single file
```

---

## Author

**XRChris** — building WebXR experiences one file at a time.
