# DOOM Map Utility Functions Documentation

## Overview
This file (`p_maputl.c`) contains utility functions for handling movement and collision detection in DOOM. It provides essential calculations for determining positions, intersections, and spatial relationships between game objects and map geometry.

## Key Concepts
Before diving into the functions, it's helpful to understand some DOOM-specific concepts:

- **Fixed Point Numbers**: DOOM uses fixed-point arithmetic (instead of floating point) for precise calculations. Numbers are stored as integers where a portion represents the fractional part.
- **FRACUNIT**: The basic unit of measurement in DOOM's fixed-point system.
- **Blockmap**: A spatial partitioning system that divides the map into blocks for efficient collision detection.

## Core Functions

### Distance Calculation
`P_AproxDistance(dx, dy)`
- Provides a quick approximation of distance between two points
- Takes x and y differences as inputs
- Returns an estimated distance without using expensive square root calculations
- Used for performance-critical operations where exact distance isn't necessary

### Line Side Tests
`P_PointOnLineSide(x, y, line)`
- Determines which side of a line a point is on
- Returns 0 for front side, 1 for back side
- Used for collision detection and visibility calculations

`P_BoxOnLineSide(tmbox, ld)`
- Tests if a box (defined by coordinates) is on a particular side of a line
- Returns -1 if the box crosses the line
- Used for checking if objects intersect with walls

### Thing (Object) Position Management
`P_UnsetThingPosition(thing)`
- Removes an object from the game's spatial tracking systems
- Updates both sector and blockmap links
- Called before moving an object

`P_SetThingPosition(thing)`
- Places an object into the game's spatial tracking systems
- Updates sector and blockmap links
- Called after moving an object

### Intercept Calculations
These functions handle ray-casting and line-of-sight calculations:

`P_PathTraverse(x1, y1, x2, y2, flags, traverser)`
- Traces a line between two points
- Calls a callback function for each line or thing encountered
- Used for line-of-sight checks, projectile paths, etc.

`P_InterceptVector(v2, v1)`
- Calculates where two lines intersect
- Returns the fractional distance along the first line where intersection occurs
- Critical for collision detection

## Global Variables
- `opentop`, `openbottom`, `openrange`: Track vertical space available for movement
- `lowfloor`: Keeps track of the lowest floor height encountered
- `intercepts`: Array storing intersection points during path traversal
- `trace`: Current line being traced for intersection tests

## Technical Notes
1. The code uses extensive bit manipulation and fixed-point math for performance
2. Many calculations are optimized for speed rather than accuracy
3. The blockmap system allows for efficient spatial queries
4. Special care is taken to handle edge cases in geometric calculations

## Usage Example
When a monster needs to check if it can see a player:
1. `P_PathTraverse` is called with the monster's position and player's position
2. The traverser function checks each intercepted line
3. If an opaque wall is hit, line of sight is blocked
4. If no blocking lines are found, the monster can see the player

This documentation provides a high-level overview. The actual code contains many optimizations and special cases for DOOM's specific needs.
