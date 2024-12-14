# DOOM Door Animation System Documentation

## Overview
This file (`p_doors.c`) handles all door-related functionality in DOOM, including opening, closing, and special door behaviors. It's responsible for animating vertical doors that players can interact with throughout the game.

## Key Concepts for Non-C Programmers
- **Sectors**: Areas in the game world defined by floor and ceiling heights
- **Thinkers**: Game objects that need regular updates (like moving doors)
- **Fixed-point Numbers**: Special number format used for precise calculations in DOOM

## Door Types
The code handles several types of doors:
- Normal doors
- Blazing doors (faster than normal)
- Locked doors (requiring keys)
- Timed doors (close after 30 seconds or open after 5 minutes)

## Main Functions

### T_VerticalDoor
The core door animation function that handles:
- Door movement up/down
- Wait times at fully open position
- Different door behaviors based on type
- Sound effects for door operations

Parameters:
- `door`: Pointer to door data structure

### EV_DoLockedDoor
Handles doors that require keys:
- Checks if player has required key
- Plays "oof" sound if key missing
- Shows appropriate message for missing keys

Parameters:
- `line`: The triggering line in the map
- `type`: Door behavior type
- `thing`: Object (usually player) trying to use door

### EV_DoDoor
Creates and initializes new door actions:
- Sets up door movement parameters
- Handles different door types
- Manages sound effects
- Controls door speed and wait times

### EV_VerticalDoor
Handles manual door operations:
- Processes key checks
- Creates new door thinkers
- Sets up door parameters
- Manages door heights and speeds

## Technical Details

### Door States
Doors can be in several states:
1. Waiting (0)
2. Initial Wait (2)
3. Going Down (-1)
4. Going Up (1)

### Speed Values
- Normal doors: VDOORSPEED
- Blazing doors: 4 * VDOORSPEED

### Wait Times
- Standard wait: VDOORWAIT
- Special cases: 30 seconds, 5 minutes

## Conclusion
The door system is a crucial part of DOOM's gameplay mechanics, providing both basic level navigation and security mechanisms through locked doors. The code manages all aspects of door behavior, from simple movements to complex key-based security systems.
