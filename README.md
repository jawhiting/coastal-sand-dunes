# Coastal Sand Dunes Explorer

A realistic 3D coastal sand dunes environment built with Three.js, featuring dramatic height variations and an animated ocean.

## Features

- **Massive procedurally generated sand dunes** with extreme height variance (0-300+ units)
- **Coastal environment** with dunes tapering down to meet the ocean
- **Animated ocean** with realistic wave motion
- **First-person controls** with walk and fly modes
- **Dynamic lighting** with shadows and atmospheric fog
- **Realistic sand materials** with color variation

## How to Use

1. Open `sand_dunes.html` in a modern web browser (Chrome, Firefox, Edge, or Safari)
2. Click anywhere to lock the pointer and start exploring
3. Use the controls to navigate:

### Controls

- **WASD** - Move around
- **Mouse** - Look around
- **Space** - Toggle between Walk and Fly modes
- **Shift** - Move faster
- **Q** - Move up (Fly mode only)
- **E** - Move down (Fly mode only)
- **Esc** - Release pointer lock

## Technical Details

- **Terrain Size**: 3000x3000 units
- **Ocean Size**: 6000x6000 units
- **Terrain Resolution**: 300x300 segments
- **Height Range**: 0-300+ units
- **Built with**: Three.js r160

## Features Overview

### Terrain Generation
- Multi-octave noise for natural variation
- Dramatic dune formations with multiple wave patterns
- Sharp ridges for towering peaks
- Mega-dunes for large-scale landscape features
- Coastal gradient that tapers dunes to beach level at edges

### Coastal Environment
- Sea level at y=0
- Animated ocean with multi-directional wave motion
- Coastal fog with blue-grey haze
- Semi-transparent water with metallic reflections

### Navigation
- Fly mode: Free 3D movement
- Walk mode: Automatically follows terrain surface
- Boundary checking to keep player within terrain area
- Real-time position debug display

## Development

This project was created with assistance from Claude (Anthropic). See `CHAT_HISTORY.md` for the full development conversation and Claude state that can be used to resume development.

## License

This project is open source and available for educational and personal use.
