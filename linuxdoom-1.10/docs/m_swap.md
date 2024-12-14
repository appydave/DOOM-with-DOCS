# Endianness Handling in DOOM (m_swap.c)

## Overview
This file handles byte swapping operations necessary for DOOM to work correctly across different computer architectures. Specifically, it deals with endianness - the order in which bytes are stored in computer memory for multi-byte numbers.

## What is Endianness?
Endianness refers to how computers store numbers that are larger than one byte:
- **Big Endian**: Stores the most significant byte first (like reading left-to-right)
- **Little Endian**: Stores the least significant byte first (like reading right-to-left)

For example, the number 258 (0x0102 in hex) is stored as:
- Big Endian: 01 02
- Little Endian: 02 01

## Code Structure

### Conditional Compilation
The file uses conditional compilation (`#ifndef __BIG_ENDIAN__`) to only include the byte-swapping code when needed. On big-endian machines, these functions aren't necessary because DOOM's data is already in the correct format.

### Functions

#### SwapSHORT
```c
unsigned short SwapSHORT(unsigned short x)
```
- **Purpose**: Swaps the bytes in a 16-bit (2-byte) number
- **Input**: A 16-bit unsigned number
- **Output**: The same number with bytes swapped
- **How it works**: 
  - Shifts the high byte right by 8 positions
  - Shifts the low byte left by 8 positions
  - Combines them with OR (|)

#### SwapLONG
```c
unsigned long SwapLONG(unsigned long x)
```
- **Purpose**: Swaps the bytes in a 32-bit (4-byte) number
- **Input**: A 32-bit unsigned number
- **Output**: The same number with bytes swapped
- **How it works**:
  - Breaks the number into 4 bytes
  - Shifts and masks each byte to its new position
  - Combines them with OR operations

## Usage in DOOM
These functions are used throughout DOOM when reading game data (like WAD files) to ensure numbers are interpreted correctly regardless of the computer's architecture. For example:
- Loading level data
- Reading sound effects
- Processing game resources

## Technical Notes
- The code uses bitwise operations (>>, <<, &, |) for efficient byte manipulation
- No masking with 0xFF is needed when shifting bytes in SwapSHORT due to C's handling of unsigned shorts
- The functions are only compiled on little-endian systems where byte swapping is necessary

## Summary
This file is a crucial part of DOOM's portability, allowing the game to run correctly on both big-endian and little-endian systems by providing functions to convert numbers between these formats when needed.
