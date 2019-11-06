# The custom objects file (war3map.w3o)

This document defines the common file format shared between these files:

| File extension | Object type | Object IDs location | Modification IDs location |
|---------------|-----|-----------------|-----------|
| `w3u` | Units | Units\UnitData.slk | Units\UnitMetaData.slk | 
| `w3t` | Items | Units\ItemData.slk | Units\UnitMetaData.slk |
| `w3b` | Destructibles | Units\DestructableData.slk | Units\DestructableMetaData.slk |
| `w3d` | Doodads | Doodads\Doodads.slk | Doodads\DoodadMetaData.slk |
| `w3a` | Abilities | Units\AbilityData.slk | Units\AbilityMetaData.slk |
| `w3h` | Buffs/Effects | Units\AbilityBuffData.slk | Units\AbilityBuffMetaData.slk |
| `w3q` | Upgrades | Units\UpgradeData.slk | Units\UpgradeMetaData.slk |

## File format
### Header
| Size | Description |
|-----|-------|
| `int` | file version |
| flexible | original objects table |
| flexible | custom objects table |

### Objects table
| Size | Description |
|-----|-------|
| `int` | number "NMOD" of objects |
| `object[NOBJ]` | NOBJ number of objects |

#### Object
| Size | Description |
|-----|-------|
| `char[4]` | original ID |
| `char[4]` | new object ID (0 if original objects table) |
| `int` | number NMOD of modifications |
| `modification[NMOD]` | NMOD number of modifications |

##### Modification
| Size | Description |
|-----|-------|
| `char[4]` | ID |
| `int` | modification type |

If the file is modifing doodads, abilities or upgrades:

| Size | Description |
|-----|-------|
| `int` | level (variation for doodads) |
| `int` | column in AbilityData.slk (only used by abilities) |

Always followed by

| Size | Description |
|-----|-------|
| `modification type` | modification amount |
| `char[4]` | either equal to 0, original ID or new ID |



## Modification types
| Value of int | Data type |
| ------|-------|
| 0 | `int` |
| 1 | `real`
| 2 | `unsigned real` |
| 3 | `string` |


