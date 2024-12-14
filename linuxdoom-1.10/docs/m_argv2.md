# Command Line Argument Handler (m_argv.h)

## Overview
This header file defines the interface for handling command line arguments in DOOM. It provides access to the program's command line arguments and functionality to search through them.

## Global Variables
- `myargc`: An integer storing the count of command line arguments
- `myargv`: A pointer to an array of strings (char**) containing the actual command line arguments

## Functions

### M_CheckParm
```c
int M_CheckParm (char* check)
```
This function searches through the command line arguments for a specific parameter.
- **Input**: A string to search for in the arguments
- **Returns**: The position (index) of the parameter if found, or 0 if not found
- **Usage**: Used throughout DOOM to check if specific command line options were provided

## Usage in DOOM
This header is fundamental to DOOM's startup process, allowing the game to process command line options that control various aspects of the game's behavior. Other parts of the engine use these functions to check for specific parameters that affect their operation.
