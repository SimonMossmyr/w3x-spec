 # war3map.doo (The doodad file for trees)

The file contains the doodad definitions and positions.

## File format

The DOO file consists of 

 1. A 16 byte doodad header,
 2. Doodad data of usually 50 bytes (size can vary) for each doodad,
 3. A special doodads header,
 4. Special doodads data of 16 bytes each,
 5. A 16 byte tree header, and
 6. Tree data of usually 50 bytes (size can vary) for each tree.
 
 The special doodads can't be edited once they are placed.

### Doodad header

| Size | Description | Default value |
|-----|-----|------|
| `char[4]` | file ID | `W3do` |
| `int` | file version | 8 |
| `int` | subversion? | `[0B 00 00 00]h` |
| `int` | number of trees defined ||

### Doodad data

| Size | Description |
|-----|-----|
| `char[4]` | Doodad ID (can be found in the file "Units\DestructableData.slk") |
| `int` | Variation (little endian) |
| `float` | Doodad X coordinate on the map |
| `float` | Doodad Y coordinate on the map |
| `float` | Doodad Z coordinate on the map |
| `float` | Doodad angle (radians) |
| `float` | Doodad X scale |
| `float` | Doodad Y scale |
| `float` | Doodad Z scale |
| `byte` | Doodad flags |
| `byte` | Doodad life (integer stored in %, 100% is 0x64, 170% is 0xAA for example) |
| `int` | Random item table pointer <br> if -1 -> no item table <br> if >= 0 -> items from the item table with this number (defined in the w3i) are dropped on death |
| `int` | number `n` of item sets dropped on death (this can only be greater than 0 if the item table pointer was -1) then there is n times a item set structure |
| `int` | Doodad ID number in the World Editor (little endian) (each tree has a different one) |

### Special doodads header

| Size | Description | Default value |
|-----|-----|-----|
| `int` | special doodad format version | `0` |
| `int` | number `s` of "special" doodads ("special" like cliffs,...) ||

### Special doodads data

| Size | Description |
|----|-----|
| `char[4]` | doodad ID |
| `int` | Z? (0) |
| `int` | X? (w3e coordinates) |
| `int` | Y? (w3e coordinates) |

### Tree header and data
The tree header and data is identical to normal doodads, including File ID `W3do`, but all Doodad IDs appear to be the same.


## Doodad Flags
0= invisible and non-solid doodad<br>
1= visible but non-solid doodad<br>
2= normal doodad (visible and solid)<br>

## Item set format

Where is this located in the file? O_o

### Header

| Size | Description |
|----|-----|
| `int` | number `n` of items in the item set |

### Data

| Size | Description |
|----|-----|
| `char[4]` | item id (as in ItemData.slk) <br> this can also be a random item id (see bottom of war3mapUnits.doo definition) |
| `int` | percentual chance of choice |
