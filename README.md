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

1. Open `http://localhost:8000/sand_dunes.html` in a modern browser (Chrome, Firefox, Edge, or Safari)
2. Click anywhere to lock the pointer and start exploring
3. Use the controls below to navigate, and the top-right panel to tweak the scene

### Controls

- **WASD** - Move around
- **Mouse** - Look around
- **Space** - Toggle between Walk and Fly modes
- **Shift** - Sprint (move faster)
- **Q** - Move up (Fly mode only)
- **E** - Move down (Fly mode only)
- **R** - Regenerate a new dune landscape
- **Esc** - Release pointer lock

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
