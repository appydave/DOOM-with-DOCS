# DOOM Status Bar Implementation (st_stuff.c)

## Overview
This file implements the status bar functionality in DOOM - the information display at the bottom of the screen showing health, ammo, weapons, and the player's face. It handles both the visual elements and the logic for updating this information during gameplay.

## Key Components

### Status Bar Elements
- Health percentage
- Armor percentage 
- Ammunition counts (current and maximum)
- Weapon selection indicators
- Key card indicators
- Player face display (showing health status and reactions)
- Frags counter (for deathmatch)

### Major Functions

#### Initialization Functions
- `ST_Init()`: Initializes the status bar system
- `ST_Start()`: Starts up the status bar for a new game
- `ST_Stop()`: Shuts down the status bar
- `ST_loadData()`: Loads graphics resources needed for the status bar
- `ST_createWidgets()`: Sets up all visual elements of the status bar

#### Update Functions
- `ST_Ticker()`: Main update function called every game tick
- `ST_updateFaceWidget()`: Updates the player's face display based on health and game events
- `ST_doPaletteStuff()`: Handles color palette effects (for damage, items, etc.)
- `ST_Drawer()`: Main drawing function for the status bar

### Face System
The status bar includes a sophisticated face display system that shows:
- Different expressions based on health levels
- Reaction to taking damage
- Direction player was hit from
- Special states (god mode, picking up items)
- Death state

### Cheat System
Includes implementation of various cheat codes:
- God mode
- All weapons
- Full ammo
- Level select
- Position display
- Music change

## Technical Details

### Key Data Structures
- Uses multiple widget types for different display elements
- Maintains state information for face animations
- Tracks player status through global player pointer

### Resource Management
- Loads and manages various graphic resources (numbers, faces, backgrounds)
- Handles palette effects for different game states
- Manages memory allocation for display buffer

## Implementation Notes
The code uses a widget-based system where each element of the status bar (health, ammo, etc.) is treated as an independent widget that can be updated and drawn separately. This modular approach allows for efficient updates of only changed elements.

The face system is particularly complex, using a priority system to determine which expression to show when multiple conditions apply (e.g., being hurt while in god mode).

## Conclusion
This file is central to DOOM's user interface, providing players with essential gameplay information through a sophisticated status bar system. It demonstrates good separation of concerns between data loading, state management, and display logic.
