# DOOM Source Code Documentation

## Table of Contents

### Core Systems
- [am_map.md](linuxdoom-1.10/docs/am_map.md) - Automap display and navigation system
- [d_main.md](linuxdoom-1.10/docs/d_main.md) - Main game initialization and control
- [d_main2.md](linuxdoom-1.10/docs/d_main2.md) - Additional main program documentation
- [d_net.md](linuxdoom-1.10/docs/d_net.md) - Network game communication protocols
- [doomdef.md](linuxdoom-1.10/docs/doomdef.md) - Core game constants and definitions
- [doomdef2.md](linuxdoom-1.10/docs/doomdef2.md) - Additional game definitions documentation
- [doomstat.md](linuxdoom-1.10/docs/doomstat.md) - Global game state variables
- [d_items.md](linuxdoom-1.10/docs/d_items.md) - Weapon and item definitions

### Rendering
- [r_bsp.md](linuxdoom-1.10/docs/r_bsp.md) - Binary space partition rendering
- [r_data.md](linuxdoom-1.10/docs/r_data.md) - Texture and sprite management
- [r_draw.md](linuxdoom-1.10/docs/r_draw.md) - Core drawing routines
- [r_main.md](linuxdoom-1.10/docs/r_main.md) - Main rendering engine code
- [r_plane.md](linuxdoom-1.10/docs/r_plane.md) - Floor and ceiling rendering
- [r_segs.md](linuxdoom-1.10/docs/r_segs.md) - Wall segment rendering system
- [r_sky.md](linuxdoom-1.10/docs/r_sky.md) - Sky texture handling
- [r_things.md](linuxdoom-1.10/docs/r_things.md) - Sprite rendering system

### Game Logic
- [p_ceilng.md](linuxdoom-1.10/docs/p_ceilng.md) - Ceiling movement mechanics
- [p_doors.md](linuxdoom-1.10/docs/p_doors.md) - Door animation and behavior
- [p_enemy.md](linuxdoom-1.10/docs/p_enemy.md) - Enemy AI and behavior
- [p_floor.md](linuxdoom-1.10/docs/p_floor.md) - Floor movement system
- [p_inter.md](linuxdoom-1.10/docs/p_inter.md) - Object interaction handling
- [p_lights.md](linuxdoom-1.10/docs/p_lights.md) - Dynamic lighting effects
- [p_map.md](linuxdoom-1.10/docs/p_map.md) - Movement and collision detection
- [p_maputl.md](linuxdoom-1.10/docs/p_maputl.md) - Map utility functions
- [p_mobj.md](linuxdoom-1.10/docs/p_mobj.md) - Moving object management
- [p_plats.md](linuxdoom-1.10/docs/p_plats.md) - Platform and elevator system
- [p_pspr.md](linuxdoom-1.10/docs/p_pspr.md) - Player sprite and weapon handling
- [p_saveg.md](linuxdoom-1.10/docs/p_saveg.md) - Save game system
- [p_setup.md](linuxdoom-1.10/docs/p_setup.md) - Level loading and setup
- [p_sight.md](linuxdoom-1.10/docs/p_sight.md) - Line of sight calculations
- [p_spec.md](linuxdoom-1.10/docs/p_spec.md) - Special effects handler
- [p_switch.md](linuxdoom-1.10/docs/p_switch.md) - Switch and button mechanics
- [p_telept.md](linuxdoom-1.10/docs/p_telept.md) - Teleporter functionality
- [p_tick.md](linuxdoom-1.10/docs/p_tick.md) - Game tick and object updates
- [p_user.md](linuxdoom-1.10/docs/p_user.md) - Player movement and controls

### User Interface
- [f_finale.md](linuxdoom-1.10/docs/f_finale.md) - End game sequences
- [f_wipe.md](linuxdoom-1.10/docs/f_wipe.md) - Screen transition effects
- [hu_lib.md](linuxdoom-1.10/docs/hu_lib.md) - Heads-up display library
- [hu_stuff.md](linuxdoom-1.10/docs/hu_stuff.md) - HUD implementation
- [m_menu.md](linuxdoom-1.10/docs/m_menu.md) - Menu system
- [st_lib.md](linuxdoom-1.10/docs/st_lib.md) - Status bar widget library
- [st_stuff.md](linuxdoom-1.10/docs/st_stuff.md) - Status bar implementation
- [v_video.md](linuxdoom-1.10/docs/v_video.md) - Video drawing system
- [wi_stuff.md](linuxdoom-1.10/docs/wi_stuff.md) - Intermission screen handler

### System Interface
- [i_net.md](linuxdoom-1.10/docs/i_net.md) - Network interface implementation
- [i_sound.md](linuxdoom-1.10/docs/i_sound.md) - Sound system implementation
- [i_system.md](linuxdoom-1.10/docs/i_system.md) - System interface functions
- [i_video.md](linuxdoom-1.10/docs/i_video.md) - Video interface implementation

### Utilities
- [info.c.md](linuxdoom-1.10/docs/info.c.md) - Game object definitions
- [m_argv.md](linuxdoom-1.10/docs/m_argv.md) - Command line argument handling
- [m_argv2.md](linuxdoom-1.10/docs/m_argv2.md) - Additional argument handling docs
- [m_bbox.md](linuxdoom-1.10/docs/m_bbox.md) - Bounding box calculations
- [m_cheat.md](linuxdoom-1.10/docs/m_cheat.md) - Cheat code system
- [m_fixed.md](linuxdoom-1.10/docs/m_fixed.md) - Fixed-point math implementation
- [m_misc.md](linuxdoom-1.10/docs/m_misc.md) - Miscellaneous utility functions
- [m_random.md](linuxdoom-1.10/docs/m_random.md) - Random number generation
- [m_swap.md](linuxdoom-1.10/docs/m_swap.md) - Byte swapping for endianness
- [s_sound.md](linuxdoom-1.10/docs/s_sound.md) - Sound effect system
- [sounds.md](linuxdoom-1.10/docs/sounds.md) - Sound definitions
- [strings.md](linuxdoom-1.10/docs/strings.md) - String handling system
- [tables.md](linuxdoom-1.10/docs/tables.md) - Lookup tables for calculations
- [z_zone.md](linuxdoom-1.10/docs/z_zone.md) - Memory management system

### Network Driver
- [README.MD](ipx/README.MD) - IPX network driver overview
- [ReadME-C.MD](ipx/ReadME-C.MD) - C implementation details
- [ReadME-H.MD](ipx/ReadME-H.MD) - Header file documentation
