# DOOM X11 Video Implementation (i_video.c)

## Overview
This file implements DOOM's graphics system for Unix/Linux systems using the X11 windowing system. It handles creating the game window, managing the display buffer, handling keyboard/mouse input, and rendering the game graphics to the screen.

## Key Components

### Display Setup
- Uses X11 library to create and manage the game window
- Supports different screen multiplication factors (1x, 2x, 3x, 4x)
- Implements MIT-SHM (Shared Memory) extension for faster graphics performance
- Handles color palette management for 256-color display

### Major Functions

#### I_InitGraphics()
Creates and initializes the X11 window and graphics context.
- Sets up the display connection
- Creates the game window
- Initializes shared memory if available
- Sets up color management
- Handles mouse grabbing (if requested)

#### I_FinishUpdate()
Updates the screen with new frame data.
- Handles different screen multiplication modes
- Manages the shared memory buffer updates
- Synchronizes with X server
- Draws performance dots if developer mode is enabled

#### I_GetEvent()
Processes X11 input events.
- Handles keyboard input
- Processes mouse movement and buttons
- Translates X11 events to DOOM's internal event system

#### I_ShutdownGraphics()
Cleans up graphics resources when shutting down.
- Detaches shared memory
- Releases allocated memory

### Important Variables
- `X_display`: Connection to X11 server
- `X_mainWindow`: Main game window
- `multiply`: Screen size multiplier (1-4)
- `image`: X11 image buffer for rendering
- `screens[0]`: DOOM's main screen buffer

### Technical Details

#### Shared Memory Implementation
The code uses MIT-SHM extension when available for better performance:
- Checks if running on local display
- Allocates shared memory segment
- Attaches memory to both process and X server

#### Color Management
- Uses 256-color palette mode
- Implements gamma correction
- Handles dynamic palette updates

#### Screen Scaling
Supports multiple scaling modes:
- 1x: Original size
- 2x: Double size with pixel doubling
- 3x: Triple size with pixel tripling
- 4x: Quadruple size (noted as "broken" in comments)

## Usage Notes
- Command line options:
  - `-2`, `-3`, `-4`: Select screen multiplication factor
  - `-grabmouse`: Lock mouse to game window
  - `-disp`: Specify X11 display
  - `-geom`: Set window geometry

## Error Handling
- Checks for X11 connection failures
- Validates visual mode support (requires 256-color PseudoColor)
- Handles shared memory allocation failures

## Limitations
- Only supports 256-color PseudoColor visual
- 4x scaling mode is marked as broken
- Mouse handling without DGA extension is imperfect
