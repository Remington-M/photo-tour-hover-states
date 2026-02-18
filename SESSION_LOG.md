# Photo Tour Hover States - Session Log
**Date:** February 18, 2026
**Project:** Interactive hover state prototype for photo gallery grids

## Overview
Built an interactive desktop prototype to test and refine different hover effects for a photo tour masonry grid layout. The prototype includes 5 distinct hover states with a comprehensive dev panel for real-time parameter adjustments.

## Files Created
- `photo-tour-prototype.html` - Complete standalone prototype with all hover effects and dev tools

## Features Implemented

### 1. Simple Scrim (Current Design)
- Dark overlay on hover
- Adjustable color, opacity, duration, and easing

### 2. Subtle Zoom
- 1% scale increase on hover (adjustable 1.0-1.2x)
- Smooth animation with configurable easing
- Very subtle motion enhancement

### 3. Expand Border Radius
- Changes border radius from 32px → 56px on hover
- Creates a morphing effect
- Both default and hover radius are adjustable

### 4. Lighting Effect (Mouse Follow)
- Radial spotlight that tracks mouse position
- Adjustable glow size (100-800px)
- Three-stage gradient with configurable opacities
- Multiple blend modes available (overlay, screen, soft-light, etc.)
- Mid-point and fade-out stops controllable

### 5. 3D Tilt with Edge Lighting (Most Complex)
- **3D Tilt:**
  - Perspective-based rotation following mouse position
  - Max rotation: 0-15° (default: 2.5°)
  - Adjustable perspective depth (500-2000px)
  - Spring-based easing for natural motion

- **Edge Lighting (Bevel/Emboss Effect):**
  - Dual-layer lighting system (::before and ::after pseudo-elements)
  - Directional gradients that rotate with tilt angle
  - Inset box shadows for depth
  - **Adjustable parameters:**
    - Intensity (0-1.5): Overall brightness
    - Width (5-40%): How far edge extends from border
    - Sharpness (0-50px): Blur radius for crisp vs soft edges
    - Falloff (10-60%): Gradient fade distance
  - Light source appears to follow tilt direction
  - Shadow/highlight positioning calculated from mouse delta

## Dev Panel Features

### Design
- Floating circular toggle button (⚙️) in bottom right
- Collapsible panel with glassmorphism effect
- 360px width, max 70vh height with scrolling
- Dark theme with semi-transparent backdrop blur

### Controls
- **Dual input system:** Sliders + manual number inputs for precision
- **Real-time updates:** All changes apply instantly
- **Panel switching:** Automatically shows relevant controls per hover style
- **Keyboard shortcuts:**
  - `D` to toggle panel
  - `Escape` to close
- **Copy CSS button:** Exports production-ready code with JavaScript when needed

### Parameter Types
- Range sliders with live value display
- Number inputs for precise values
- Color picker with hex input
- Dropdown selects for easing curves and blend modes

## Technical Implementation

### CSS Techniques
- CSS custom properties (--variables) for dynamic values
- Pseudo-elements (::before, ::after) for layered effects
- Transform: perspective() for 3D tilt
- Mix-blend-mode for lighting integration
- Inset box-shadows for bevel effects
- Linear gradients with calculated angles

### JavaScript
- Real-time parameter binding between sliders and inputs
- Mouse position tracking with delta calculations
- Trigonometric calculations for lighting angles
- Dynamic CSS injection via style element
- Event delegation for efficient updates

### Gradient Mathematics
For edge lighting:
```
angle = atan2(deltaY, deltaX) * (180 / PI)
tiltAmount = sqrt(rotateX² + rotateY²) / maxRotation
intensity = min(tiltAmount × baseIntensity, maxIntensity)
```

## Design Decisions

### Why These 5 Effects?
1. **Scrim** - Industry standard, baseline comparison
2. **Zoom** - Popular micro-interaction, very subtle at 1%
3. **Radius** - Unique morphing effect, visually interesting
4. **Lighting** - Dynamic, follows user input, engaging
5. **Tilt** - Most premium feel, adds depth and dimension

### Tilt + Edge Lighting Refinements
- Started with simple radial gradient spotlight
- Evolved to bevel/emboss for better dimensionality
- Added multiple parameters after user feedback for fine control
- Shadow/highlight positioning calculated from tilt direction for realism
- Intensity scales with tilt amount (not just mouse distance)

### Image Sources
- Replaced Figma localhost URLs with Unsplash images
- Used hotel/property themed photos matching the use case
- Different aspect ratios (3:4, 4:3, 1:1, 16:9) for masonry variety

## Usage Instructions

1. **Open prototype:**
   ```bash
   open "/Users/remington_mcelhaney/Coding/Prototypes/Hover States/photo-tour-prototype.html"
   ```

2. **Select hover style** from the top buttons

3. **Click ⚙️ button** or press `D` to open dev panel

4. **Adjust parameters** in real-time:
   - Use sliders for quick changes
   - Type exact values for precision

5. **Test on images** by hovering and moving mouse

6. **Copy CSS** when satisfied with settings

## Key Learnings

- Edge lighting needs multiple control points (width, sharpness, falloff) for versatility
- Tilt effects feel more premium when motion is slower/heavier
- 1% zoom is barely perceptible but effective
- Bevel/emboss requires layered approach (gradients + box-shadows)
- Dev panels should be collapsible and non-intrusive
- Dual input (slider + number) provides best UX for precision

## Next Steps / Potential Enhancements
- [ ] Add combination effects (e.g., zoom + scrim, tilt + lighting + zoom)
- [ ] Mobile/responsive versions of effects
- [ ] Animation curve visualization
- [ ] Preset configurations library
- [ ] Export as React/Vue components
- [ ] A/B testing framework integration
- [ ] Performance metrics overlay
- [ ] Video recording of interactions

## Performance Notes
- All effects use CSS transforms and opacity for GPU acceleration
- No layout thrashing - uses CSS custom properties for dynamic updates
- Mouse tracking throttled implicitly by requestAnimationFrame in browser
- Minimal JavaScript - most heavy lifting done by CSS

## Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Requires CSS custom properties support
- 3D transforms require preserve-3d support
- Tested on macOS (Darwin 25.2.0)
