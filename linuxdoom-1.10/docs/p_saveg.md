# DOOM Save Game System Documentation

## Overview
This file (`p_saveg.c`) handles saving and loading game state in DOOM. It archives (saves) and unarchives (loads) the entire game state, including players, world geometry, monsters, and special effects. The code uses a global byte pointer `save_p` to write/read data to/from the save file.

## Key Concepts for Non-C Programmers
- **Pointers**: Variables that store memory addresses. In this code, they're used extensively to reference game objects.
- **Structs**: Collections of related data fields. For example, `player_t` contains all data about a player.
- **Memory Management**: The code uses `Z_Malloc` to allocate memory and `Z_Free` to release it.
- **Type Casting**: Converting between different data types, often seen with pointers.

## Main Components

### Save File Handling
- Uses a global `save_p` pointer to track position in save file
- `PADSAVEP()` macro ensures data alignment for different computer architectures

### Player Archiving Functions
- `P_ArchivePlayers()`: Saves all active player data
  - Loops through player slots
  - Saves player state, weapons, and sprite states
  
- `P_UnArchivePlayers()`: Loads player data
  - Restores player states from save file
  - Relinks player references

### World State Functions
- `P_ArchiveWorld()`: Saves level geometry
  - Saves sector properties (floors, ceilings, lighting)
  - Saves line definitions and textures
  
- `P_UnArchiveWorld()`: Loads level geometry
  - Restores sectors and lines
  - Resets special effects

### Game Object (Thinker) Functions
- `P_ArchiveThinkers()`: Saves active game objects
  - Primarily handles mobile objects (monsters, items)
  - Saves object states and properties
  
- `P_UnArchiveThinkers()`: Loads game objects
  - Recreates monsters and items
  - Restores their states and positions

### Special Effects Functions
- `P_ArchiveSpecials()`: Saves active effects
  - Handles moving platforms, doors, lights
  - Saves effect timers and states
  
- `P_UnArchiveSpecials()`: Loads effects
  - Restores all active special effects
  - Reconnects them to their sectors

## Data Types
The code uses several specialized types for different game elements:
- `thinker_t`: Base type for updateable game objects
- `mobj_t`: Mobile objects (monsters, items)
- `ceiling_t`, `vldoor_t`, `floormove_t`: Various special effects
- `sector_t`, `line_t`: Level geometry elements

## Save Process Flow
1. Archive players
2. Archive world geometry
3. Archive active objects (monsters, items)
4. Archive special effects
5. Write terminator markers

## Load Process Flow
1. Unarchive players
2. Unarchive world geometry
3. Clear existing objects
4. Unarchive saved objects
5. Unarchive special effects
6. Reconnect all references

## Technical Notes
- Uses pointer arithmetic for save file navigation
- Handles cross-platform compatibility issues
- Manages complex object relationships and references
- Includes error checking for corrupt save files

## Conclusion
The save game system preserves the entire game state by methodically saving and restoring all dynamic elements. It handles the complex task of maintaining object relationships and ensuring that the game can resume exactly as it was when saved.
