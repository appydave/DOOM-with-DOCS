# Random Number Generation in DOOM

## Overview
This file (`m_random.c`) implements DOOM's random number generation system. It provides a simple but effective way to generate pseudo-random numbers between 0 and 255 using a lookup table approach rather than complex mathematical calculations.

## Key Components

### Random Number Table
The code uses a pre-defined lookup table (`rndtable`) containing 256 numbers. This table stores predetermined "random" values that the game cycles through. Think of it like a deck of cards with numbers that you keep shuffling through.

### Global Variables
- `rndindex`: Tracks the current position in the random table for general game use
- `prndindex`: Tracks the current position for predictable game events (like enemy behavior)

## Functions

### M_Random()
- **Purpose**: Generates random numbers for general game use
- **How it works**: 
  1. Increments the index counter (`rndindex`)
  2. Wraps the counter back to 0 if it reaches 256 (using `&0xff`)
  3. Returns the number from the lookup table at that position
- **Returns**: A number between 0 and 255

### P_Random()
- **Purpose**: Generates "predictable" random numbers for game mechanics
- **How it works**: Similar to M_Random(), but uses a separate index (`prndindex`)
- **Used for**: Game elements that need to be consistent/reproducible, like enemy behavior
- **Returns**: A number between 0 and 255

### M_ClearRandom()
- **Purpose**: Resets both random number generators
- **How it works**: Sets both index counters back to 0
- **When used**: Typically when starting a new game or needing to reset randomization

## Technical Implementation
The code uses bitwise operations (`&0xff`) to wrap numbers back to the range 0-255. This is more efficient than using modulo arithmetic (`% 256`).

## Why Two Random Number Generators?
DOOM uses two separate random number sequences:
1. One for general randomization (M_Random)
2. One for gameplay elements that need to be predictable/reproducible (P_Random)

This dual system ensures that certain game elements remain consistent while still allowing for random variety in other aspects of the game.
