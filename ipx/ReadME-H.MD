# DOOM IPX Network Driver Documentation

## Overview
This documentation covers the IPX networking code used in DOOM II for multiplayer gaming. The code enables network communication between different computers running DOOM II using the IPX protocol, which was common in the DOS era.

## Header Files Structure

### DOOMNET.H
This header file defines the core networking structures and constants used by DOOM II.

#### Key Components:
- `doomcom_t`: Main communication structure between DOOM and the network driver
  - Contains game settings (players, episode, skill level etc.)
  - Handles packet data transmission
- Constants for network configuration:
  - `MAXNETNODES` (8): Maximum computers in a game
  - `MAXPLAYERS` (4): Maximum number of players
  - Commands: `CMD_SEND` (1) and `CMD_GET` (2)

### IPXNET.H
Defines the IPX protocol specific structures and packet handling.

#### Important Structures:
- `packet_t`: Complete packet structure containing:
  - ECB (Event Control Block)
  - IPX header
  - Timestamp
  - Game data
- `IPXPacket`: Network packet structure with source/destination information
- `setupdata_t`: Used during game setup to coordinate players

#### Key Types:
- `doomdata_t`: Game-specific data structure
- `localadr_t`: Local address storage
- `nodeadr_t`: Node address storage

### Language Files (IPXSTR.H & IPX_FRCH.H)
Contains string definitions for user messages in:
- English (IPXSTR.H)
- French (IPX_FRCH.H)

Messages cover various network events like:
- Player discovery
- Error conditions
- Setup status

## Network Communication Flow

1. **Initialization**
   - Driver initializes IPX communication
   - Sets up interrupt vectors
   - Prepares packet structures

2. **Game Setup**
   - Discovers other players on network
   - Synchronizes game parameters
   - Assigns player numbers

3. **During Game**
   - Handles packet transmission between nodes
   - Manages timing and sequencing
   - Processes game commands

## Technical Concepts for Non-C Programmers

### Structures
Think of structures (`struct`) as containers that group related data. For example, `doomcom_t` is like a form containing all necessary game setup information.

### Packets
Network packets are like envelopes containing:
- Address information (who it's from/to)
- Control information (how to handle it)
- The actual game data

### Interrupts
Interrupts are like doorbell rings - they signal the computer to pause and handle network communication before returning to the game.

## Conclusion
This network driver enables DOOM II multiplayer by:
1. Setting up communication between computers
2. Managing player discovery and game setup
3. Handling real-time game data exchange
4. Supporting multiple languages for user feedback

The code demonstrates sophisticated network programming for its era, handling both low-level network protocols and high-level game coordination.
