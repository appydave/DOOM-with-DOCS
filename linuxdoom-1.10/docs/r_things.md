# DOOM Sprite Rendering System (r_things.c)

## Overview
This file contains the core sprite rendering logic for DOOM. It handles drawing all movable objects (monsters, items, weapons) in the game world. The code manages both the sprites visible in the 3D world and the player's weapon sprites shown at the bottom of the screen.

## Key Concepts
For non-C programmers, here are some important concepts used throughout this code:
- **Sprites**: 2D images that represent game objects from different angles
- **Vissprites**: "Visible sprites" - sprites that are potentially visible in the current frame
- **Fixed-point arithmetic**: Used for precise calculations without floating point math
- **BSP**: Binary Space Partitioning, used for determining what's visible

## Major Components

### Data Structures
- `vissprite_t`: Represents a sprite that might be visible in the current frame
- `maskdraw_t`: Used for masked texture drawing operations
- `spritedef_t`: Defines a sprite's complete set of frames
- `spriteframe_t`: Represents a single frame of a sprite

### Key Global Variables
- `vissprites[]`: Array of potentially visible sprites
- `spritelights`: Lighting level lookup tables
- `sprites`: Array of all sprite definitions
- `numsprites`: Total number of sprite definitions

### Main Functions

#### R_InitSprites
Purpose: Initializes the sprite rendering system at game startup
- Takes a list of sprite names
- Sets up sprite rotation matrices
- Handles flipped sprites

#### R_ProjectSprite
Purpose: Determines if a game object's sprite should be visible
- Transforms sprite coordinates relative to viewer
- Checks if sprite is in view
- Creates vissprite entries for visible sprites

#### R_DrawPlayerSprites
Purpose: Handles drawing the player's weapon
- Manages weapon bobbing
- Handles weapon transparency
- Applies appropriate lighting

#### R_DrawMasked
Purpose: Main entry point for sprite rendering
- Sorts visible sprites by distance
- Draws sprites from back to front
- Handles masked mid-textures
- Draws player weapon last

### Rendering Process
1. Each frame, the engine clears the vissprite list
2. During BSP traversal, potentially visible sprites are added
3. Sprites are sorted by distance from viewer
4. Sprites are drawn from farthest to nearest
5. Player's weapon sprite is drawn last

## Technical Details

### Sprite Rotation
- Sprites can have 8 rotations (viewing angles)
- Rotation 0 faces the viewer
- Rotations proceed clockwise
- Some sprites use a single rotation for all angles

### Clipping
The code handles several types of clipping:
- View frustum clipping (sprites outside view angle)
- Distance clipping (too far/near)
- BSP-based occlusion
- Screen bounds clipping

### Memory Management
- Sprites are cached from WAD file
- Visible sprite list is reset each frame
- Uses DOOM's zone memory system

## Conclusion
This file is central to DOOM's visual presentation, handling all movable object rendering. It demonstrates sophisticated 3D graphics techniques while working within the constraints of 1993 hardware, using clever optimizations like fixed-point math and pre-computed tables.
