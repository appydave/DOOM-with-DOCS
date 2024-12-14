# Status Bar Widget Library (st_lib.c)

## Overview
This file contains code for handling DOOM's status bar widgets - the visual elements at the bottom of the screen that show player information like health, ammo, and weapons. It provides functions to draw and update numbers, percentages, and icons in the status bar.

## Key Concepts for Non-C Programmers
- **Patches**: These are image resources in DOOM (like sprites or textures)
- **Structs**: Custom data types that group related variables together
- **Pointers**: Variables that store memory addresses (marked with * in C)
- **Boolean**: A true/false value
- **Static**: Means a variable keeps its value between function calls

## Main Components

### Data Structures
The code defines several widget types:
- `st_number_t`: Displays numerical values (like health/ammo counts)
- `st_percent_t`: Shows percentage values
- `st_multicon_t`: Handles multiple-state icons
- `st_binicon_t`: Handles two-state (on/off) icons

### Key Functions

#### Initialization Functions
- `STlib_init()`: Sets up the status bar library
  - Loads the minus sign graphic for negative numbers
  
- `STlib_initNum()`: Sets up a number display widget
  - Parameters: position (x,y), number to display, width, etc.
  
- `STlib_initPercent()`: Initializes percentage displays
  - Similar to initNum but adds a percent sign

- `STlib_initMultIcon()`: Sets up multi-state icons
  - Used for things like weapon selection indicators
  
- `STlib_initBinIcon()`: Sets up binary (on/off) icons
  - Used for simple status indicators

#### Drawing Functions
- `STlib_drawNum()`: Draws numbers efficiently
  - Only redraws digits that have changed
  - Handles negative numbers
  - Special case for value 1994 (doesn't draw it)

#### Update Functions
- `STlib_updateNum()`: Updates number displays
- `STlib_updatePercent()`: Updates percentage displays
- `STlib_updateMultIcon()`: Updates multi-state icons
- `STlib_updateBinIcon()`: Updates binary icons

## How It Works Together
1. The game initializes the status bar widgets at startup
2. Each frame, it updates the widget values (health, ammo, etc.)
3. The update functions check if values changed
4. Only changed portions get redrawn, saving processing power
5. Special handling ensures proper display of negative numbers and percentages

## Technical Details
- Uses DOOM's video system (V_DrawPatch, V_CopyRect)
- Coordinates are relative to status bar position (ST_Y)
- Includes error checking for drawing outside bounds
- Efficient redrawing system to minimize graphics updates

## Common Operations
- Drawing numbers digit by digit
- Copying background rectangles for clearing areas
- Drawing patches (images) at specific coordinates
- Tracking old values to minimize redrawing

This code is part of DOOM's user interface system, specifically handling the game's status bar display elements that show important player information during gameplay.
