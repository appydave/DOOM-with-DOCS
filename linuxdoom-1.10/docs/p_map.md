# DOOM Movement and Collision System (p_map.c)

## Overview
This file contains the core movement and collision detection system for DOOM. It handles how objects (players, monsters, projectiles) move through the game world, interact with walls and other objects, and implements features like sliding along walls and damage from explosions.

## Key Concepts
For non-C programmers:
- `fixed_t`: A special number type DOOM uses for precise positions (think decimal numbers)
- `mobj_t`: "Map Object" - represents any physical thing in the game (player, monster, item)
- `line_t`: Represents a wall or boundary in the game
- `sector_t`: A room or area in the game defined by floor and ceiling heights

## Major Systems

### Movement and Collision
The core movement system uses these main functions:

#### P_CheckPosition
Checks if an object can be placed at a specific position without overlapping walls or other objects.
- Input: An object and target X,Y coordinates
- Output: True if position is valid, false if blocked
- Also calculates floor and ceiling heights at that position

#### P_TryMove
Attempts to move an object to a new position:
1. Checks if position is valid using P_CheckPosition
2. Handles height differences (stairs, ledges)
3. Triggers special effects when crossing certain lines
4. Updates object's position if move is valid

#### P_SlideMove
Sophisticated system that lets players slide along walls when they hit them at an angle:
1. Finds the wall that was hit
2. Calculates new movement direction along the wall
3. Attempts to slide in that direction
4. Can handle multiple walls in sequence

### Combat Systems

#### P_LineAttack
Handles "instant hit" weapons (like the pistol):
1. Traces a line from shooter to target
2. Checks for walls or objects in the way
3. Applies damage to first thing hit
4. Spawns visual effects (bullet puffs, blood)

#### P_RadiusAttack
Handles explosions:
1. Takes an origin point and damage radius
2. Finds all objects within blast radius
3. Checks line of sight to each object
4. Applies damage based on distance from explosion

### Special Features

#### P_UseLines
Handles player interaction with walls/doors:
1. Checks in front of player for usable walls
2. Activates doors, switches, etc.
3. Plays "can't use" sound if nothing usable found

#### P_ChangeSector
Handles moving floors/ceilings:
1. Adjusts heights of all objects in sector
2. Can crush objects if they don't fit
3. Handles special effects like blood/gibs

## Technical Details

### Global Variables
- `tmthing`: Current object being moved/checked
- `tmx`, `tmy`: Target coordinates being tested
- `tmflags`: Current object's flags
- `floatok`: Whether current position is valid for height
- `tmbbox`: Bounding box for collision checks

### Helper Functions
- `PIT_CheckLine`: Checks collision with a single wall
- `PIT_CheckThing`: Checks collision with a single object
- `PTR_AimTraverse`: Helps aim at targets
- `PTR_ShootTraverse`: Handles projectile collision

## Summary
This file is the heart of DOOM's physics system, handling all movement, collision, and related effects. It's designed to be fast and efficient while providing convincing physics behavior within the limitations of 1993 hardware. The code uses many global variables to avoid passing large amounts of data between functions, which was a common optimization technique in that era.
