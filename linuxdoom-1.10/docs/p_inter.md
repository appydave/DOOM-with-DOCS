# DOOM Interaction Handler (p_inter.c)

## Overview
This file handles interactions between game objects in DOOM, particularly collisions and their effects. It manages crucial gameplay mechanics like picking up items, taking damage, and handling player death.

## Key Components

### Constants and Global Variables
- `BONUSADD`: Bonus count increment (6)
- `maxammo`: Maximum ammunition limits for different weapon types
- `clipammo`: Ammunition per clip for different weapon types

### Core Functions

#### Item Collection Functions

##### P_GiveAmmo
- **Purpose**: Gives ammunition to a player
- **Parameters**: 
  - player: The player receiving ammo
  - ammo type: Kind of ammunition
  - num: Number of clip loads
- **Behavior**: 
  - Checks ammo limits
  - Doubles ammo in baby/nightmare skill levels
  - May trigger weapon switching if previously empty

##### P_GiveWeapon
- **Purpose**: Gives a weapon to a player
- **Handles**: 
  - Different behavior for multiplayer/singleplayer
  - Ammunition with weapon pickup
  - Network game considerations

##### P_GiveBody
- **Purpose**: Heals the player
- **Limits**: Cannot exceed MAXHEALTH

##### P_GiveArmor
- **Purpose**: Provides armor protection
- **Behavior**: Only gives armor if better than current

#### Combat Functions

##### P_DamageMobj
- **Purpose**: Core damage handling system
- **Parameters**:
  - target: Object receiving damage
  - inflictor: Object causing damage
  - source: Responsible entity
  - damage: Amount of damage
- **Features**:
  - Armor calculation
  - God mode checking
  - Death handling
  - Damage feedback
  - AI reaction triggering

##### P_KillMobj
- **Purpose**: Handles entity death
- **Features**:
  - Kill counting
  - Item dropping
  - State changes
  - Player death specifics

#### Special Item Handling

##### P_TouchSpecialThing
- **Purpose**: Handles pickup item collisions
- **Handles**:
  - All collectible items (weapons, ammo, powerups)
  - Sound effects
  - Player messages
  - Score counting

## Technical Details

### State Management
The code uses state machines to manage object behaviors:
- Death states
- Pain states
- Spawn states

### Networking Considerations
- Special handling for multiplayer games
- Deathmatch-specific behaviors
- Network-safe item handling

### Damage System
Complex damage calculation considering:
- Armor protection
- Skill levels
- Invulnerability
- Special sector effects

## Conclusion
This file is central to DOOM's gameplay mechanics, handling core interactions that make the game work. It manages everything from simple item pickups to complex damage calculations and death sequences.
