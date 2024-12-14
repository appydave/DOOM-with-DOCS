# DOOM Line of Sight Implementation (p_sight.c)

## Overview
This file implements line-of-sight (LOS) calculations in DOOM, determining if one game object can "see" another. It's a crucial part of enemy AI and visibility checking, using the game's BSP (Binary Space Partitioning) tree structure and REJECT lookup table for optimization.

## Key Concepts
- **Line of Sight**: Determines if there's an unobstructed path between two points
- **BSP Tree**: A data structure that divides space into regions for efficient spatial queries
- **REJECT Table**: A pre-calculated lookup table that quickly determines if two sectors can possibly see each other

## Major Functions

### P_CheckSight
The main function that determines if two objects (t1 and t2) can see each other.
- **Input**: Two game objects (mobj_t structures)
- **Output**: Boolean (true if objects can see each other)
- **Process**:
  1. Quick rejection check using REJECT table
  2. Calculates sight slopes from viewer's height
  3. Traces line through BSP tree to check for obstacles

### P_CrossBSPNode
Recursively traverses the BSP tree to check for line-of-sight obstructions.
- **Input**: BSP node number
- **Output**: Boolean (true if sight line passes through node)
- **Process**:
  1. Determines which side of node the sight line starts on
  2. Recursively checks child nodes
  3. Handles special case of subsectors

### P_CrossSubsector
Checks if a sight line can pass through a subsector (leaf node of BSP tree).
- **Input**: Subsector number
- **Output**: Boolean (true if sight line passes through)
- **Process**:
  1. Checks each line in subsector
  2. Tests for line intersections
  3. Handles two-sided lines and height differences

### Helper Functions

#### P_DivlineSide
Determines which side of a dividing line a point lies on.
- Returns 0 (front), 1 (back), or 2 (on the line)

#### P_InterceptVector2
Calculates intersection point of two lines.
- Used for precise collision detection

## Technical Details

### Important Variables
- `sightzstart`: Eye level of viewing object
- `topslope`, `bottomslope`: Vertical angles to target
- `strace`: Line from viewer to target
- `sightcounts`: Statistics counters

### Key Data Structures
- `divline_t`: Represents a line divider
- `node_t`: BSP tree node
- `subsector_t`: Leaf node in BSP tree
- `seg_t`: Line segment in game world

## Optimization Techniques
1. REJECT table for quick impossible-sight determination
2. BSP tree for efficient space traversal
3. Early exit conditions throughout the process

## Summary
This code implements an efficient line-of-sight system using BSP trees and pre-calculated lookup tables. It's essential for enemy AI and visibility determination in DOOM, balancing accuracy with performance through various optimization techniques.
