# DOOM Cheat Sequence Handler (m_cheat.c)

## Overview
This file implements the cheat code detection system for DOOM. It provides functionality to check for cheat code sequences entered by the player and retrieve any parameters associated with those cheats. The code is designed to work with a simple but effective pattern matching system that can detect specific sequences of keystrokes.

## Key Components

### Global Variables
- `firsttime`: A static integer flag used to initialize the cheat translation table only once
- `cheat_xlate_table`: An array of 256 unsigned chars that stores the scrambled key mappings

### Data Structures
The code works with a `cheatseq_t` structure (defined elsewhere) that holds:
- A sequence of characters representing the cheat code
- A pointer (p) to track progress through the sequence

### Main Functions

#### cht_CheckCheat
```c
int cht_CheckCheat(cheatseq_t* cht, char key)
```
Purpose: Checks if a pressed key continues or completes a cheat sequence.

Parameters:
- `cht`: Pointer to the cheat sequence structure
- `key`: The key that was just pressed

Returns:
- 1 if the cheat sequence was completed
- 0 if the sequence is incomplete or failed

How it works:
1. On first run, initializes the translation table
2. If sequence hasn't started, points to beginning
3. Compares the pressed key against the expected next character
4. Advances pointer if match, resets if no match
5. Checks for sequence completion (0xff marker)

#### cht_GetParam
```c
void cht_GetParam(cheatseq_t* cht, char* buffer)
```
Purpose: Extracts parameters from a cheat sequence after the trigger sequence.

Parameters:
- `cht`: Pointer to the cheat sequence structure
- `buffer`: Where to store the extracted parameters

How it works:
1. Finds the parameter section (marked by 1)
2. Copies characters until reaching end marker (0xff)
3. Null-terminates the result

## Technical Details
- Uses a scramble table to obscure cheat codes in memory
- Special markers in sequences:
  - 1: Marks start of parameter section
  - 0xff: Marks end of sequence
- Implements a simple state machine for sequence matching

## Usage in DOOM
This code is called by the status bar (st_stuff) module when processing keyboard input. It enables the game to recognize cheat codes like IDDQD, IDKFA, etc., while providing a way to include parameters in some cheats (like level selection).
