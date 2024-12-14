# Zone Memory Allocation System (z_zone.c)

## Overview
This file implements a memory management system (called the "Zone Memory Allocator") for the DOOM game engine. It provides controlled memory allocation with features specifically designed for game development, including memory blocks that can be tagged and purged when needed.

## Key Concepts for Non-C Programmers
- **Memory Allocation**: Programs need to request memory from the computer to store data. This code manages that process.
- **Memory Blocks**: Think of these as labeled containers that hold data. Each block knows its size and what it's being used for.
- **Pointers**: These are like addresses that tell where something is stored in memory. In this code, they're used to link memory blocks together.

## Memory Block Structure
Each memory block contains:
- Size information
- Links to previous and next blocks
- User information (who owns the block)
- Tag (indicates how the block can be used)
- ID (for validation)

## Main Functions

### Z_Init
- **Purpose**: Initializes the memory zone system
- **What it does**: Creates one large free block of memory that will be divided up as needed

### Z_Malloc
- **Purpose**: Allocates memory for use
- **Parameters**:
  - size: How much memory is needed
  - tag: How the memory will be used
  - user: Who owns the memory
- **Returns**: A pointer to the allocated memory

### Z_Free
- **Purpose**: Returns memory back to the system
- **What it does**: Marks memory as available and combines adjacent free blocks

### Z_FreeTags
- **Purpose**: Frees all memory blocks with tags in a specified range
- **Useful for**: Clearing out all memory of a certain type at once

### Z_CheckHeap
- **Purpose**: Validates the memory system's integrity
- **What it does**: Checks for common memory problems like:
  - Blocks that don't connect properly
  - Invalid links between blocks
  - Adjacent free blocks that should be merged

## Memory Tags
Memory blocks can be tagged with different levels:
- Static (permanent)
- Cache (can be reused if needed)
- Purgeable (can be freed if memory runs low)

## Error Handling
The system includes various safety checks:
- Validates memory block IDs
- Ensures blocks are properly connected
- Prevents invalid memory operations

## Debugging Tools
- Z_DumpHeap: Prints information about all memory blocks
- Z_FileDumpHeap: Saves memory information to a file
- Z_CheckHeap: Verifies memory system integrity

## Summary
This memory management system provides DOOM with controlled, efficient memory use. It allows the game to:
- Allocate memory as needed
- Free memory when it's no longer needed
- Automatically purge less important data when memory runs low
- Track memory usage and detect problems

The system is particularly suited for gaming needs, where memory management needs to be both flexible and reliable.
