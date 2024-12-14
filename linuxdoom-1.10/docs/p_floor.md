# Floor Movement System in DOOM (p_floor.c)

## Overview
This file handles all floor-related movement mechanics in DOOM, including raising/lowering floors and building staircases. It's a crucial part of DOOM's dynamic level architecture system that allows sectors of the map to move vertically.

## Key Components

### Floor Movement Core (T_MovePlane)
The `T_MovePlane` function is the fundamental mechanism for moving any horizontal surface (floor or ceiling) in DOOM. It:
- Takes parameters for movement speed, destination height, and direction
- Handles crush checks (when something might get crushed by the moving surface)
- Returns status codes for movement completion or crushing events

### Floor Movement Types
The code supports various types of floor movements:
- Simple raising/lowering
- Crushing floors
- Texture changes during movement
- Speed variations (normal and turbo)
- Stair-building

### Main Functions

#### T_MoveFloor
Handles the actual movement of a floor per game tick:
- Moves the floor toward its destination
- Plays movement sounds
- Handles completion of movement
- Cleans up when movement is done

#### EV_DoFloor
Initiates floor movement with various behaviors:
- Processes different floor movement types
- Sets up movement parameters
- Creates and manages floor movement thinkers
- Handles special effects like texture changes

#### EV_BuildStairs
Specialized function for creating staircases:
- Builds ascending stairs sector by sector
- Handles different stair types (normal and turbo)
- Manages height increments and movement speeds

## Technical Concepts

### Thinkers
The code uses "thinkers" - special structures that manage ongoing processes in the game. Floor movements are implemented as thinkers that update each game tick.

### Fixed-Point Numbers
Heights and speeds use DOOM's fixed-point number system (FRACUNIT) for precise movement calculations.

### Sector References
Floors are part of "sectors" - the basic building blocks of DOOM's level architecture. Each moving floor is associated with a specific sector.

## Common Use Cases
1. Platform lifts
2. Crushing ceilings
3. Rising/lowering floors for doors
4. Staircase creation
5. Environmental hazards

## Conclusion
This code is essential for DOOM's dynamic level interactions, allowing for complex vertical movement of floor surfaces that create much of the game's architectural dynamism and puzzle elements.
