# DOOM Sound System Data Structures

## Overview
This file contains the core data structures that define DOOM's music and sound effect (SFX) catalog. It serves as a comprehensive registry of all audio assets used in the game, including both music tracks and sound effects.

## Music System
The file defines an array `S_music[]` containing information about all music tracks in the game. Each entry represents a single music track with:
- A unique identifier (like "e1m1" for Episode 1 Map 1's music)
- A handle field (initialized to 0)

The music tracks are organized by:
- Episode/map themes (e1m1 through e3m9)
- Special event music (intermission, intro, victory)
- DOOM II specific tracks

## Sound Effects System
The `S_sfx[]` array defines all sound effects in the game. Each sound effect entry contains:
- Name: A unique identifier (like "pistol", "shotgn")
- Singularity flag: Indicates if multiple instances can play simultaneously
- Priority: Volume/importance level (0-127)
- Link: Pointer to linked sounds (used for variations)
- Pitch start/end: Pitch modification range
- Volume: Sound volume level

Sound effects are categorized into:
- Weapon sounds (pistol, shotgun, etc.)
- Door/environment sounds
- Monster vocals (pain, death, active)
- Player sounds
- Item pickup effects
- Special effects

## Technical Implementation
The data is structured using two main arrays:
1. `musicinfo_t S_music[]`: Music track registry
2. `sfxinfo_t S_sfx[]`: Sound effects registry

Each sound effect entry is carefully tuned with specific priority levels and flags to ensure proper playback in the game engine.

## Usage Notes
- Sound effect entry 0 is a dummy entry required by the engine
- Some sounds are linked (like the chaingun using the pistol sound)
- Priority values determine which sounds take precedence during busy gameplay
- Singularity flags prevent sound effect overlap when needed

This file serves as a critical reference for DOOM's audio system, defining the complete sound palette available to the game engine.
