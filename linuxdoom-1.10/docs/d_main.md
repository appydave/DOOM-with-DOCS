# DOOM Main Game Control (d_main.h)

## Overview
This header file defines the core game control interfaces for DOOM, including initialization, main game loop control, and WAD file handling.

## Constants
- `MAXWADFILES`: Maximum number of WAD files (20) that can be loaded simultaneously

## Global Variables
- `wadfiles`: An array of strings storing paths to WAD files to be loaded

## Key Functions

### D_DoomMain
```c
void D_DoomMain (void)
```
The main entry point for DOOM's game logic. This function:
- Initializes all game subsystems
- Processes command line parameters
- Starts the main game loop

### D_AddFile
```c
void D_AddFile (char *file)
```
Adds a WAD file to the list of files to be loaded.
- **Input**: Path to a WAD file
- **Usage**: Called during startup to queue WAD files for loading

### D_PostEvent
```c
void D_PostEvent (event_t* ev)
```
Handles input events from the I/O system.
- **Input**: Pointer to an event structure
- **Purpose**: Routes input events into the game engine

### Game State Control Functions
- `D_PageTicker`: Updates the demo/title page timer
- `D_PageDrawer`: Draws the current page (demo/title)
- `D_AdvanceDemo`: Moves to the next demo sequence
- `D_StartTitle`: Initiates the title screen sequence

## Usage in DOOM
This header defines the high-level control flow of the DOOM engine, managing the game's initialization, main loop, and state transitions. It serves as the primary interface between the system-level code and the game logic.
