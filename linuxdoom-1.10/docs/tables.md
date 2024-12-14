# DOOM Tables Module Documentation

## Overview
This module contains pre-calculated lookup tables used throughout DOOM for fast trigonometric calculations and other mathematical operations. These tables are crucial for the game's performance, as they avoid expensive runtime calculations by storing pre-computed values.

## Key Components

### SlopeDiv Function
```c
int SlopeDiv(unsigned num, unsigned den)
```
This function performs a specialized division operation used for slope calculations:
- Takes two unsigned integers as input: numerator and denominator
- Returns a slope value within a predefined range (SLOPERANGE)
- Used for calculating angles and slopes in the game's rendering engine
- Includes safety checks to prevent division by very small numbers

### Lookup Tables

#### 1. Fine Tangent Table (finetangent)
- Size: 4096 entries
- Purpose: Provides pre-calculated tangent values
- Used for: BAM (Binary Angle Measurement) calculations
- Range: Covers a full 360-degree rotation
- Precision: 12 bits of 16-bit effectively

#### 2. Fine Sine Table (finesine)
- Size: 10240 entries
- Purpose: Provides pre-calculated sine values
- Can also be used for cosine calculations through indexing
- Used for: Smooth movement and rotation calculations
- High precision for accurate game physics

#### 3. Tangent to Angle Table (tantoangle)
- Size: 2049 entries
- Purpose: Quick conversion from tangent values to angles
- Used for: Fast angle calculations in rendering
- Enables efficient lookup instead of expensive arctangent calculations

## Technical Details

### Binary Angle Measurements (BAM)
The tables use BAM for angle representations:
- Angles are stored as integers
- Full circle = 8192 units
- Provides fast and precise angle calculations without floating-point math

### Memory Usage
- Total static memory: ~66KB
- finetangent: 16KB (4096 * 4 bytes)
- finesine: 40KB (10240 * 4 bytes)
- tantoangle: 8KB (2049 * 4 bytes)

## Usage in DOOM
These tables are fundamental to DOOM's:
- 3D rendering engine
- Movement calculations
- Collision detection
- Visual effects
- Enemy AI movement

## Implementation Notes
- All values are pre-calculated to avoid runtime computation
- Tables use fixed-point arithmetic for speed
- Designed for platforms with limited floating-point capabilities
- Critical for maintaining DOOM's performance on 1993-era hardware

## Conclusion
The tables.c module is a cornerstone of DOOM's mathematical operations, providing fast access to trigonometric values through lookup tables rather than runtime calculations. This approach was crucial for achieving acceptable performance on early 1990s computer hardware.
