# DOOM Heads-Up Display (HUD) Implementation

## Overview
This file (`hu_stuff.c`) implements the heads-up display functionality for DOOM. The HUD includes features like message display, chat system, and map title display. It's a crucial part of DOOM's user interface, handling both single-player messages and multiplayer chat functionality.

## Key Components

### Constants and Data Structures
- Map name arrays for different DOOM versions (shareware, registered, retail, DOOM 2, Plutonia, TNT)
- Character translation tables for French and English keyboard layouts
- HUD positioning constants (e.g., `HU_TITLEX`, `HU_TITLEY`)
- Chat macro definitions and player name arrays

### Global Variables
- `hu_font`: Array of font patches for HUD text
- `chat_on`: Boolean flag for chat mode status
- `message_on`: Boolean flag for message display status
- `headsupactive`: Boolean indicating if HUD is active

### Main Functions

#### HU_Init()
Initializes the HUD system by:
- Setting up character translation tables based on language
- Loading the HUD font graphics from WAD file

#### HU_Start()
Starts the HUD system:
- Initializes message widgets
- Sets up map title display
- Creates chat interface elements
- Called when starting a new game or loading a saved game

#### HU_Drawer()
Renders the HUD elements:
- Draws messages
- Draws chat interface
- Draws map title (when in automap mode)

#### HU_Responder()
Handles user input for the HUD:
- Processes chat commands
- Handles message refresh
- Manages chat macros
- Supports both English and French keyboard layouts

### Chat System
The code includes a comprehensive chat system for multiplayer games:
- Support for broadcast messages
- Player-to-player direct messages
- Chat macros for quick messages
- Queue system for chat characters

## Technical Details

### Character Translation
- Implements keyboard mapping for different languages
- Handles shift-key translations
- Supports special characters for French keyboard layout

### Message Queue
- Uses a circular buffer (QUEUESIZE = 128)
- Implements queue operations (HU_queueChatChar, HU_dequeueChatChar)
- Prevents buffer overflow

## Usage Notes
- The HUD system automatically activates when a game starts
- Chat features only available in multiplayer mode
- Supports up to 4 players (MAXPLAYERS)
- Messages have an automatic timeout (HU_MSGTIMEOUT)

## Integration with DOOM
- Interfaces with DOOM's main game loop
- Uses DOOM's WAD file system for font loading
- Coordinates with sound system for chat notifications
- Integrates with automap display system

This documentation provides a high-level overview of the HUD implementation in DOOM. The code demonstrates sophisticated text handling, input processing, and display management techniques typical of 90s-era game development.
