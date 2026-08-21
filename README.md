# Coastal Sand Dunes Explorer

A realistic, interactive 3D coastal sand-dune landscape built with Three.js. It features procedurally generated, wind-shaped dunes, physically-based sky and sun, reflective animated water, and a live control panel.

## Features

- **Realistic procedural dunes** using Perlin noise (FBM + domain warping) with wind-aligned ridged crests for natural, non-repeating dune fields
- **Physically-based sky & sun** (Rayleigh/Mie scattering) with an adjustable time of day
- **Image-based lighting** — the sky is baked into an environment map so the sand is lit by the sky
- **Reflective, animated ocean** with sun glints and wind-driven waves
- **Realistic sand shading** — colors vary by height, slope, and moisture (wet sand at the shoreline, bright crests, shadowed lee faces), plus a procedural wind-ripple normal map
- **Coastal island taper** so the dunes descend into the surrounding sea
- **Live control panel** to change sun position, wind, exposure, and regenerate the terrain
- **First-person navigation** with walk and fly modes, ACES tone mapping, and soft shadows

## How to Use

The app uses ES modules and an import map, so it must be served over HTTP (opening the file directly via `file://` will not work).

**On your phone (GitHub Pages):** after Pages is enabled, open
[https://jawhiting.github.io/coastal-sand-dunes/](https://jawhiting.github.io/coastal-sand-dunes/).

```bash
# From the repository root
python3 -m http.server 8000
# then open http://localhost:8000/sand_dunes.html
```

In a Cursor Cloud Agent this server starts automatically (see `.cursor/environment.json`).

1. Open `http://localhost:8000/sand_dunes.html` in a modern browser (Chrome, Firefox, Edge, Safari, or the Meta Quest Browser)
2. Click anywhere to lock the pointer and start exploring, or tap **ENTER VR** on a headset
3. Use the controls below to navigate, and the top-right panel to tweak the scene

### Controls

- **WASD** - Move around
- **Mouse** - Look around
- **Space** - Toggle between Walk and Fly modes
- **Shift** - Sprint (move faster)
- **Q** - Move up (Fly mode only)
- **E** - Move down (Fly mode only)
- **R** - Regenerate a new dune landscape
- **F** or hold **left mouse** - Fire the sand gun (build a dune)
- **G** or hold **right mouse** - Dig sand away
- **C** / **V** - Cycle sand colour forward / back
- **Esc** - Release pointer lock

### Meta Quest / WebXR

Quest Browser (and other WebXR headsets) can enter true stereoscopic VR. This uses the current **WebXR** standard — the older WebVR API is retired and is not needed.

1. Open the page over **HTTPS** (GitHub Pages) or localhost. WebXR will not start on plain `http://` LAN IPs.
2. Tap **ENTER VR** at the bottom of the page (the Quest Browser will ask to start an immersive session).
3. Look around by turning your head. Controllers are shown in-world.

| Control | Action |
| --- | --- |
| Left thumbstick | Move |
| Right thumbstick left/right | Snap-turn 30° |
| Right thumbstick up/down | Fly up/down (Fly mode) |
| Right trigger | Sand gun (build or dig, per the panel) |
| Grip / squeeze | Sprint |
| A / X | Toggle Walk / Fly |
| B / Y | Cycle sand colour |

Walk mode follows the dune surface; Fly mode is free 3D movement. Shadows and mesh density are reduced automatically on Quest so stereo rendering stays smoother.

### Sand gun (sculpt the dunes)

You can change the landscape while you are in it. A height-field brush raises or lowers nearby terrain vertices where a stream of sand grains lands, then updates local lighting and sand color.

- **Desktop:** enter the scene, aim with the mouse, hold **F** or the left mouse button to spray. Hold **G** or the right mouse button to dig. Press **C** or **V** (or use the Colour dropdown) to cycle Gold, Ivory, Red, Black, Pink, Moss, Ocean, and Violet. That colour tints both the grain stream and the vertices that the brush moves.
- The **Sand gun** folder also has Build/Dig, radius, flow, and **Spray 2.5s (from camera)**.
- **Quest:** hold the **right trigger** to fire from the in-hand sand gun. Grip is sprint so you can still move quickly while building.

Built-up sand can make an existing ridge taller or raise a new mound, including out of the shallows. **R** / Regenerate resets the island.

### Control panel (top-right)

- **Time of day** — sun elevation, sun azimuth, and exposure
- **Wind & sand** — wind direction and strength (reshapes dunes on regenerate, drives ripples and waves)
- **Scene** — toggle the ocean, wireframe, and regenerate the dunes
- **Navigation** — switch Walk/Fly and adjust move speed

## Technical Details

- **Terrain Size**: 3000x3000 units, 384x384 segments
- **Ocean**: 30000x30000 reflective water plane at sea level (y=0)
- **Height Range**: roughly 0-300 units, tapering below sea level at the coast
- **Noise**: `ImprovedNoise` (Perlin) with FBM, domain warping, and ridged multifractal crests
- **Rendering**: ACES filmic tone mapping, PCF soft shadows, PMREM sky environment
- **Built with**: Three.js r160 (`Sky`, `Water`, `ImprovedNoise`, `lil-gui` add-ons via CDN)

## How It Works

### Terrain generation
- Multi-octave Perlin FBM for the rolling base terrain
- Domain warping to break up regularity and add organic shapes
- Ridged multifractal noise sampled in wind-aligned coordinates to form long dune crests that run across the wind
- Circular coastal gradient that lowers the terrain below sea level toward the edges

### Sand shading
- Per-vertex colors blended from wet sand, beach, dry sand, bright crest, and shadowed lee tones based on height and slope
- A procedurally generated ripple normal map, rotated to match the wind direction

### Sky, sun & water
- `Sky` provides atmospheric scattering; the sun vector drives the directional light, water sun direction, fog color, and environment map
- `Water` renders live reflections with animated normals whose distortion scales with wind strength

## Development

This project is a single self-contained file (`sand_dunes.html`) that loads Three.js and its add-ons from a CDN. See `CHAT_HISTORY.md` for the original development conversation.

## License

This project is open source and available for educational and personal use.
