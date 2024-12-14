# DOOM Level Setup (p_setup.c)

## Overview
This file is responsible for loading and setting up DOOM game levels from WAD files. It handles all the map data loading, including vertices, sectors, lines, and things that make up each level's geometry and gameplay elements.

## Key Concepts for Non-C Programmers
- **WAD Files**: These are data files containing DOOM level data ("Where's All the Data")
- **Lumps**: Sections within WAD files containing specific types of data
- **Fixed-point Numbers**: DOOM uses fixed-point arithmetic instead of floating point for performance
- **Memory Zones**: Special memory management system used by DOOM for efficient allocation/deallocation

## Global Variables
The file maintains several important global arrays and variables that store level data:
- `vertexes`: Array of points that define corners of walls
- `sectors`: Array of areas (rooms) in the level
- `lines`: Array of walls/boundaries
- `nodes`: Binary space partition (BSP) tree nodes for rendering
- `blockmap`: Spatial subdivision grid for collision detection
- `rejectmatrix`: Quick lookup table for visibility between sectors

## Major Functions

### P_LoadVertexes
**Purpose**: Loads vertex (point) data from WAD file
- Reads X,Y coordinates for each point in the level
- Converts coordinates to DOOM's fixed-point format
- Allocates memory for vertex data

### P_LoadSectors
**Purpose**: Loads sector (room) data
- Reads floor/ceiling heights
- Sets lighting levels
- Links to floor/ceiling textures

### P_LoadLineDefs
**Purpose**: Loads line (wall) definitions
- Creates connections between vertices
- Sets wall properties (one/two sided, special effects)
- Calculates wall angles and bounding boxes

### P_LoadThings
**Purpose**: Loads objects and monsters
- Places players, monsters, items, and decorations
- Handles game mode specific spawning rules
- Converts coordinates and angles

### P_SetupLevel
**Purpose**: Main level initialization function
- Takes episode and map number
- Coordinates loading of all level elements
- Initializes game state for new level
- Sets up multiplayer spawn points

## Memory Management
The code uses DOOM's zone memory system:
- `Z_Malloc`: Allocates memory in specific zones
- `Z_Free`: Frees allocated memory
- `PU_LEVEL`: Memory zone for level data (cleared between levels)

## Technical Details
- Uses a block-based system for collision detection
- Implements BSP tree for efficient rendering
- Handles both single-player and deathmatch game modes
- Supports different skill levels

## Conclusion
This file is central to DOOM's level loading system, transforming raw WAD data into playable 3D environments. It demonstrates sophisticated memory management and data structure techniques that were groundbreaking for 1993 gaming technology.
