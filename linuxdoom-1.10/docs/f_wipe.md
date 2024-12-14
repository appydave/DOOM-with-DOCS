# Screen Wipe Effects in DOOM (f_wipe.c)

## Overview
This file implements the screen transition effects (known as "wipes") that appear between levels in DOOM. It provides two main types of transitions:
1. Color transformation wipe
2. Melting screen effect (the iconic DOOM level transition)

## Key Components

### Global Variables
- `go`: Controls whether the wipe effect is active
- `wipe_scr_start`: Pointer to the starting screen image
- `wipe_scr_end`: Pointer to the ending screen image
- `wipe_scr`: Pointer to the current screen being drawn
- `y`: Array storing vertical positions for the melt effect

### Screen Transformation Function
`wipe_shittyColMajorXform`
- Transforms screen data from row-major to column-major format
- Makes the melting effect more efficient
- Takes an array of pixels and rearranges them by columns instead of rows

### Color Transform Effect
Three main functions handle the color transformation:
1. `wipe_initColorXForm`: Initializes by copying the start screen
2. `wipe_doColorXForm`: Gradually changes pixel colors from start to end screen
3. `wipe_exitColorXForm`: Cleanup function

### Melt Effect
The famous melting transition uses three functions:
1. `wipe_initMelt`: 
   - Sets up the initial state
   - Creates random starting positions for each column
   - Transforms screen data for efficient column access

2. `wipe_doMelt`:
   - Core of the melting animation
   - Processes each column of the screen
   - Creates the dripping effect by gradually revealing the new screen

3. `wipe_exitMelt`:
   - Cleanup function
   - Frees allocated memory

### Screen Management
- `wipe_StartScreen`: Captures the initial screen state
- `wipe_EndScreen`: Captures the final screen state
- `wipe_ScreenWipe`: Main control function that:
  - Selects which wipe effect to use
  - Manages the wipe animation process
  - Controls timing and completion

## Technical Details for Non-C Programmers
- The code uses "pointers" (`byte*`, `short*`) which are variables that store memory addresses
- Memory management is handled through `Z_Malloc` (allocate) and `Z_Free` (deallocate)
- Screen data is stored as arrays of pixels, either as bytes or shorts
- The melting effect works by manipulating columns of pixels independently

## How It Works Together
1. When a level transition begins:
   - The current screen is saved
   - The next screen is prepared
   - A wipe effect is initiated
2. During the transition:
   - The selected effect (color transform or melt) processes the screens
   - Each frame updates the display to show the progression
3. The effect continues until completion, creating a smooth transition between screens

This code is responsible for DOOM's distinctive visual transitions, particularly the memorable melting effect between levels.
