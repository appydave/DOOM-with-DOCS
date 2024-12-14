# Video Drawing System (v_video.c)

## Overview
This file is part of the DOOM source code and handles the game's video drawing functionality. It provides functions for drawing graphics to the screen, managing gamma correction, and handling screen updates. The code is responsible for fundamental graphics operations like drawing patches (sprites/textures) and copying rectangular blocks of pixels.

## Key Components

### Screen Buffers
- The game maintains 5 screen buffers (`screens[5]`), each representing a full screen's worth of pixels
- Screen dimensions are defined by `SCREENWIDTH` and `SCREENHEIGHT`
- A "dirty box" system (`dirtybox[4]`) tracks which areas of the screen need updating

### Gamma Correction
- Implements gamma correction using lookup tables (`gammatable[5][256]`)
- 5 different gamma levels available for brightness adjustment
- Each table maps input colors (0-255) to adjusted output colors

## Main Functions

### V_MarkRect(x, y, width, height)
Marks a rectangular area of the screen as needing to be updated.
- Parameters: x/y coordinates, width/height of rectangle
- Used internally to track which parts of screen need redrawing

### V_CopyRect(srcx, srcy, srcscrn, width, height, destx, desty, destscrn)
Copies a rectangular area from one screen buffer to another.
- Useful for copying background elements or implementing split-screen effects
- Performs bounds checking in debug builds

### V_DrawPatch(x, y, scrn, patch)
Core drawing function for game sprites and textures.
- Draws a "patch" (DOOM's sprite format) to the screen
- Handles transparency and offset positioning
- Complex function that processes column-based image data

### V_DrawPatchFlipped(x, y, scrn, patch)
Similar to V_DrawPatch but mirrors the image horizontally.
- Used for mirror effects, particularly for face sprites

### V_DrawBlock(x, y, scrn, width, height, src)
Draws a simple rectangular block of pixels.
- Direct memory copy without transparency
- Used for full-screen updates or simple rectangular graphics

### V_GetBlock(x, y, scrn, width, height, dest)
Copies a rectangular area from screen to memory.
- Reverse of V_DrawBlock
- Used for saving portions of the screen

### V_Init()
Initialization function that:
- Allocates memory for screen buffers
- Sets up the basic video system
- Called once at game startup

## Technical Notes
- Uses direct memory access for performance
- Implements safety checks with `RANGECHECK` define
- Heavily optimized for the hardware of its era (1993)
- Uses byte-level operations for pixel manipulation

## Memory Management
- Screen buffers are allocated in low memory for DOS compatibility
- Each screen buffer is `SCREENWIDTH * SCREENHEIGHT` bytes
- Total of 4 screen buffers for various rendering purposes

This code represents a fundamental part of DOOM's graphics system, handling everything from basic pixel operations to complex sprite rendering. While some concepts (like patches and screen buffers) are DOOM-specific, the underlying principles of graphics programming remain relevant today.
