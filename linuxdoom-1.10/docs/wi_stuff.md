# DOOM Intermission Screen Handler (wi_stuff.c)

## Overview
This file handles the intermission screens in DOOM - the screens that appear between levels showing statistics like kills, items collected, and secrets found. It manages both single-player and multiplayer (including deathmatch) intermission displays.

## Key Components

### Data Structures

#### Animation Types
```c
typedef enum {
    ANIM_ALWAYS,  // Animation that plays continuously
    ANIM_RANDOM,  // Animation that plays randomly
    ANIM_LEVEL    // Animation tied to specific level
} animenum_t;
```

#### Animation Structure
```c
typedef struct {
    animenum_t type;    // Type of animation
    int period;         // Time between frames
    int nanims;        // Number of frames
    point_t loc;       // Screen location
    patch_t* p[3];     // Animation frames
    // ... other animation control fields
} anim_t;
```

### Major Functions

#### Initialization
- `WI_Start()`: Entry point for intermission screen
- `WI_loadData()`: Loads graphics and initializes resources
- `WI_initStats()`: Prepares statistics display
- `WI_initVariables()`: Sets up initial state

#### Update and Drawing
- `WI_Ticker()`: Main update function called each game tick
- `WI_Drawer()`: Renders the intermission screen
- `WI_drawStats()`: Displays player statistics
- `WI_drawTime()`: Shows level completion time
- `WI_drawNum()`: Utility for drawing numbers

#### State Management
- `WI_updateStats()`: Updates statistics counters
- `WI_checkForAccelerate()`: Handles player input to skip
- `WI_initAnimatedBack()`: Sets up background animations

### Screen Types

1. **Single Player**
   - Shows kills, items, secrets percentages
   - Displays level completion time
   - Compares with par time

2. **Network Game**
   - Shows statistics for all players
   - Includes frags in deathmatch mode

3. **Deathmatch**
   - Displays kill matrix between players
   - Shows total frags per player

## Technical Details

### Animation System
The code uses a sophisticated animation system for the background and various UI elements:
- Animations can be continuous, random, or level-triggered
- Each animation has multiple frames stored as patches
- Timing is controlled through the game's tick system

### State Machine
The intermission screen operates as a state machine with states:
- StatCount: Counting up statistics
- ShowNextLoc: Showing the next level
- NoState: Cleanup state

### Resource Management
- Graphics are loaded from WAD file using `W_CacheLumpName`
- Resources are properly freed using `Z_ChangeTag`
- Memory management is handled through DOOM's zone memory system

## Conclusion
This code represents a complex UI system that handles the between-level intermission screens in DOOM. It manages multiple display modes, animations, and player statistics, while integrating with DOOM's resource management and rendering systems.
