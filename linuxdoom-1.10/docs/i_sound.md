# Sound System Implementation (i_sound.c)

## Overview
This file implements the sound system for DOOM on Linux systems. It handles both sound effects (SFX) and music playback, though music functionality is mostly stubbed out. The code manages digital audio output through the Linux sound device (/dev/dsp), supporting stereo 16-bit sound at 11025Hz.

## Key Components

### Sound Buffer Management
- Uses a mixing buffer (mixbuffer) to combine multiple sound channels
- Supports 8 simultaneous sound channels
- Sample rate: 11025 Hz
- 16-bit stereo output
- Buffer size: 512 samples * 4 (SAMPLECOUNT * BUFMUL)

### Global Variables
- `audio_fd`: File descriptor for the sound device
- `channels[]`: Array of pointers to current sound data
- `channelsend[]`: Array of pointers to end of sound data
- `mixbuffer[]`: The global mixing buffer where all sounds are combined
- `lengths[]`: Array storing lengths of all sound effects
- `vol_lookup[]`: Volume adjustment lookup table

## Main Functions

### I_InitSound()
Initializes the sound system:
1. Opens /dev/dsp device
2. Configures audio parameters (stereo, 16-bit, 11025Hz)
3. Loads all sound effects from WAD file
4. Initializes mixing buffer

### I_UpdateSound()
Core mixing function that:
1. Mixes active sound channels into the global buffer
2. Applies volume and stereo separation
3. Clamps values to prevent distortion
4. Prepares final output for the sound device

### getsfx()
Loads a sound effect from the WAD file:
1. Locates sound data using "ds" prefix
2. Loads and pads the sound data
3. Returns pointer to processed sound data

### addsfx()
Adds a sound effect to play:
1. Finds available channel
2. Sets up channel parameters (volume, separation)
3. Returns handle for sound management

## Sound Channel Management
Each channel tracks:
- Current position in sound data
- End position
- Volume levels (left/right)
- Start time
- Sound ID

## Error Handling
- Uses I_Error() for fatal errors
- Checks for device availability
- Validates volume levels

## Technical Notes
- Uses Linux sound card API (OSS)
- Supports interrupt-driven or polling sound output
- Can be compiled with external sound server (SNDSERV)
- Handles endianness issues for sample data

## Music System
The music system is mostly stubbed out with dummy functions:
- I_InitMusic()
- I_PlaySong()
- I_StopSong()
etc.

## Usage Example
```c
// Start a sound effect
int handle = I_StartSound(sfx_pistol, 127, 128, 128, 0);

// Update sound mixing (called every game tick)
I_UpdateSound();

// Submit mixed sound to device
I_SubmitSound();
```

## Limitations
- Music playback not implemented
- Fixed sample rate
- Maximum 8 simultaneous sounds
- Linux-specific implementation
