# DOOM Info.c Documentation

## Overview
This file contains the core data structures that define the behavior, appearance, and properties of all objects (called "things" or "mobjs") in DOOM. It includes two major arrays:
- `states[]`: Defines all possible states/animations for game objects
- `mobjinfo[]`: Defines properties for every type of game object

## Key Concepts for Non-C Programmers

### Structures
The file uses C structures (`struct`) which are like templates that group related data together:
- `state_t`: Defines a single animation frame/state
- `mobjinfo_t`: Defines properties for a type of game object

### Arrays
The file primarily consists of two large arrays that contain predefined data:
- Arrays in C are fixed-size collections of items
- Each array element contains multiple fields defined by its structure

### Constants and Flags
Many values reference predefined constants (like `MF_SOLID`) that act as flags or identifiers:
- Flags are used to give objects specific properties (can be solid, shootable, etc.)
- Constants make the code more readable and maintainable

## Major Components

### State Definitions (states[])
Each state defines:
- Which sprite to display
- How long to display it
- What action function to call
- Which state comes next
- Additional properties

Example state entry:
```c
{SPR_PLAY,0,-1,{NULL},S_NULL,0,0}  // S_PLAY
```
- `SPR_PLAY`: Sprite to use
- `0`: Sprite frame
- `-1`: Duration (-1 means forever)
- `{NULL}`: No action function
- `S_NULL`: No next state
- `0,0`: Additional parameters

### Object Definitions (mobjinfo[])
Each entry defines a complete game object type with properties like:
- Health
- Speed
- Size
- Behavior states
- Sound effects
- Flags for special properties

Example object entry:
```c
{
    2018,           // doomednum (map editor number)
    S_ARM1,         // spawnstate
    1000,           // spawnhealth
    S_NULL,         // seestate
    sfx_None,       // seesound
    8,              // reactiontime
    sfx_None,       // attacksound
    S_NULL,         // painstate
    0,              // painchance
    sfx_None,       // painsound
    S_NULL,         // meleestate
    S_NULL,         // missilestate
    S_NULL,         // deathstate
    S_NULL,         // xdeathstate
    sfx_None,       // deathsound
    0,              // speed
    20*FRACUNIT,    // radius
    16*FRACUNIT,    // height
    100,            // mass
    0,              // damage
    sfx_None,       // activesound
    MF_SPECIAL,     // flags
    S_NULL          // raisestate
}
```

## Key Object Types
The file defines all game objects including:
- Players
- Monsters (Imps, Demons, etc.)
- Weapons
- Ammunition
- Power-ups
- Decorations
- Special effects

## Usage
This file provides the foundational data that:
1. Tells the game engine how objects should behave
2. Defines what states/animations are available
3. Sets up properties for every type of game object
4. Controls object interactions through flags

## Conclusion
info.c is a crucial data file that defines the behavior and properties of everything that exists in the DOOM world. While it contains little actual code, its data structures form the backbone of how objects appear and behave in the game.
