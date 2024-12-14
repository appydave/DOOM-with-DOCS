# DOOM Heads-Up Display Library (hu_lib.c)

## Overview
This file contains the implementation of DOOM's heads-up display (HUD) text handling system. It provides functionality for drawing and managing text on the screen, including both static text and user input handling. This is a crucial part of DOOM's user interface, handling everything from status messages to text input.

## Key Components

### Text Line Management
The code manages three main types of text structures:
- Simple text lines (hu_textline_t)
- Scrolling text (hu_stext_t) 
- Input text (hu_itext_t)

### Important Functions

#### Basic Text Line Operations
- `HUlib_init()`: Initializes the HUD library
- `HUlib_clearTextLine()`: Clears a text line
- `HUlib_initTextLine()`: Sets up a new text line with position and font
- `HUlib_addCharToTextLine()`: Adds a character to a text line
- `HUlib_delCharFromTextLine()`: Removes a character from a text line

#### Drawing Functions
- `HUlib_drawTextLine()`: Renders a line of text on screen
- `HUlib_eraseTextLine()`: Erases a line of text from screen

#### Scrolling Text Functions
- `HUlib_initSText()`: Initializes scrolling text
- `HUlib_addLineToSText()`: Adds a new line to scrolling text
- `HUlib_addMessageToSText()`: Adds a message with optional prefix
- `HUlib_drawSText()`: Draws scrolling text
- `HUlib_eraseSText()`: Erases scrolling text

#### Input Text Functions
- `HUlib_initIText()`: Initializes input text
- `HUlib_keyInIText()`: Handles keyboard input
- `HUlib_drawIText()`: Draws input text
- `HUlib_eraseIText()`: Erases input text

## Technical Details

### Text Rendering
Text is rendered using patch_t structures (DOOM's sprite/texture format). Characters are drawn individually using V_DrawPatchDirect(). The code supports:
- Upper case characters only
- Basic cursor display
- Screen boundary checking
- Automatic text wrapping

### Memory Management
The code uses fixed-size buffers for text storage with a maximum line length (HU_MAXLINELENGTH). No dynamic memory allocation is used, which is typical for games of this era.

### Screen Updates
The code includes optimization features:
- Selective updates (needsupdate flag)
- Automap awareness
- Screen boundary checking
- View window consideration

## Usage Example
To display a message on screen:
1. Initialize a text line with `HUlib_initTextLine()`
2. Add characters with `HUlib_addCharToTextLine()`
3. Draw it with `HUlib_drawTextLine()`
4. Erase when needed with `HUlib_eraseTextLine()`

## Integration with DOOM
This library is used for:
- Game messages
- Menu text
- Status information
- Player chat
- Console input

## Notes for Non-C Programmers
- The code uses extensive pointer manipulation, typical in C
- Boolean values are implemented as integers (0 = false, non-zero = true)
- Functions often return boolean values to indicate success/failure
- The code assumes a specific screen layout and coordinate system
