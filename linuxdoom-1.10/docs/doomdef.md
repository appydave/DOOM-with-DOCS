# DOOM Core Definitions (doomdef.h)

## Overview
This header file contains fundamental definitions and constants used throughout the DOOM engine. It defines game modes, key controls, screen dimensions, and various game-specific enumerations.

## Key Components

### Version Information
- `VERSION`: DOOM version number (110)

### Game Modes
```c
typedef enum {
    shareware,    // DOOM 1 shareware
    registered,   // DOOM 1 registered
    commercial,   // DOOM 2 retail
    retail,       // DOOM 1 retail
    indetermined  // No IWAD found
} GameMode_t;
```

### Screen Configuration
- `SCREENWIDTH`: 320 pixels
- `SCREENHEIGHT`: 200 pixels
- `BASE_WIDTH`: Base screen width (320)
- `SCREEN_MUL`: Screen multiplication factor
- `INV_ASPECT_RATIO`: Inverse aspect ratio for scaling

### Game Constants
- `MAXPLAYERS`: Maximum number of players (4)
- `TICRATE`: Game updates per second (35)

### Game Items and Weapons
- Card types (blue, yellow, red cards/skulls)
- Weapon types (fist, pistol, shotgun, etc.)
- Ammunition types
- Power-up types and durations

### Keyboard Controls
Defines key codes for:
- Arrow keys
- Function keys (F1-F12)
- Special keys (Enter, Escape, etc.)
- Modifier keys (Shift, Ctrl, Alt)

## Usage in DOOM
This header serves as the central reference for core game constants and types. It's included by most other source files and provides the fundamental definitions that shape DOOM's behavior and capabilities.
