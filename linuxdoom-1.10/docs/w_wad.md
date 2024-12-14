# WAD File Handling System (w_wad.c)

## Overview
This file implements DOOM's WAD (Where's All the Data) file handling system. WAD files are DOOM's custom archive format that contains all game assets like levels, sprites, sounds etc. The code provides functionality to read and manage these WAD files, including loading files, caching data, and retrieving specific game assets (called "lumps").

## Key Concepts for Non-C Programmers
- **Lumps**: Individual data items stored in WAD files (like a level map or sound effect)
- **Handles**: References to opened files (like file IDs)
- **Caching**: Storing frequently accessed data in memory for faster access
- **Structs**: Custom data types that group related data together (similar to objects)

## Important Data Structures

### wadinfo_t
The header information of a WAD file:
- `identification`: 4 characters identifying the WAD type (IWAD or PWAD)
- `numlumps`: Number of lumps in the file
- `infotableofs`: Location of the lump information table

### filelump_t
Information about a lump in the WAD file:
- `filepos`: Position of the lump in the file
- `size`: Size of the lump
- `name`: Name of the lump (8 characters)

### lumpinfo_t
Runtime information about loaded lumps:
- `handle`: File handle
- `position`: Position in file
- `size`: Size of lump
- `name`: Name of lump

## Major Functions

### W_AddFile(char *filename)
Adds a WAD file to the game:
- Opens the specified file
- Reads its header
- Adds its lumps to the global lump directory
- Handles both WAD files and single lump files

### W_InitMultipleFiles(char** filenames)
Initializes the WAD system with multiple files:
- Takes a null-terminated list of filenames
- Calls W_AddFile for each file
- Sets up the lump cache system

### W_CacheLumpNum(int lump, int tag)
Caches a lump for quick access:
- Takes a lump number and cache tag
- Loads the lump into memory if not already cached
- Returns pointer to the cached data

### W_ReadLump(int lump, void* dest)
Reads a lump's data:
- Takes a lump number and destination buffer
- Reads the lump's data from the WAD file into memory

### W_CheckNumForName(char* name)
Searches for a lump by name:
- Takes a lump name (up to 8 characters)
- Returns the lump number if found, -1 if not found
- Case-insensitive search

## Memory Management
The code uses a caching system to manage memory efficiently:
- Lumps are only loaded when needed
- Cached lumps can be marked for different purposes (tags)
- Memory can be freed when no longer needed

## Error Handling
The code uses I_Error() for error handling, which typically displays an error message and terminates the program. Common errors include:
- File not found
- Invalid WAD format
- Memory allocation failures
- Attempting to access invalid lumps

## Usage Example
```c
// Initialize WAD system with DOOM.WAD
char* wadfiles[] = {"DOOM.WAD", NULL};
W_InitMultipleFiles(wadfiles);

// Get a specific lump (e.g., a sound effect)
int lumpnum = W_GetNumForName("DSPISTOL");
void* sounddata = W_CacheLumpNum(lumpnum, PU_CACHE);
```

## Conclusion
The WAD handling system is a crucial part of DOOM's architecture, providing efficient access to all game assets. It implements a simple but effective caching system and provides a clean interface for accessing game data. While the implementation uses C-specific features like pointers and manual memory management, the overall design is straightforward and focused on performance.
