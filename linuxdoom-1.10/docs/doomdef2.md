# DOOM Definition Files Documentation

## Overview
The doomdef.h and doomdef.c files contain fundamental definitions and constants used throughout the DOOM game engine. These files establish the core game parameters, version information, and essential enumerations that define game states, weapons, items, and controls.

## Key Components

### Game Version and Mode
- Game version is defined as 1.10 (VERSION = 110)
- Different game modes are defined to handle various DOOM releases:
  - Shareware (DOOM 1 shareware)
  - Registered (DOOM 1 registered)
  - Commercial (DOOM 2 retail)
  - Retail (DOOM 1 retail)

### Screen and Display Settings
- Base screen width: 320 pixels
- Screen height: 200 pixels
- Screen multiplier: 1
- Inverse aspect ratio: 0.625

### Game Parameters
- Maximum players: 4
- Tick rate: 35 ticks per second (TICRATE)

### Game States
Four main game states are defined:
1. GS_LEVEL - Active gameplay
2. GS_INTERMISSION - Between levels
3. GS_FINALE - End game sequence
4. GS_DEMOSCREEN - Demo playback

### Game Items and Weapons

#### Key Cards
Six different key cards/skulls:
- Blue card/skull
- Yellow card/skull
- Red card/skull

#### Weapons
Nine weapon types:
- Fist
- Pistol
- Shotgun
- Chaingun
- Missile launcher
- Plasma rifle
- BFG
- Chainsaw
- Super shotgun

#### Ammunition Types
Four main ammo types:
- Clips (for pistol/chaingun)
- Shells (for shotguns)
- Cells (for plasma rifle/BFG)
- Missiles (for missile launcher)

### Power-ups
Six different power-up types with specific durations:
- Invulnerability (30 seconds)
- Strength
- Invisibility (60 seconds)
- Iron Feet (60 seconds)
- All Map
- Infrared Vision (120 seconds)

### Keyboard Controls
Defines key mappings for:
- Arrow keys
- Function keys (F1-F12)
- Special keys (Enter, Escape, Tab)
- Modifier keys (Shift, Ctrl, Alt)

## Technical Notes
- The code includes optional range checking for parameter validation (RANGECHECK)
- Sound server implementation can be configured (SNDSERV)
- Screen resolution is fixed and not dynamically adjustable
- The implementation includes preprocessor definitions for cross-platform compatibility

## Implementation Details
While doomdef.h contains all the definitions and declarations, doomdef.c is primarily a placeholder file that implements the header. The actual functionality is distributed across other source files in the DOOM codebase.

## Usage
These files serve as the foundation for the DOOM engine, providing essential definitions that are used throughout the codebase. Any modification to these core definitions could have wide-ranging effects on the game's behavior and functionality.
