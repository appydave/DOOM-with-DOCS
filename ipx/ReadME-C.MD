# DOOM IPX Network Driver Documentation

## Overview
This code implements IPX networking support for DOOM, allowing multiple players to play DOOM together over a local network using the IPX protocol. The implementation consists of three main files:

- `DOOMNET.C`: Handles launching DOOM with networking enabled
- `IPXSETUP.C`: Sets up the network connection and coordinates between players
- `IPXNET.C`: Implements the low-level IPX packet driver functionality

## Key Concepts for Non-C Programmers

Before diving into the code details, here are some important C concepts used throughout:

- **Pointers**: Variables that store memory addresses. Marked with `*` in declarations.
- **Structs**: Custom data types that group related variables together.
- **Function Pointers**: Variables that store the address of functions to call them indirectly.
- **Interrupts**: Special functions that handle hardware events.
- **Memory Segments**: In DOS, memory is divided into segments (addressed with segment:offset pairs).

## File Details

### IPXNET.C
This file implements the core IPX networking functionality:

#### Key Data Structures
- `packet_t`: Represents a network packet containing:
  - ECB (Event Control Block) for IPX
  - IPX header
  - Data payload
  - Timestamp

#### Important Functions
- `InitNetwork()`: Sets up IPX sockets and packet buffers
- `SendPacket()`: Sends data to other players
- `GetPacket()`: Receives data from other players
- `OpenSocket()/CloseSocket()`: Manages IPX network sockets

### IPXSETUP.C 
This file handles network game setup:

#### Key Functions
- `LookForNodes()`: Discovers other players on the network
- `main()`: Coordinates the entire setup process:
  1. Processes command line arguments
  2. Initializes network
  3. Finds other players
  4. Launches DOOM

#### Notable Features
- Supports response files (command line arguments from a file)
- Configurable network parameters like number of players
- Handles player number assignment

### DOOMNET.C
This file manages launching DOOM with networking enabled:

#### Key Functions
- `LaunchDOOM()`: Starts DOOM with proper network parameters
- `NetISR()`: Interrupt handler for network communication

## Network Protocol Overview

The networking works by:
1. Each player runs IPXSETUP
2. Players discover each other via broadcast packets
3. Player numbers are assigned based on network addresses
4. DOOM is launched with networking parameters
5. During game, packets are exchanged via IPX

## Technical Details

### Packet Format
- ECB header (IPX control block)
- IPX header (addresses, length, etc)
- Timestamp
- Game data

### Network Discovery
Players exchange setup packets containing:
- Number of nodes found
- Number of nodes wanted
- Player configuration

### Synchronization
- Uses timestamps to order packets
- Supports "ticdup" for slow networks
- Handles drone nodes (non-player spectators)

## Common Operations

### Starting a Network Game
1. Run IPXSETUP with desired parameters
2. Wait for all players to join
3. Game launches automatically when ready

### Command Line Options
- `-nodes N`: Set number of players
- `-vector X`: Set interrupt vector
- `-port X`: Set IPX socket number

## Error Handling
The code includes extensive error checking for:
- IPX initialization failures
- Packet transmission errors
- Invalid configurations
- Network timeouts

## Limitations
- Maximum 4 players
- IPX protocol only
- DOS-specific implementation
- Requires compatible network cards

## Conclusion
This implementation enabled multiplayer DOOM over local networks in the DOS era. While dated by modern standards, it demonstrates effective use of the IPX protocol and careful handling of network synchronization issues that remain relevant in modern game networking.
