# Platform (Elevator) System Documentation
> Documentation for DOOM's platform/elevator movement system (p_plats.c)

## Overview
This file implements the elevator platform system in DOOM - the code that handles moving floors that can raise and lower. These platforms are used to create interactive level elements like lifts, elevators, and moving floors that can transport the player vertically through the game world.

## Key Concepts
For those unfamiliar with C programming:
- A "sector" is a basic building block of DOOM's levels - an area with a floor and ceiling
- "Thinkers" are objects that need to update each game tick
- FRACUNIT is DOOM's fixed-point math unit (1 FRACUNIT = 1.0 in decimal)

## Platform Types
The code supports several types of platforms:
- `perpetualRaise`: Continuously moves up and down
- `downWaitUpStay`: Moves down, waits, then moves up and stays there
- `blazeDWUS`: A faster version of downWaitUpStay
- `raiseAndChange`: Raises by a specific amount and changes floor texture
- `raiseToNearestAndChange`: Raises to match nearest higher floor and changes texture

## Key Functions

### T_PlatRaise
The main platform movement function that:
- Handles platform state (up, down, waiting, in_stasis)
- Moves platforms using T_MovePlane
- Plays appropriate sound effects
- Handles crushing checks
- Manages platform state transitions

### EV_DoPlat
Creates and initializes new platform movements:
- Takes a line trigger and platform type as input
- Finds affected sectors using line tags
- Creates and configures new platform thinkers
- Sets up movement parameters (speed, wait time, heights)

### Platform Management Functions
- `P_AddActivePlat`: Adds a platform to the active platforms list
- `P_RemoveActivePlat`: Removes a platform from active duty
- `P_ActivateInStasis`: Reactivates stopped platforms
- `EV_StopPlat`: Stops platforms with matching tags

## Global State
- `activeplats`: Array tracking all active platforms (max MAXPLATS)

## Technical Details
The code uses:
- Fixed-point math for precise movement
- State machines for platform behavior
- Sound triggers for movement feedback
- Sector specialdata for tracking active effects

## Platform States
Platforms can be in these states:
1. `up`: Moving upward
2. `down`: Moving downward
3. `waiting`: Paused between movements
4. `in_stasis`: Temporarily stopped by trigger

## Summary
This system provides DOOM's vertical platform movement mechanics, handling everything from simple lifts to complex synchronized platforms. It integrates with the game's physics, sound, and trigger systems to create interactive vertical level elements.
