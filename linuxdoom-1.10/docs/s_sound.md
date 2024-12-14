# Sound System (s_sound.c)

## Overview
This file implements the core sound system for DOOM, handling both sound effects (SFX) and music playback. It manages sound channels, volume control, positional audio, and music state management.

## Key Concepts

### Sound Channels
- The game uses multiple channels to play sounds simultaneously
- Each channel can play one sound effect at a time
- Channels are managed through a `channel_t` structure that tracks:
  - The sound being played
  - Where the sound is coming from
  - A handle to identify the playing sound

### Sound Properties
- Volume: Ranges from 0-127
- Separation: Controls stereo positioning (left/right balance)
- Pitch: Controls sound frequency/tone
- Priority: Determines which sounds take precedence when channels are full

## Major Functions

### Initialization
`S_Init(sfxVolume, musicVolume)`
- Sets up the sound system
- Allocates channels for mixing
- Initializes volume levels for both SFX and music

### Sound Playback
`S_StartSound(origin, sfx_id)`
- Starts playing a sound effect
- Parameters:
  - origin: Where the sound comes from (usually an object in the game)
  - sfx_id: Which sound to play

`S_StartSoundAtVolume(origin, sfx_id, volume)`
- Like S_StartSound but with explicit volume control
- Handles positioning and priority

### Music Control
`S_StartMusic(m_id)`
- Starts playing a music track
- Simple wrapper around S_ChangeMusic

`S_ChangeMusic(musicnum, looping)`
- Changes the currently playing music
- Can set whether the music should loop

### Sound Updates
`S_UpdateSounds(listener)`
- Main update function called regularly
- Updates volume and positioning based on player movement
- Stops finished sounds
- Manages channel cleanup

### Volume Control
`S_SetMusicVolume(volume)`
- Sets music volume (0-127)

`S_SetSfxVolume(volume)`
- Sets sound effects volume (0-127)

## Technical Details

### Distance Calculations
- Sounds get quieter with distance
- Uses approximate distance calculation for performance
- Has special handling for map 8 (different attenuation)

### Channel Management
- Limited number of simultaneous sounds
- Priority system when all channels are in use
- Automatic cleanup of finished sounds

### Constants
```c
#define S_CLIPPING_DIST    (1200*0x10000)  // When to stop playing sounds
#define S_CLOSE_DIST       (160*0x10000)   // Distance for max volume
#define NORM_VOLUME        snd_MaxVolume    // Default volume
#define S_NUMCHANNELS      2               // Number of sound channels
```

## Usage Example
When a monster makes a sound:
1. Game calls S_StartSound with monster position and sound ID
2. System finds available channel
3. Calculates volume based on distance to player
4. Starts playing sound with calculated parameters
5. Updates sound properties each frame as player/monster move

## Integration Notes
- Works with external sound drivers through I_* functions
- Supports both music and sound effects independently
- Handles pause/resume for game state changes
