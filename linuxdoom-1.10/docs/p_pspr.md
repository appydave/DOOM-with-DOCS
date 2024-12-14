# DOOM Weapon Sprite Animation and Actions (p_pspr.c)

## Overview
This file handles weapon animations and actions in DOOM. It manages how weapons appear on screen, their firing mechanics, and player weapon state changes. The code controls everything from raising/lowering weapons to firing effects and damage calculations.

## Key Concepts

### Weapon States
- Weapons exist in various states (ready, firing, lowering, raising)
- Each state has associated animations and behaviors
- States are managed through a state machine system

### Player Sprite Definitions (pspdef_t)
- Represents weapon sprites from the player's viewpoint
- Tracks weapon position and current animation state
- Separate definitions for weapon and muzzle flash

## Core Functions

### Weapon State Management
- `P_SetPsprite`: Sets weapon sprite state and handles state transitions
- `P_BringUpWeapon`: Initiates weapon raising animation
- `P_DropWeapon`: Handles weapon lowering when player dies

### Weapon Actions
- `P_FireWeapon`: Main weapon firing logic
- `P_CheckAmmo`: Verifies sufficient ammo and handles weapon switching
- `P_BulletSlope`: Calculates bullet trajectory for hit detection

### Animation States
- `A_WeaponReady`: Handles weapon idle state and firing checks
- `A_Raise`: Controls weapon raising animation
- `A_Lower`: Controls weapon lowering animation

### Weapon-Specific Actions
- `A_FirePistol`: Pistol firing logic
- `A_FireShotgun`: Shotgun firing pattern (7 pellets)
- `A_FireShotgun2`: Super shotgun pattern (20 pellets)
- `A_FirePlasma`: Plasma rifle projectile
- `A_FireBFG`: BFG 9000 firing sequence
- `A_Punch`: Melee attack calculations
- `A_Saw`: Chainsaw attack logic

## Constants

### Weapon Movement
- `LOWERSPEED`: Speed of lowering weapons (6 units)
- `RAISESPEED`: Speed of raising weapons (6 units)
- `WEAPONBOTTOM`: Lowest weapon position (128 units)
- `WEAPONTOP`: Highest weapon position (32 units)

### Special Values
- `BFGCELLS`: Ammo cost for BFG shot (40 cells)

## Technical Details

### Weapon Bobbing
- `P_CalcSwing`: Calculates weapon movement during player motion
- Uses sine/cosine tables for smooth animation
- Adjusts weapon position based on player movement speed

### Damage Calculation
- Different weapons use varying random factors
- Special multipliers for power-ups (e.g., berserk strength)
- Range and spread patterns vary by weapon type

## State Machine Implementation
The code uses a state machine to manage weapon states and transitions. Each state can:
- Set sprite coordinates
- Trigger sound effects
- Execute action functions
- Chain to next states automatically

## Summary
This file is central to DOOM's weapon system, handling everything from visual presentation to combat mechanics. It demonstrates classic game programming patterns like state machines and fixed-point math for smooth animations.
