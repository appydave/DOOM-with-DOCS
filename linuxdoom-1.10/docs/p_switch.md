# DOOM Switch and Button Handler (p_switch.c)

## Overview
This file handles the logic for switches and buttons in DOOM - interactive wall elements that players can use to trigger various effects in the game world. It manages texture changes for switches, button timing, and processes different types of special actions when switches are activated.

## Key Components

### Switch List Data Structure
The code maintains a list of switch textures in `alphSwitchList`, containing:
- Pairs of texture names (on/off states)
- Episode number where each switch appears
- Organized by game version (shareware, registered, DOOM II)

### Global Variables
- `switchlist`: Array storing texture numbers for switches
- `numswitches`: Total number of switch pairs
- `buttonlist`: Array tracking active button states

## Core Functions

### P_InitSwitchList
Initializes the switch system at game start:
- Determines which switches to include based on game episode
- Converts texture names to texture numbers
- Sets up the runtime switch list

### P_StartButton
Manages button activation:
- Parameters:
  - `line`: The triggering line
  - `w`: Where on wall (top/middle/bottom)
  - `texture`: Button texture
  - `time`: How long button stays pressed
- Prevents double-activation of buttons
- Sets up button timer and sound origin

### P_ChangeSwitchTexture
Handles the visual change when switches are activated:
- Changes wall texture between on/off states
- Plays appropriate sound effect
- Special handling for exit switches
- Can set up button timer for reusable switches

### P_UseSpecialLine
Main function for processing switch/button actions:
- Extensive switch statement handling different line types
- Actions include:
  - Door controls (open/close/locked)
  - Floor movement
  - Ceiling effects
  - Platform control
  - Light changes
  - Level exits

## Special Effects
The code can trigger various world changes:
- Building stairs
- Moving floors/ceilings
- Operating doors
- Controlling platforms
- Changing light levels
- Triggering exits

## Technical Notes
- Uses texture system for visual feedback
- Integrates with sound system for switch effects
- Coordinates with other game systems (doors, platforms, etc.)
- Handles both one-time switches and reusable buttons

## Summary
This code is central to DOOM's interactive environment, managing the player's ability to affect the game world through switches and buttons. It bridges the gap between player input and game world changes, handling both the visual feedback and actual effects of switch activation.
