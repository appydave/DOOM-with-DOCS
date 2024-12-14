# DOOM Enemy AI and Behavior System (p_enemy.c)

## Overview
This file contains the core enemy artificial intelligence (AI) and behavior system for DOOM. It handles how monsters think, move, attack, and react to players and other stimuli in the game world.

## Key Components

### Enemy Movement System
- Implements 8-directional movement using `dirtype_t` enum (EAST, NORTHEAST, NORTH, etc.)
- Uses lookup tables (`xspeed`, `yspeed`) for movement calculations
- Handles collision detection and path finding through `P_Move` and `P_TryWalk` functions

### Enemy AI States
The file implements several key AI behaviors:
1. **Looking** (`A_Look`): Monsters searching for players
2. **Chasing** (`A_Chase`): Movement toward targets
3. **Attacking** (`A_*Attack` functions): Various attack patterns
4. **Death** (`A_Fall`, `A_XScream`, etc.): Death behaviors

### Sound Alert System
- `P_NoiseAlert`: Allows monsters to alert others when they spot a player
- `P_RecursiveSound`: Propagates sound through connected sectors
- Handles sound blocking by walls and doors

### Boss-Specific Behaviors
- Special routines for major bosses (Spider Mastermind, Cyberdemon, etc.)
- `A_BossDeath`: Handles special events when bosses die
- Level-specific triggers and events

## Key Functions

### Core AI Functions
- `P_LookForPlayers`: Basic player detection
- `P_CheckSight`: Line-of-sight checking
- `P_Move`: Basic movement implementation
- `P_NewChaseDir`: Pathfinding logic

### Attack Functions
- `A_FaceTarget`: Turns monster to face their target
- `A_SkullAttack`: Lost Soul's charging attack
- `A_PainAttack`: Pain Elemental's soul-spawning attack
- Various weapon attacks (BFG, plasma, etc.)

### Special Monster Behaviors
- `A_VileChase`: Archvile's resurrection ability
- `A_BrainSpit`: Boss brain's cube-spawning attack
- `A_SpawnFly`: Handles spawned monster behavior

## Technical Notes
- Uses fixed-point math for precise positioning
- Implements A* pathfinding principles in a simplified form
- Handles monster state machines through function pointers
- Coordinates with sound and rendering systems

## Conclusion
This file is central to DOOM's famous monster AI system. While simple by modern standards, it creates engaging enemy behaviors through a combination of basic pathfinding, state machines, and specialized monster abilities.
