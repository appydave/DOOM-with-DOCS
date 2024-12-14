# Bounding Box Management (m_bbox.c)

## Overview
This file contains functions for managing 2D bounding boxes in the DOOM engine. A bounding box is a rectangular area defined by its top, bottom, left, and right coordinates, used for collision detection and object boundaries in the game.

## Key Concepts
- A bounding box is represented by an array of fixed-point numbers
- The array stores coordinates in this order: [BOXTOP, BOXBOTTOM, BOXLEFT, BOXRIGHT]
- Fixed-point numbers are used instead of floating-point for precise, consistent calculations

## Functions

### M_ClearBox
**Purpose**: Initializes a bounding box with extreme values to prepare it for coordinate updates.

**Parameters**:
- `box`: An array of fixed-point numbers representing the bounding box

**What it does**:
- Sets the top and right edges to the minimum possible integer value
- Sets the bottom and left edges to the maximum possible integer value
- This setup ensures the first coordinate added will properly define the initial box size

### M_AddToBox
**Purpose**: Updates a bounding box to include a new point (x,y).

**Parameters**:
- `box`: The bounding box to update
- `x`: X-coordinate of the point to include
- `y`: Y-coordinate of the point to include

**What it does**:
- Compares the new coordinates against the current box boundaries
- Expands the box if the new point lies outside current boundaries:
  - If x is less than the left edge, updates left edge
  - If x is greater than the right edge, updates right edge
  - If y is less than the bottom edge, updates bottom edge
  - If y is greater than the top edge, updates top edge

## Technical Notes
- The code uses C preprocessor macros (not shown in this file) to define BOXTOP, BOXBOTTOM, BOXLEFT, BOXRIGHT
- MININT and MAXINT are used as initial values to ensure proper box initialization
- The 'fixed_t' type is DOOM's custom fixed-point number type for precise calculations

## Usage Example
```c
fixed_t myBox[4];  // Create array for box coordinates
M_ClearBox(myBox); // Initialize box
M_AddToBox(myBox, x1, y1); // Add first point
M_AddToBox(myBox, x2, y2); // Add second point
// Box now encompasses both points
```

## Summary
This code provides essential functionality for DOOM's collision detection system by managing bounding boxes. It allows the game to track the boundaries of objects and determine when they intersect with other objects or walls.
