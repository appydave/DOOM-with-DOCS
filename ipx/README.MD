# DOOM IPX Network Driver

This directory contains the IPX networking implementation for DOOM multiplayer support. IPX (Internetwork Packet Exchange) was a networking protocol commonly used in the early 1990s, particularly popular with Novell NetWare networks.

## Overview

The IPX driver enables DOOM multiplayer games over local area networks using the IPX protocol. This was one of the primary networking methods for DOOM's release in 1993, alongside serial connections and modems.

## Features

- Supports up to 4 players in multiplayer games
- Handles packet transmission and reception over IPX networks
- Compatible with Novell NetWare networks
- Low latency for local network play

## Technical Details

The implementation includes:
- IPX socket management
- Packet formatting and parsing
- Player discovery and connection handling
- Integration with DOOM's network game code

## Building

The IPX driver is compiled as part of the main DOOM build process. Make sure you have the necessary IPX development libraries installed on your system.

## Historical Note

While IPX is now largely obsolete, having been replaced by TCP/IP, this code represents an important part of DOOM's multiplayer legacy and early network gaming history.
