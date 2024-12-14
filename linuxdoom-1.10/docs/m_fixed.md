# Fixed Point Math Implementation in DOOM

## Overview
This file implements fixed-point arithmetic operations for the DOOM engine. Fixed-point math was commonly used in older games as a faster alternative to floating-point calculations, while still allowing for fractional values.

## What is Fixed-Point Math?
Fixed-point numbers are integers that represent fractional values by reserving a certain number of bits for the decimal part. In DOOM, a 32-bit integer is split into:
- 16 bits for the whole number part
- 16 bits for the fractional part (FRACBITS)

For example, the number 1.5 would be represented as 1.5 * 2^16 in this system.

## Key Functions

### FixedMul(fixed_t a, fixed_t b)
- **Purpose**: Multiplies two fixed-point numbers
- **How it works**: 
  1. Converts inputs to long long to prevent overflow
  2. Multiplies the numbers
  3. Shifts right by FRACBITS (16) to adjust the decimal point
- **Example**: If a = 1.5 and b = 2.0 in fixed-point format, returns their product 3.0

### FixedDiv(fixed_t a, fixed_t b)
- **Purpose**: Divides two fixed-point numbers with overflow protection
- **How it works**:
  1. Checks if the division might overflow
  2. Returns maximum/minimum integer if overflow would occur
  3. Otherwise calls FixedDiv2 for actual division
- **Parameters**:
  - a: Numerator (fixed-point)
  - b: Denominator (fixed-point)

### FixedDiv2(fixed_t a, fixed_t b)
- **Purpose**: Performs actual fixed-point division
- **How it works**:
  1. Converts fixed-point numbers to doubles
  2. Performs division
  3. Converts result back to fixed-point
  4. Checks for divide-by-zero errors

## Technical Details
- Uses FRACUNIT (defined elsewhere) as the scaling factor (2^16)
- Employs both integer and floating-point math internally
- Includes overflow protection and error checking
- Compatible with GNU C++ compiler

## Important Notes
- The code includes error handling for division by zero
- Uses long long type for intermediate calculations to prevent overflow
- Provides both a pure integer version (commented out) and a floating-point assisted version of FixedDiv2

## Usage in DOOM
This fixed-point math system is crucial for:
- Game physics calculations
- Movement and positioning
- Angle calculations
- Rendering calculations

The implementation balances accuracy with performance, which was essential for running DOOM on 1990s hardware.
