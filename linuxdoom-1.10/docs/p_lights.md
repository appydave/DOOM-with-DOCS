# DOOM Lighting Effects System (p_lights.c)

## Overview
This file handles sector-based lighting effects in DOOM, controlling various types of dynamic lighting including flickering lights, flashing lights, and glowing effects. These effects help create the game's atmospheric and dynamic environment.

## Key Concepts
For non-C programmers:
- A "sector" is a basic building block in DOOM's world - an area with a specific floor height, ceiling height, and lighting level
- "Thinkers" are objects that get updated each game tick to handle dynamic behavior
- Light levels in DOOM range from 0 (darkest) to 255 (brightest)

## Light Effect Types

### 1. Fire Flicker Effect
Functions: `T_FireFlicker`, `P_SpawnFireFlicker`
- Simulates the uneven lighting of fire
- Randomly varies light level between a maximum and minimum
- Updates every 4 game ticks
- Minimum light level is calculated based on surrounding sectors

### 2. Broken Light Flash
Functions: `T_LightFlash`, `P_SpawnLightFlash`
- Simulates a malfunctioning light that flashes irregularly
- Alternates between maximum and minimum brightness
- Uses random timing between flashes
- Duration ranges from 1 to 64 game ticks for bright state, 1 to 7 for dim state

### 3. Strobe Light
Functions: `T_StrobeFlash`, `P_SpawnStrobeFlash`, `EV_StartLightStrobing`
- Creates a regular strobing light effect
- Can be configured for fast or slow strobing
- Can be synchronized or randomized
- Often triggered by player actions

### 4. Light Control Functions
Functions: `EV_TurnTagLightsOff`, `EV_LightTurnOn`
- Allow lights in tagged sectors to be turned on or off
- When turning lights on, can either set specific brightness or match brightest neighbor
- Used for switches and triggers in the game

### 5. Glowing Light
Functions: `T_Glow`, `P_SpawnGlowingLight`
- Creates a smoothly changing light level that cycles between bright and dim
- Light level changes gradually by GLOWSPEED units each update
- Changes direction when reaching maximum or minimum levels

## Technical Implementation
The code uses several data structures to manage different light effects:
- `fireflicker_t`: For fire-like flickering
- `lightflash_t`: For broken/flashing lights
- `strobe_t`: For strobe effects
- `glow_t`: For smooth glowing transitions

Each effect type is implemented as a "thinker" that updates on regular game ticks, modifying its sector's light level according to its specific behavior pattern.

## Memory Management
The code uses DOOM's zone memory management system (`Z_Malloc`) to allocate memory for light effects, with the `PU_LEVSPEC` tag indicating the memory should persist for the duration of the current level.

## Integration with Game Engine
Light effects are typically:
1. Spawned during level initialization
2. Updated each game frame through the thinker system
3. Automatically cleaned up when changing levels
4. Can be triggered by player actions or level events

This system provides the dynamic lighting that helps create DOOM's atmospheric and sometimes unsettling environment.
