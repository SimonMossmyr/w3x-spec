# The imported file list (war3map.imp)

## File format
| Size | Description |
|-----|-----|
| `int` | file format version |
| `int` | number "NIMP" of imported files |
| `imported_file[NIMP]` | NIMP number of imported files |

### Imported file structure
| Size | Description |
|-----|-----|
| `byte` | tells if the path is complete or needs "war3mapImported\" (5 or 8= standard path, 10 or 13: custom path) |
| `string` | the path inside the w3m of each imported file (like "war3mapImported\mysound.wav") |

## Note
Any file added in the W3M and added in the .imp will NOT be removed by the World Editor each time you save your map.

This file can also be found in Warcraft campaign files with the name war3campaign.imp with the only difference that the standard path for imported files is "war3campaignImported\".
