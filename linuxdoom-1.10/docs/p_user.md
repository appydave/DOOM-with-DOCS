# Player Movement and State Management (p_user.c)

## Overview
This file handles player-related functionality in DOOM, specifically focusing on player movement, view bobbing (the swaying motion while walking), and state management. It's a crucial part of DOOM's player control system.

## Key Components

### Movement Constants
- `MAXBOB`: Defines maximum view bobbing amplitude (16 pixels)
- `INVERSECOLORMAP`: Index for special visual effects (invulnerability)
- `onground`: Boolean tracking if player is on ground

### Core Functions

#### P_Thrust
Controls player movement in a specific direction.
- **Parameters**: 
  - player: The player to move
  - angle: Direction of movement
  - move: Movement force
- Converts angles to x/y momentum using cosine/sine calculations

#### P_CalcHeight
Manages view height and bobbing effects while moving.
- Calculates walking/running view bob
- Adjusts view height based on player state
- Handles ceiling collision detection
- Uses sine wave for smooth bobbing motion

#### P_MovePlayer
Processes player movement commands.
- Handles forward/backward movement
- Processes side-to-side movement
- Changes player animation state when moving
- Only allows movement control when on ground

#### P_DeathThink
Manages player state when dying.
- Lowers view height to ground
- Handles death animation
- Makes player face their killer
- Allows respawn when use button pressed

#### P_PlayerThink
Main player logic update function.
- Processes movement commands
- Handles weapon changes
- Updates power-up timers
- Manages special effects (invulnerability, infrared vision)
- Controls player-environment interaction

## Technical Concepts
- **Fixed-point Math**: Uses DOOM's fixed-point number system for precise calculations
- **Angle System**: Uses DOOM's angle units (ANG90 = 90 degrees)
- **State Machine**: Manages player states (alive, dead, running, etc.)
- **View Bobbing**: Simulates walking motion through view height oscillation

## Power-ups and Effects
- Invulnerability
- Invisibility
- Infrared Vision
- Radiation Suit (Iron Feet)
- Strength
- Damage counting
- Bonus counting

## Conclusion
This file is central to DOOM's player experience, handling everything from basic movement to complex state management. It creates the characteristic feel of DOOM's player control through careful manipulation of view angles, heights, and movement calculations.
