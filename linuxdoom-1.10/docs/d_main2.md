# DOOM Main Program (d_main.c) Documentation

## Overview
This file contains the main program logic for DOOM, handling game initialization, startup, and the main game loop. It's essentially the "conductor" that coordinates all other parts of the game to work together.

## Key Components

### Game Mode Detection
The code determines which version of DOOM is being run:
- Shareware (free demo version)
- Registered (full version)
- Commercial (DOOM 2)
- Retail (Ultimate DOOM)

### Important Functions

#### D_DoomMain()
The main entry point for DOOM. This function:
1. Processes command line arguments
2. Identifies the game version
3. Initializes all game subsystems (graphics, sound, etc.)
4. Starts either the demo loop or the actual game

#### D_DoomLoop()
The main game loop that runs continuously until the game ends. It:
- Handles frame timing
- Processes player input
- Updates game state
- Renders graphics
- Plays sounds

#### D_Display()
Manages the game's visual output, including:
- Drawing the game world
- Handling screen wipes between levels
- Managing the status bar
- Drawing menus

### Command Line Processing
The code handles various command line options like:
- `-skill` (set difficulty)
- `-episode` (choose episode)
- `-warp` (jump to specific level)
- `-file` (load additional WAD files)
- `-playdemo` (play recorded demos)

### WAD File Management
WAD files are DOOM's data files containing levels, graphics, and sounds. The code:
- Locates WAD files
- Validates their contents
- Loads additional WAD files specified by the player

### Game State Management
Tracks and manages different game states:
- Title screen
- Demo playback
- Active gameplay
- Intermission screens
- Final screens

## Technical Concepts for Non-C Programmers

### Header Files
Lines starting with `#include` load additional code files, similar to importing libraries in other languages.

### Function Pointers
C can store references to functions to call them later, used extensively in the event handling system.

### Memory Management
The code manually manages memory using functions like:
- `malloc()` - Request memory
- `free()` - Release memory
This is different from languages with automatic memory management.

## Conclusion
d_main.c serves as the central coordinator for DOOM, bringing together all the game's components - graphics, sound, input, game logic - into a cohesive whole. It handles initialization, manages the game loop, and ensures all parts of the game work together smoothly.
