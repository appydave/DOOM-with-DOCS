# DOOM Finale System (f_finale.c)

## Overview
This file handles the end-game sequences in DOOM, including text displays, victory screens, and the character casting sequence that appears at the end of DOOM II. It manages the finale animations, text rendering, and end-game state transitions.

## Key Components

### Global Variables
- `finalestage`: Controls which part of the finale is showing (0=text, 1=art screen, 2=character cast)
- `finalecount`: Timer for controlling animation pacing
- `finaletext`: Pointer to the current ending text being displayed
- `finaleflat`: Name of the background texture to use

### Text Content
The code contains multiple text variables (e1text through e4text, c1text through c6text, etc.) that store different ending messages for:
- Different DOOM episodes
- DOOM II levels
- Various game scenarios

### Main Functions

#### F_StartFinale()
Initializes the finale sequence by:
- Setting game state to finale mode
- Choosing appropriate music
- Selecting the correct ending text and background based on game mode
- Resetting animation counters

#### F_TextWrite()
Renders text on screen with these features:
- Draws a tiled background
- Displays text character by character with typewriter effect
- Handles line breaks and text positioning
- Uses the DOOM font system for character rendering

#### F_CastDrawer() and Related Functions
Manages the DOOM II cast sequence:
- Shows each game monster in turn
- Displays character names
- Handles animation states
- Responds to player input for death sequences

### Special Effects

#### F_BunnyScroll()
A special ending sequence showing scrolling graphics and text, specifically for Episode 3's ending.

## Technical Details
The code uses several DOOM engine systems:
- Sprite and texture management
- Sound system for music and effects
- Event handling for user input
- Screen drawing primitives

## How It All Works Together
1. When a player completes a game episode/level, F_StartFinale() is called
2. Based on game state, it shows either:
   - Scrolling text messages
   - Static victory screens
   - The character casting sequence (DOOM II)
3. Animation timers control the pacing
4. Player input can advance or interact with certain sequences

## Notes for Non-C Programmers
- Functions prefixed with F_ belong to the finale system
- The code uses pointer arithmetic for memory management
- Many magic numbers represent screen coordinates or timing values
- The system relies heavily on DOOM's engine capabilities for graphics and sound
