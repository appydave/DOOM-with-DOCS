# DOOM String Handling System

## Overview
The DOOM string handling system consists of three key files that manage text messages and strings used throughout the game:

- `dstrings.h` - Main string definitions header
- `d_englsh.h` - English language strings
- `d_french.h` - French language strings

This system enables DOOM to support multiple languages and centralizes all game text in one place.

## String Organization

### Message Categories
The strings are organized into several categories:

1. System Messages
   - Development mode notifications
   - CD-ROM related messages

2. Menu Text
   - Quit messages
   - Save/Load prompts
   - Difficulty selection
   - Graphics settings

3. Gameplay Messages
   - Item pickup notifications
   - Key card requirements
   - Level names
   - Chat macros
   - Status messages

4. Story Text
   - Episode completion text
   - Level transition narratives
   - Secret level messages

### Language Support
The game uses conditional compilation to switch between languages:
```c
#ifdef FRENCH
#include "d_french.h"
#else
#include "d_englsh.h"
#endif
```

## Key Components

### Quit Messages
The game features multiple quit messages stored in an array:
```c
char* endmsg[NUM_QUITMESSAGES+1]
```
These messages are randomly selected when the player attempts to quit the game.

### Level Names
Each level has a unique identifier and name:
- Episode 1: E1M1 through E1M9
- Episode 2: E2M1 through E2M9
- Episode 3: E3M1 through E3M9
- Episode 4: E4M1 through E4M9

Example:
```c
#define HUSTR_E1M1 "E1M1: Hangar"
```

### Character Names
The game includes names for all characters that appear in the end credits:
```c
#define CC_ZOMBIE "ZOMBIEMAN"
#define CC_DEMON  "DEMON"
```

## Usage Notes

1. String Constants
   - All strings are defined as preprocessor macros
   - This allows easy language switching without code changes
   - Maintains consistent text throughout the game

2. Text Formatting
   - Uses '\n' for line breaks
   - Some messages include formatting placeholders
   - Special characters are escaped properly

3. Story Text
   - Long narrative texts use multiple concatenated strings
   - Maintains readability in source code
   - Allows for proper text wrapping in-game

## Implementation Details

The string system is designed to be:
- Memory efficient (uses preprocessor definitions)
- Easy to maintain (centralized string storage)
- Language-flexible (supports multiple language files)
- Consistent (standardized naming conventions)

## Technical Notes

1. Header Guards
   - Each header file uses include guards
   - Prevents multiple inclusion
   - Example: `#ifndef __DSTRINGS__`

2. Naming Conventions
   - HUSTR_: HUD (Heads Up Display) strings
   - STSTR_: Status strings
   - AMSTR_: Automap strings
   - CC_: Character cast strings

3. String Storage
   - No runtime string allocation
   - All strings are compile-time constants
   - Reduces memory management overhead

## Conclusion

The DOOM string handling system demonstrates effective text management in a large game project through:
- Centralized string management
- Multi-language support
- Organized categorization
- Efficient memory usage

This design has influenced many subsequent games and remains a good example of practical string handling in C game development.
