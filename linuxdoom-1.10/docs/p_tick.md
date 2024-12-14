# DOOM Engine: Thinker and Ticker System (p_tick.c)

## Overview
This file implements DOOM's "thinker" system - a core game engine component that manages game objects that need to be updated each frame (like monsters, doors, etc). It also handles the main game tick logic that updates the game state.

## Key Concepts for Non-C Programmers
- **Thinkers**: Think of these as game objects that need to be "active" and updated each frame. They could be moving platforms, animated doors, monsters, etc.
- **Linked List**: A data structure where each element points to the next one, like a chain. Used here to track all active thinkers.
- **Function Pointers**: Ways to store references to functions that can be called later. Used here to define what action each thinker should take.

## Global Variables
- `leveltime`: Tracks how long the current level has been running in game ticks
- `thinkercap`: Special thinker that acts as both the start and end of the thinker list (forms a circular list)

## Core Functions

### Thinker Management

#### P_InitThinkers
Initializes the thinker list by setting up the circular reference in `thinkercap`.

#### P_AddThinker
Adds a new thinker to the list. Like adding a new active object to the game that needs regular updates.

#### P_RemoveThinker
Marks a thinker for removal by setting its function pointer to -1. The actual removal happens later during P_RunThinkers.

#### P_AllocateThinker
Currently empty - likely meant for future memory allocation of thinkers.

#### P_RunThinkers
The main update loop for all thinkers. For each thinker in the list:
- If marked for removal (-1), removes it and frees its memory
- Otherwise, runs its assigned function

### Game Update Logic

#### P_Ticker
The main game update function that runs each frame. It:
1. Checks if the game is paused
2. Updates all active players
3. Runs all thinkers
4. Updates special effects
5. Handles respawning
6. Increments the level timer

## Technical Details
The thinker system uses a circular doubly-linked list where each thinker points to both the next and previous thinker. This makes adding and removing thinkers efficient.

Memory management is handled through the Z_Zone system (DOOM's memory manager), with thinkers being allocated and freed as needed.

## Common Usage Patterns
1. New game objects that need regular updates are created as thinkers
2. They're added to the list via P_AddThinker
3. Each frame, P_Ticker ensures all active thinkers are updated
4. When objects are no longer needed, they're marked for removal
5. The next update cycle cleans up removed thinkers

This system allows DOOM to efficiently manage hundreds of active game objects while maintaining good performance on 1993-era hardware.
