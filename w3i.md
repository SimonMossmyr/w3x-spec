# "war3map.w3i" (The info file)

## File format
| Size | Description |
|-----|-------|
| `int` | file format version = 25 |
| `int` | number of saves (map version) |
| `int` | editor version (little endian) |
| `String` | map name |
| `String` | map author |
| `String` | map description |
| `String` | players recommended |
| `float[8]` | "Camera Bounds" as defined in the JASS file |
| `int[4]` | camera bounds complements* (see note) (ints A, B, C and D) |
| `int` | map playable area width E* (see note) |
| `int` | map playable area height F* (see note) |
| `int` | flags |
| `char` | map main ground type. Defined in W3E specification. |
| `int` | Loading screen background number which is its index in the preset list (-1 = none or custom imported file) |
| `String` | path of custom loading screen model (empty string if none or preset) |
| `String` | Map loading screen text |
| `String` | Map loading screen title |
| `String` | Map loading screen subtitle |
| `int` | used game data set (index in the preset list, 0 = standard) |
| `String` | Prologue screen path (usually empty) |
| `String` | Prologue screen text (usually empty) |
| `String` | Prologue screen title (usually empty) |
| `String` | Prologue screen subtitle (usually empty) |
| `int` | use terrain fog (0 = not used, greater 0 = index of terrain fog style dropdown box) |
| `float` | fog start z height |
| `float` | fog end z height |
| `float` | fog density |
| `byte` | fog red value |
| `byte` | fog green value |
| `byte` | fog blue value |
| `byte` | fog alpha value |
| `int` | global weather id (0 = none, else it's set to the 4-letter-id of the desired weather found in TerrainArt\Weather.slk) |
| `String` | custom sound environment (set to the desired sound lable) |
| `char` | tileset id of the used custom light environment |
| `byte` | custom water tinting red value |
| `byte` | custom water tinting green value |
| `byte` | custom water tinting blue value |
| `byte` | custom water tinting alpha value |
| `int` | max number "MAXPL" of players |
| `player_data[MAXPL]` | then, there is MAXPL times a player data like described below. |
| `int` | max number "MAXFC" of forces |
| `force_data[MAXFC]` | then, there is MAXFC times a force data like described below. |
| `int` | number "UCOUNT" of upgrade availability changes |
| `upgrade_availability[UCOUNT]` | then, there is UCOUNT times a upgrade availability change like described below. |
| `int` | number "TCOUNT" of tech availability changes (units, items, abilities) |
| `tech_availability[TCOUNT]` | then, there is TCOUNT times a tech availability change like described below |
| `int` | number "UTCOUNT" of random unit tables |
| `random_unit_table[UTCOUNT]` | then, there is UTCOUNT times a unit table like described below |
| `int` | number "ITCOUNT" of random item tables |
| `random_item_table[ITCOUNT]` | then, there is ITCOUNT times a item table like described below |


## Note
map width = A + E + B

map height = C + F + D

## Flags
| Bit | Description |
|----|--------|
| `0x0001` | hide minimap in preview screens |
| `0x0002` | modify ally priorities |
| `0x0004` | melee map |
| `0x0008` | playable map size was large and has never been reduced to medium (?) |
| `0x0010` | masked area are partially visible |
| `0x0020` | fixed player setting for custom forces |
| `0x0040` | use custom forces |
| `0x0080` | use custom techtree |
| `0x0100` | use custom abilities |
| `0x0200` | use custom upgrades |
| `0x0400` | map properties menu opened at least once since map creation (?) |
| `0x0800` | show water waves on cliff shores |
| `0x1000` | show water waves on rolling shores |
| `0x2000` | unknown |
| `0x4000` | unknown |
| `0x8000` | unknown |

## Player data format

| Size | Description |
| -------|---------|
| `int` | internal player number |
| `int` | player type. 1=Human, 2=Computer, 3=Neutral, 4=Rescuable |
| `int` | player race. 1=Human, 2=Orc, 3=Undead, 4=Night Elf |
| `int` | 00000001 = fixed start position |
| `String` | Player name |
| `float` | Starting coordinate X |
| `float` | Starting coordinate Y |
| `int` | ally low priorities flags (bit "x"=1 --> set for player "x") |
| `int` | ally high priorities flags (bit "x"=1 --> set for player "x") |

## Force data format
| Size | Description |
| -------|---------|
| `int` | force flags |
| `int` | player masks (bit "x"=1 --> player "x" is in this force) |
| `String` | Force name |

### Force flags
| Bit | Description |
|-----|------|
| `0x01` | allied (force 1) |
| `0x02` | allied victory |
| `0x04` | share vision |
| `0x10` | share unit control |
| `0x20` | share advanced unit control |

## Upgrade availability change format
| Size | Description |
| -------|---------|
| `int` | Player Flags (bit "x"=1 if this change applies for player "x") |
| `char[4]` | upgrade id (as in UpgradeData.slk) |
| `int` | Level of the upgrade for which the availability is changed (this is actually the level - 1, so 1 => 0) |
| `int` | Availability (0 = unavailable, 1 = available, 2 = researched) |

## Tech availability change format
| Size | Description |
| -------|---------|
| `int` | Player Flags (bit "x"=1 if this change applies for player "x") |
| `char[4]` | tech id (this can be an item, unit or ability) |

There's no need for an availability value, if a tech-id is in this list, it means that it's not available |

## Random unit table format
| Size | Description |
| -------|---------|
| `int` | Number "NRG" of random groups |
| `random_group[NRG]` | then we have n times the following data (for each group) |

### Random group format
| Size | Description |
| -------|---------|
| `int` | Group number |
| `string` | Group name |
| `int` | Number "POS" of positions |
| `int[POS]` | Positions are the table columns where you can enter the unit/item ids, all units in the same line have the same chance, but belong to different "sets" of the random group, called positions here. For each positon is specified if it's a unit table (=0), a building table (=1) or an item table (=2) |
| `int` | Number "NUT" of units/items, this is the number of lines in the table, each position can have that many or fewer entries |
| `random_unit_item[NUT]` | now there's "i" times the following structure (for each line) |

#### Random unit or item
| Size | Description |
| -------|---------|
| `int` | Chance of the unit/item (percentage) |
| `char[POS * 4]` | For each position are the unit/item id's for this line specified. This can also be a random unit/item ids (see bottom of war3mapUnits.doo definition). A unit/item id of 0x00000000 indicates that no unit/item is created |

## Random item tables format
| Size | Description |
| -------|---------|
| `int` | Number "NRI" of random item tables |
| `item_table[NRI]` | then we have n times the following data (for each item table) |

### Random item table format
| Size | Description |
| -------|---------|
| `int` | Table number |
| `string` | Table name |
| `int` | Number "NIS" of item sets on the current item table |
| `item_set[NIS]` | then we have m times the following data (for each item set) |

#### Item set format
| Size | Description |
| -------|---------|
| `int` | Number "NITEMS" of items on the current item set |
| `item[NITEMS]` | then we have i times the following two values (for each item) |

##### Item format
| Size | Description |
| -------|---------|
| `int` | Percentual chance |
| `char[4]` | Item id (as in ItemData.slk) |

This can also be a random item id (see bottom of war3mapUnits.doo definition)
