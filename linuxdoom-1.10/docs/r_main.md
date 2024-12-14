# DOOM Rendering Main Module (r_main.c)

## Overview
This file contains the core rendering logic for DOOM's 3D engine. It handles the setup and main loop of the rendering system, including view calculations, BSP traversal, and coordinate transformations. The code is responsible for converting the game's 3D world into a 2D screen representation.

## Key Components

### Global Variables
- `viewx`, `viewy`, `viewz`: Player's view position in the game world
- `viewangle`: Current viewing angle
- `viewcos`, `viewsin`: Cached trigonometric values for view angle
- `centerx`, `centery`: Screen center coordinates
- `framecount`: Counter for frame tracking
- `detailshift`: Graphics detail level (0 = high, 1 = low)

### Important Data Structures
- Lookup tables for angles and screen coordinates
- Light level tables for shading
- View angle conversion tables

## Major Functions

### R_Init()
Initializes the rendering system:
- Sets up data structures
- Initializes lookup tables
- Configures view parameters
- Prepares rendering subsystems (planes, lights, sky)

### R_RenderPlayerView(player_t* player)
Main rendering function that:
1. Sets up the frame parameters
2. Clears rendering buffers
3. Renders the BSP tree
4. Draws planes (floors/ceilings)
5. Renders masked textures (sprites)

### Geometric Utility Functions

#### R_PointToAngle(fixed_t x, fixed_t y)
Converts cartesian coordinates to angles:
- Takes x,y coordinates relative to viewer
- Returns angle in DOOM's angle format
- Uses octant system for efficient calculation

#### R_PointInSubsector(fixed_t x, fixed_t y)
Determines which subsector contains a point:
- Traverses BSP tree
- Returns pointer to containing subsector
- Used for collision detection and rendering

### View Setup Functions

#### R_SetupFrame(player_t* player)
Prepares rendering frame:
- Sets view position and angle
- Updates lighting parameters
- Initializes frame counters

#### R_ExecuteSetViewSize()
Handles view size changes:
- Calculates screen parameters
- Updates scaling factors
- Selects appropriate rendering functions

## Technical Concepts

### Fixed-Point Math
The code uses fixed-point arithmetic (fixed_t type) for precise calculations without floating-point math:
- Numbers are scaled by FRACUNIT (1.0 = 65536)
- Special multiplication and division functions handle fixed-point math

### BSP Tree
Binary Space Partitioning (BSP) tree is used for:
- Determining drawing order
- Efficient point location
- Visibility determination

### Angle Representation
Angles are stored in "BAM" (Binary Angle Measurement):
- Full circle = 2^32 units
- Allows fast binary angle calculations
- Lookup tables optimize trigonometric functions

## Conclusion
This module forms the backbone of DOOM's rendering system, coordinating various subsystems to create the game's 3D view. It manages the complex task of converting a 3D world space into a 2D screen space while handling visibility, lighting, and perspective calculations.
