# DOOM Network Implementation (i_net.c)

## Overview
This file implements the networking functionality for DOOM, specifically handling UDP-based multiplayer communication between different game instances. It provides the foundation for multiplayer gaming by managing network sockets, packet sending/receiving, and player connections.

## Key Components

### Network Configuration
- Uses UDP (User Datagram Protocol) for game communication
- Default port: IPPORT_USERRESERVED + 0x1d
- Supports multiple players through node-based networking

### Important Functions

#### UDPsocket()
Creates and returns a new UDP socket for network communication.
- Returns: Socket file descriptor
- Throws error if socket creation fails

#### BindToLocalPort(int s, int port)
Binds a socket to a specific local port.
- Parameters:
  - s: Socket descriptor
  - port: Port number to bind to
- Configures socket to accept connections on any network interface

#### PacketSend()
Handles sending game data packets to other players.
- Performs byte-swapping for network compatibility
- Sends player movement commands and game state information
- Uses sendto() for UDP packet transmission

#### PacketGet()
Receives and processes incoming network packets.
- Handles packet validation and player identification
- Performs byte-swapping on received data
- Updates game state with received information

#### I_InitNetwork()
Initializes the network subsystem for DOOM.
- Processes command-line arguments for network configuration
- Sets up player numbers and host connections
- Initializes UDP sockets for communication
- Configures single-player or multiplayer mode

### Data Structures

#### doomdata_t
Game data packet structure containing:
- Checksum for validation
- Player information
- Movement commands
- Game state data

## Technical Details

### Network Protocol
- Uses UDP for fast, connectionless communication
- Implements custom byte-ordering (ntohl/htonl) for cross-platform compatibility
- Supports multiple players through node-based addressing

### Error Handling
- Robust error checking for socket operations
- Detailed error messages using strerror()
- Graceful handling of network failures

## Usage

### Command Line Options
- `-dup n`: Sets packet duplication (1-9)
- `-extratic`: Enables extra tics for network synchronization
- `-port n`: Specifies custom port number
- `-net x`: Enables multiplayer mode (x = player number)

### Network Setup
1. Program initializes network system
2. Creates and binds UDP sockets
3. Establishes connections with other players
4. Begins game data transmission

## Conclusion
This implementation provides the networking foundation for DOOM's multiplayer functionality, handling all aspects of network communication while maintaining game state synchronization between players.
