# Doom Automap Implementation (am_map.c)

## Overview
This file implements Doom's automap feature - an overhead view of the game level that players can access during gameplay. The automap shows walls, player positions, and optionally grid lines and game objects ("things").

## Key Components

### Constants and Configuration
- Color definitions (e.g., REDS, BLUES, GREENS) for different map elements
- Key bindings for automap controls (panning, zooming, toggling features)
- Scale and zoom parameters
- Grid settings

### Data Structures
- `fpoint_t`: Screen coordinates (x,y)
- `mpoint_t`: Map coordinates (x,y) 
- `fline_t`: Line segment in screen coordinates
- `mline_t`: Line segment in map coordinates
- Pre-defined line arrays for drawing player arrows and markers

### Key Functions

#### Initialization & Setup
- `AM_Start()`: Initializes the automap
- `AM_Stop()`: Shuts down the automap
- `AM_LevelInit()`: Sets up automap for a new level

#### Drawing Functions
- `AM_drawWalls()`: Renders level walls
- `AM_drawPlayers()`: Shows player positions
- `AM_drawGrid()`: Draws coordinate grid
- `AM_drawThings()`: Shows monsters and items (in cheat mode)
- `AM_drawMarks()`: Displays player-placed markers
- `AM_Drawer()`: Main drawing routine

#### Input Handling
- `AM_Responder()`: Processes player input for panning/zooming

#### Utility Functions
- `AM_clipMline()`: Clips lines to visible area
- `AM_rotate()`: Rotates coordinates for arrow drawing
- `AM_changeWindowScale()`: Handles zoom operations

## How It Works

1. When player activates automap (default: TAB key)
   - Screen switches to overhead view
   - Initial view centered on player

2. During active automap:
   - Player can pan view (arrow keys)
   - Zoom in/out (+ and - keys)
   - Toggle grid (G key)
   - Place markers (M key)

3. Drawing process:
   - Clears frame buffer
   - Draws grid (if enabled)
   - Renders walls (different colors for different wall types)
   - Shows player position(s)
   - Displays markers
   - Updates screen

## Technical Notes
- Uses fixed-point math for precise coordinate handling
- Implements Cohen-Sutherland line clipping
- Supports multiplayer with different colored arrows
- Includes cheat mode showing all map elements

## Conclusion
The automap system provides players with a crucial navigation tool while maintaining the game's atmosphere through limited information display and gradual map revelation during exploration.
