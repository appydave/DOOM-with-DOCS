# DOOM Renderer Drawing Functions (r_draw.c)

## Overview
This file contains the core drawing functions for DOOM's renderer, specifically handling the drawing of columns and spans which are fundamental to DOOM's graphics engine. It's responsible for rendering walls, floors, ceilings, and special effects like transparency and fuzzy shadows.

## Key Concepts for Non-C Programmers
- **Fixed-point Numbers**: DOOM uses fixed-point arithmetic for precise calculations. These are integers that represent fractional values by treating part of the integer as decimals.
- **Pointers**: Variables that store memory addresses. In this code, they're often used to manipulate screen buffer data directly.
- **Screen Buffer**: A large array of bytes representing the screen, where each byte represents one pixel's color.

## Global Variables and Constants
- `viewimage`: Pointer to the screen buffer
- `viewwidth/viewheight`: Dimensions of the view window
- `SCREENWIDTH/SCREENHEIGHT`: Full screen dimensions
- `SBARHEIGHT`: Height of the status bar (32 pixels)
- `translations`: Color translation tables for player sprites

## Major Functions

### R_DrawColumn
**Purpose**: Draws a vertical column of pixels, primarily used for walls.
- Takes no parameters but uses global variables for state
- Uses fixed-point math for texture coordinate calculations
- Core of DOOM's wall rendering system

### R_DrawSpan
**Purpose**: Draws horizontal spans of pixels, used for floors and ceilings.
- Uses global variables for coordinates and texture information
- Performs texture mapping with perspective correction
- Critical for rendering floor and ceiling textures

### R_DrawFuzzColumn
**Purpose**: Creates the transparent/fuzzy effect used for spectres.
- Implements a simple pixel-offsetting algorithm
- Creates a shimmer effect by sampling adjacent pixels
- Uses a pre-defined fuzz table for offset patterns

### R_InitBuffer
**Purpose**: Sets up the screen buffer and viewing window.
- Calculates column offsets for efficient rendering
- Handles different view window sizes
- Creates lookup tables to avoid multiplication during rendering

### R_FillBackScreen
**Purpose**: Draws the background pattern and beveled edges around the view window.
- Only used when view window is smaller than screen
- Draws decorative borders around the game view
- Uses DOOM's patch system for border graphics

## Special Effects
1. **Color Translation**
   - Used for different colored player sprites
   - Remaps specific color ranges to create different appearances

2. **Fuzzy Effect**
   - Creates semi-transparent appearance
   - Used for invisible enemies and certain powerups

## Memory Management
- Uses DOOM's zone memory system (Z_Malloc)
- Careful management of screen buffers
- Pre-calculated lookup tables for performance

## Optimization Techniques
1. Fixed-point arithmetic instead of floating-point
2. Lookup tables for quick calculations
3. Direct memory manipulation for speed
4. Unrolled loops in critical sections (commented out versions preserved)

## Conclusion
This file is central to DOOM's rendering system, handling the core drawing operations that create the game's distinctive visual style. It emphasizes performance through careful optimization while maintaining the flexibility needed for various visual effects.
