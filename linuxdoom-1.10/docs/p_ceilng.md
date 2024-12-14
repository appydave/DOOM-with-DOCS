# Ceiling Movement System in DOOM (p_ceilng.c)

## Overview
This file handles all ceiling-related animations in DOOM, including raising, lowering, and crushing ceiling movements. It's a crucial part of DOOM's dynamic environment system that allows ceilings to move, creating dramatic effects like crushing traps or revealing new areas.

## Key Components

### Global State
- `activeceilings`: An array that keeps track of all currently moving ceilings in the game
- `MAXCEILINGS`: Maximum number of ceilings that can move simultaneously

### Main Functions

#### T_MoveCeiling
The core function that handles ceiling movement physics. It:
- Controls ceiling movement direction (up/down)
- Handles different types of ceiling behaviors
- Manages sound effects during movement
- Responds to collision events

Parameters:
- `ceiling`: A pointer to the ceiling structure being moved

#### EV_DoCeiling
Initiates a new ceiling movement event. It:
- Creates a new ceiling movement based on the specified type
- Sets up initial parameters (speed, height, crush damage)
- Adds the ceiling to the active ceilings list

Parameters:
- `line`: The trigger line that activated the ceiling
- `type`: The type of ceiling movement to perform

Types of Ceiling Movements:
- fastCrushAndRaise: Quickly crushes down and raises back
- silentCrushAndRaise: Same as above but without sound
- crushAndRaise: Standard crushing ceiling
- lowerAndCrush: Lowers and stays down
- lowerToFloor: Lowers to floor level
- raiseToHighest: Raises to match highest nearby ceiling

### Utility Functions

#### P_AddActiveCeiling
Adds a ceiling to the active ceilings list for processing.

#### P_RemoveActiveCeiling
Removes a ceiling from processing when its movement is complete.

#### P_ActivateInStasisCeiling
Restarts a paused ceiling movement.

#### EV_CeilingCrushStop
Emergency stops a crushing ceiling.

## Technical Concepts for Non-C Programmers

### Structures
- `ceiling_t`: Contains all information about a moving ceiling:
  - Current position
  - Target height
  - Movement speed
  - Crush damage flag
  - Movement type

### Memory Management
The code uses DOOM's zone memory system (Z_Malloc) to allocate memory for new ceiling movements.

### Thinkers
DOOM uses a "thinker" system for updating game objects. Ceilings are registered as thinkers to receive regular updates.

## Conclusion
This system enables DOOM's dynamic ceiling mechanics, creating tension and environmental hazards through moving architecture. It's a key part of DOOM's level interaction system, allowing for complex traps and dramatic environmental changes during gameplay.
