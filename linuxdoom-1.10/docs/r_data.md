# DOOM Renderer Data Management (r_data.c)

## Overview
This file is a critical component of DOOM's rendering system, handling the preparation and management of graphical data used for rendering the game world. It deals with textures, sprites, and color maps that make up DOOM's visual elements.

## Key Concepts

### Texture System
DOOM uses a composite texture system where:
- Textures are built from one or more "patches" (smaller images)
- Textures are stored in vertical columns for efficient rendering
- The system supports both wall textures and flat textures (for floors/ceilings)

### Data Structures

#### Texture Definitions
```c
typedef struct {
    char name[8];
    boolean masked;
    short width;
    short height;
    void **columndirectory;
    short patchcount;
    mappatch_t patches[1];
} maptexture_t;
```
This structure defines how textures are composed from patches.

### Major Functions

#### R_InitTextures()
- Purpose: Initializes the texture system
- Loads texture definitions from TEXTURE1/TEXTURE2 lumps
- Creates lookup tables and allocates memory for textures
- Sets up texture translation tables for animations

#### R_GenerateComposite()
- Purpose: Builds a composite texture from its component patches
- Takes individual patches and combines them into a complete texture
- Handles proper positioning and overlapping of patches

#### R_GetColumn()
- Purpose: Retrieves a column of texture data for rendering
- Handles both simple and composite textures
- Returns cached data when possible

#### R_PrecacheLevel()
- Purpose: Pre-loads all graphics needed for a level
- Loads textures, flats, and sprites used in the current level
- Optimizes performance by having data ready in memory

## Memory Management
The code uses DOOM's zone memory allocator (Z_Malloc) for dynamic memory allocation. Different memory tags (PU_STATIC, PU_CACHE) are used to manage the lifetime of allocated memory.

## Technical Details
- Supports both shareware (TEXTURE1) and commercial (TEXTURE1+TEXTURE2) texture sets
- Uses a column-based drawing system for efficient rendering
- Implements texture caching to improve performance
- Handles texture name lookups and error checking

## Conclusion
This file is fundamental to DOOM's rendering system, managing all the graphical assets needed to display the game world. It implements an efficient texture management system that was quite advanced for its time (1993), allowing for detailed textures while working within the memory constraints of period hardware.
