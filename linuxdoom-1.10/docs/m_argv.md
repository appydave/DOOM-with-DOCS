# Command Line Argument Handler (m_argv.c)

## Overview
This file provides functionality for handling command line arguments in the DOOM game engine. It offers a simple way to check if specific parameters were provided when launching the program.

## Code Structure

### Global Variables
- `myargc`: An integer storing the total number of command line arguments
- `myargv`: A pointer to an array of strings (char**) containing the actual command line arguments

### Functions

#### M_CheckParm
```c
int M_CheckParm(char *check)
```
This function searches through command line arguments for a specific parameter.

**Parameters:**
- `check`: The string to search for in the command line arguments

**Returns:**
- The position (1 to argc-1) where the parameter was found
- 0 if the parameter wasn't found

**How it works:**
1. Loops through all command line arguments (starting at 1 to skip the program name)
2. Compares each argument with the search string (case-insensitive)
3. Returns the position if found, or 0 if not found

## Usage Example
If DOOM was launched with: `./doom -nomonsters -skill 4`
- `M_CheckParm("-nomonsters")` would return the position where "-nomonsters" appears
- `M_CheckParm("-notexist")` would return 0

## Technical Notes
- Uses `strcasecmp()` for case-insensitive string comparison
- Arguments are numbered starting from 1 (index 0 contains the program name)
- Part of DOOM's modular architecture, indicated by the 'm_' prefix

## Integration with DOOM
This module is used throughout DOOM to check for various command line options that modify game behavior, such as:
- Skill levels
- Warp commands
- Debug options
- Game modifications
