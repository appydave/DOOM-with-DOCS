# DOOM Menu System (m_menu.c)

## Overview
This file implements DOOM's menu system, including the main menu, options menu, save/load game functionality, and other game settings. It handles all menu-related drawing, user input, and menu state management.

## Key Components

### Menu Structure
The menu system uses two main data structures:
- `menuitem_t`: Represents a single menu item with properties like name, status, and callback routine
- `menu_t`: Represents an entire menu with properties like number of items, position, and drawing routine

### Global State
Important global variables:
- `menuactive`: Tracks if a menu is currently active
- `currentMenu`: Points to the currently active menu
- `itemOn`: Current selected menu item
- `messageString`: Text for popup messages
- `quickSaveSlot`: Slot number for quick save feature

### Main Functions

#### Menu Control
- `M_StartControlPanel()`: Activates the menu system
- `M_ClearMenus()`: Deactivates all menus
- `M_Drawer()`: Main drawing routine for menus
- `M_Responder(event_t* ev)`: Handles all user input for menus

#### Menu Navigation
- `M_SetupNextMenu(menu_t *menudef)`: Changes to a new menu
- `M_StartMessage()`: Shows a popup message
- `M_StopMessage()`: Removes the current message

#### Game Functions
- `M_SaveGame()`: Handles game saving
- `M_LoadGame()`: Handles game loading
- `M_QuickSave()`: Provides quick save functionality
- `M_QuickLoad()`: Loads the last quick saved game

### Menu Types
The file implements several menus:
- Main Menu
- Episode Select
- New Game/Difficulty
- Options Menu
- Sound Settings
- Load/Save Game
- Read This! (Help)

## Technical Details

### Drawing System
- Uses DOOM's patch system for graphics
- Draws menu items vertically with consistent spacing
- Animates a skull cursor for selection

### Input Handling
Supports multiple input methods:
- Keyboard (arrow keys, enter, escape)
- Mouse
- Joystick

### Save System
- Supports 6 save slots
- Allows custom save names
- Implements quick save/load feature

## Conclusion
This file is central to DOOM's user interface, providing all menu functionality and settings management. It demonstrates good separation of concerns between drawing, input handling, and menu logic while maintaining the iconic DOOM interface style.
