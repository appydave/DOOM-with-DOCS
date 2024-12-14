# DOOM Special Effects Handler (p_spec.c)

## Overview
This file implements special effects in DOOM, including:
- Texture animations
- Height changes in sectors
- Lighting changes
- Line triggers and sector triggers
- Special sector behaviors (like damaging floors)

## Key Concepts for Non-C Programmers
- **Sectors**: Areas in the game world with specific properties (floor height, ceiling height, lighting)
- **Lines**: Boundaries between sectors that can trigger effects when crossed
- **Thinkers**: Game objects that update each game tick
- **Fixed-point numbers**: Used instead of floating point for consistent behavior

## Data Structures

### Animation (anim_t)
```c
typedef struct {
    boolean     istexture;
    int         picnum;
    int         basepic;
    int         numpics;
    int         speed;
} anim_t;
```
Controls texture/flat animations in the game. Defines how textures change over time.

## Major Functions

### P_InitPicAnims()
Initializes all animated textures in the game. Sets up animations for:
- Flowing liquids (nukage, lava, etc)
- Flashing lights
- Animated walls

### P_CrossSpecialLine()
Called when something crosses a special line in the game. Handles:
- Doors opening/closing
- Lifts/platforms activating
- Teleporters
- Crushing ceilings

### P_PlayerInSpecialSector()
Checks if player is in a special sector and applies effects:
- Damage from harmful floors (slime, lava)
- Secret area detection
- Special level exits

### P_UpdateSpecials()
Main update function for special effects:
- Animates textures
- Updates scrolling walls
- Handles button timers
- Updates level timer

## Special Effects Types

### Sector Effects
- Light flickering
- Strobing lights
- Glowing lights
- Damaging floors
- Secret areas
- Automatic doors

### Line Effects
- Doors
- Lifts
- Stairs
- Crushing ceilings
- Teleporters
- Light changes

## Technical Details

### Trigger System
The code uses a tag system to connect triggers (lines) with their effects (sectors). When a line is activated:
1. Checks line's special type
2. Finds all sectors with matching tag
3. Applies effect to those sectors

### Animation System
Textures are animated by:
1. Defining animation sequences in `animdefs`
2. Updating texture numbers each tick
3. Using translation tables to swap textures

## Conclusion
This file is central to DOOM's interactive environment, handling all special effects that make the game world dynamic and interactive. It manages everything from simple animated textures to complex multi-sector effects like lifts and crushers.
