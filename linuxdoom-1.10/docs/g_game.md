# DOOM Game Logic (g_game.c)

## Overview
This file contains the core game logic for DOOM, handling everything from player movement and controls to demo recording/playback and save game functionality. It serves as the main coordinator between player inputs, game state, and the various subsystems that make DOOM work.

## Key Components

### Game State Management
The code maintains several critical game state variables:
- `gameaction`: Pending game action (loading level, starting new game, etc.)
- `gamestate`: Current state (level running, intermission, etc.) 
- `gameskill`: Difficulty level
- `gameepisode` and `gamemap`: Current episode and map numbers
- `usergame`: Whether playing a normal game vs demo
- `paused`: Game pause state

### Player Data
- Tracks up to 4 players (`MAXPLAYERS`)
- Maintains player states, scores, and statistics
- Handles respawning and level transitions

### Control Systems
Processes inputs from:
- Keyboard
- Mouse 
- Joystick
These are combined into `ticcmd_t` structures that represent player actions each game tick.

## Major Functions

### Game Initialization
- `G_InitNew()`: Starts a new game with specified skill/episode/map
- `G_DoNewGame()`: Handles new game startup sequence
- `G_InitPlayer()`: Sets up initial player state

### Game Loop
- `G_Ticker()`: Main game tick processing
- `G_BuildTiccmd()`: Builds command structure from player inputs
- `G_Responder()`: Handles input events

### Save/Load System
- `G_DoSaveGame()`: Saves current game state
- `G_DoLoadGame()`: Restores saved game
- Uses a custom serialization format to store game state

### Demo System
- `G_RecordDemo()`: Starts demo recording
- `G_PlayDemo()`: Plays back recorded demo
- Demos store player inputs to perfectly recreate gameplay

### Level Management  
- `G_DoLoadLevel()`: Loads and initializes a new level
- `G_DoCompleted()`: Handles level completion
- `G_WorldDone()`: Processes world/episode completion

## Technical Details

### Game Ticks
The game runs on a fixed tick rate system where each tick:
1. Processes player inputs
2. Updates game state
3. Handles movement and collision
4. Updates all active entities ("thinkers")

### State Transitions
The code carefully manages transitions between different game states:
- Playing levels
- Intermission screens
- Finale sequences
- Menu system

### Demo Format
Demos are stored as:
1. Header with game version and settings
2. Series of compressed input commands
3. Special marker for demo end

## Conclusion
This file is the heart of DOOM's gameplay systems, coordinating all the pieces that make the game work. It translates raw player inputs into game actions, manages the flow between levels, handles saving/loading, and ensures everything stays synchronized in both single player and network games.
