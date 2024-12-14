# DOOM Moving Object Handler (p_mobj.c)

## Overview
This file contains the core logic for handling moving objects ("mobjs") in DOOM. It manages everything from player characters to monsters to projectiles, controlling their movement, spawning, and destruction in the game world.

## Key Concepts
- **Mobj (Moving Object)**: Any entity that can move in the game world, including:
  - Players
  - Monsters
  - Projectiles (bullets, rockets, etc.)
  - Items
  - Decorations
- **Thinker**: A game object that needs regular updates each game tick
- **States**: Different animation/behavior states that mobjs can be in

## Major Functions

### P_SpawnMobj
Creates a new moving object in the game world.
- **Parameters**: x/y/z coordinates and object type
- **Purpose**: Spawns everything from players to monsters to items
- **Key operations**:
  - Allocates memory for the new object
  - Sets up initial properties (health, position, size)
  - Links object to game world sectors
  - Initializes animation state

### P_MobjThinker
The main update function for moving objects.
- **Purpose**: Called every game tick to update object state
- **Handles**:
  - Movement (calls P_XYMovement and P_ZMovement)
  - State changes
  - Monster respawning in Nightmare mode

### Movement Functions
#### P_XYMovement
- Handles horizontal movement
- Manages collision detection
- Applies friction
- Handles sliding along walls

#### P_ZMovement
- Controls vertical movement
- Manages gravity
- Handles floor/ceiling collisions
- Controls floating monsters

### Special Purpose Functions

#### P_SpawnPlayer
- Creates player entities when level starts
- Sets up player properties
- Initializes weapons and status displays

#### P_SpawnMissile
- Creates projectiles (rockets, plasma balls, etc.)
- Calculates trajectory
- Handles targeting

#### P_RemoveMobj
- Removes objects from the game
- Handles cleanup
- Manages item respawning in deathmatch

## Technical Details

### Memory Management
- Uses Z_Malloc for object allocation
- Objects are tracked in linked lists
- Memory is managed in zones for efficient allocation/deallocation

### Coordinate System
- Uses fixed-point math for precise positioning
- Coordinates are in "DOOM units" (roughly 16 units = 1 foot)
- Separate handling for x/y (horizontal) and z (vertical) movement

### State Management
- Objects can transition between different states
- States control animation and behavior
- State changes can trigger action functions

## Conclusion
This file is central to DOOM's gameplay, handling the creation, movement, and destruction of all dynamic objects in the game world. It demonstrates sophisticated techniques for 3D movement, collision detection, and game state management within the constraints of 1993 hardware.
