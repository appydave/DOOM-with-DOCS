# DOOM State Management (doomstat.h/c)

## Overview
These files manage DOOM's global state variables - essentially the "memory" of what's happening in the game at any given moment. Think of it as the game's central nervous system, keeping track of everything from player status to game settings.

## Key Components

### Game Mode Variables
- `gamemode`: Tracks whether you're playing shareware, retail, etc.
- `gamemission`: Identifies which DOOM game is running (DOOM, DOOM II, etc.)
- `modifiedgame`: A flag indicating if custom content (PWAD files) has been added
- `language`: Sets the game's language (default: English)

### Player State
- `players[MAXPLAYERS]`: Array storing data for each player (position, health, etc.)
- `playeringame[]`: Tracks which player slots are active
- `consoleplayer`: ID of the player at the keyboard
- `displayplayer`: ID of the player being shown on screen

### Game Settings
- `gameskill`: Current difficulty level
- `gameepisode`: Current episode number
- `gamemap`: Current map number
- `startskill/startepisode/startmap`: Default values for new games

### Network Game Variables
- `netgame`: True if multiple players are playing
- `deathmatch`: True if playing deathmatch mode
- `doomcom`: Communication interface for network play
- `netbuffer`: Buffer for network data
- `netcmds`: Stores player commands for network sync

### Display State
- `statusbaractive`: Is the status bar being shown?
- `automapactive`: Is the automap visible?
- `menuactive`: Is a menu currently open?
- `paused`: Is the game paused?
- `viewactive`: Is the main view being rendered?

### Sound Settings
- `snd_SfxVolume`: Sound effects volume (0-15)
- `snd_MusicVolume`: Music volume (0-15)
- `snd_MusicDevice`: Current music output device
- `snd_SfxDevice`: Current sound effects device

### Game Statistics
- `totalkills`: Total monsters in level
- `totalitems`: Total collectible items
- `totalsecret`: Total secret areas
- `leveltime`: Time spent in current level

## Technical Details
The header file (doomstat.h) declares these variables as `extern`, meaning they can be accessed from any source file that includes this header. The actual storage for these variables is in doomstat.c.

## Usage Example
When a player picks up a health pack, the game would:
1. Check `playeringame[]` to verify the player is active
2. Access the correct player's data in `players[]`
3. Update their health value
4. If it's a network game (`netgame == true`), sync this change with other players

## For Non-C Programmers
- `extern` variables are like global variables in other languages
- The header file (.h) acts like a table of contents, telling other code what variables exist
- The source file (.c) contains the actual storage space for these variables
