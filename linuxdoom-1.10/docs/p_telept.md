# Teleportation System in DOOM (p_telept.c)

## Overview
This file implements the teleportation mechanics in DOOM. When a player enters a teleporter, they are instantly transported to another location in the game world, accompanied by a fog effect and teleportation sound.

## Key Components

### Include Files
The code includes several DOOM-specific header files that provide:
- Basic definitions (`doomdef.h`)
- Sound system functions (`s_sound.h`)
- Local play functions (`p_local.h`)
- Game sounds (`sounds.h`)
- Rendering state (`r_state.h`)

### Main Function: EV_Teleport

#### Purpose
Handles the teleportation of game objects (except missiles) from one location to another.

#### Parameters
- `line`: The trigger line that activated the teleporter
- `side`: Which side of the line was touched (front or back)
- `thing`: The object being teleported (usually the player)

#### How It Works

1. **Initial Checks**
   - Prevents missiles from teleporting
   - Only allows teleportation from the front side of the teleporter

2. **Teleporter Location Finding**
   - Uses a tag system to find the destination
   - Searches through all sectors for matching tags
   - Looks for special "teleportman" markers that define destination points

3. **Teleportation Process**
   - Stores the object's original position
   - Moves the object to the new location
   - Adjusts the player's view height if needed
   - Creates fog effects at both the start and end points
   - Plays teleportation sound effects
   - Sets a brief delay before the player can move again
   - Resets the object's momentum and adjusts its angle

#### Return Value
- Returns 1 if teleportation was successful
- Returns 0 if teleportation failed or was blocked

## Technical Details

### Important Variables
- `oldx`, `oldy`, `oldz`: Store the original position
- `thing->reactiontime`: Controls post-teleport movement delay
- `thing->angle`: Direction the player faces after teleporting
- `thing->momx`, `thing->momy`, `thing->momz`: Movement momentum (reset after teleporting)

### Special Effects
- Creates fog effects (MT_TFOG) at both the departure and arrival points
- Plays teleportation sound (sfx_telept) at both locations

## Summary
This code creates DOOM's iconic teleportation system, handling both the mechanical aspects (moving objects between points) and the aesthetic elements (fog effects and sounds) that make teleportation feel satisfying and dramatic in the game.
