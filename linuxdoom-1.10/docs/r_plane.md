# DOOM Plane Rendering System (r_plane.c)

## Overview
This file is a core component of DOOM's rendering engine, specifically handling the drawing of floors and ceilings (collectively called "planes"). It maintains per-column clipping lists and handles sky area determination. This is crucial for creating DOOM's 3D-like environment from a 2D perspective.

## Key Concepts

### Visplanes
A visplane is a horizontal surface (floor or ceiling) that is visible in the game. The code manages these through the `visplane_t` structure, with a maximum of 128 visplanes allowed at once. Each visplane tracks:
- Height
- Texture (picnum)
- Light level
- Screen coordinates (minx, maxx)
- Top/bottom arrays for height information

### Clipping
The code maintains two important clipping arrays:
- `floorclip`: Tracks the lowest visible pixel for floors
- `ceilingclip`: Tracks the highest visible pixel for ceilings
These prevent drawing areas that are obscured by walls or other elements.

## Major Functions

### R_InitPlanes
Purpose: Initializes the plane rendering system at game startup.
Currently empty in this implementation ("Doh!").

### R_ClearPlanes
Purpose: Resets plane rendering data at the beginning of each frame.
- Resets clipping boundaries
- Initializes texture calculation variables
- Sets up angle-dependent scaling factors

### R_FindPlane
Purpose: Locates or creates a visplane based on height, texture, and light level.
Parameters:
- height: Vertical position of the plane
- picnum: Texture index
- lightlevel: Brightness level
Returns: Pointer to the appropriate visplane

### R_MapPlane
Purpose: Core rendering primitive that maps textures onto planes.
Parameters:
- y: Screen Y coordinate
- x1, x2: Start and end X coordinates
Handles:
- Distance calculations
- Texture coordinate mapping
- Lighting effects

### R_DrawPlanes
Purpose: Main plane rendering function called at the end of each frame.
- Processes all visible planes
- Handles special sky texture rendering
- Applies proper lighting and texture mapping

## Technical Details

### Memory Management
The code uses several fixed-size arrays:
- `visplanes`: Array of plane structures (max 128)
- `openings`: Array for storing plane spans
- Various cached values for optimization

### Sky Handling
Special case handling for sky textures:
- Always drawn at full brightness
- Uses different scaling than regular planes
- Implements infinite distance effect

### Optimization Techniques
- Caches frequently used calculations
- Uses fixed-point math for speed
- Implements span-based rendering for efficiency

## Conclusion
This code represents a crucial part of DOOM's rendering pipeline, specifically handling horizontal surfaces. It balances performance with visual quality through careful optimization and clever tricks like sky handling and span-based rendering.
