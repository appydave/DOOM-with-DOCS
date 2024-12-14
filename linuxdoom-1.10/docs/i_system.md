# DOOM System Interface (i_system.c)

## Overview
This file implements the core system interface for DOOM, handling essential low-level operations like memory management, timing, error handling, and system initialization/shutdown. It serves as a bridge between DOOM's game logic and the underlying operating system.

## Key Components

### Memory Management Functions
- `I_GetHeapSize()`: Returns the size of available memory (6MB)
- `I_ZoneBase()`: Allocates the main memory zone for DOOM
- `I_AllocLow()`: Allocates and clears a block of memory

### Timing Functions
- `I_GetTime()`: Returns game time in 1/70th second tics
- `I_WaitVBL()`: Waits for vertical blank (platform-specific delay)

### System Control Functions
- `I_Init()`: Initializes sound and graphics systems
- `I_Quit()`: Performs clean shutdown of the game
  - Saves settings
  - Shuts down networking, sound, music, and graphics
  - Exits the program

### Error Handling
- `I_Error()`: Handles fatal errors
  - Prints error message to stderr
  - Performs cleanup
  - Terminates program

### Unused/Placeholder Functions
- `I_Tactile()`: Stub for tactile feedback (unused)
- `I_BaseTiccmd()`: Returns empty command structure
- `I_BeginRead()`/`I_EndRead()`: Empty functions for reading operations

## Technical Details
- Uses UNIX system calls (gettimeofday, usleep)
- Platform-specific implementations for Sun and SGI systems
- Default memory allocation of 6MB (mb_used variable)
- Integrates with DOOM's networking (D_QuitNetGame) and game state (G_CheckDemoStatus)

## Usage in DOOM
This system interface is fundamental to DOOM's operation, providing:
- Memory management for game resources
- Precise timing for game updates
- Error handling and graceful shutdown
- Platform abstraction layer

The code demonstrates classic id Software's approach to cross-platform game development in the early 1990s.
