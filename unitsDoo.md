# "war3mapUnits.doo" (The unit and item file)

## File format
### Header
| Size | Description |
|------|------------|
| `char[4]` | file ID = "W3do" |
| `int` | file version = 8 |
| `int` | subversion? (often set to [0B 00 00 00]h) |
| `int` | number of units and items defined |

### Data
Each unit/item is defined by a block of bytes (variable length) organized like this

| Size | Description |
|------|------------|
| `char[4]` | type ID (`iDNR` = random item, `uDNR` = random unit) |
| `int` | variation |
| `float` | coordinate X |
| `float` | coordinate Y |
| `float` | coordinate Z |
| `float` | rotation angle |
| `float` | scale X |
| `float` | scale Y |
| `float` | scale Z |
| `byte` | flags |
| `int` | player number (owner) |
| `byte` | unknown (0) |
| `byte` | unknown (0) |
| `int` | hit points (-1 = use default) |
| `int` | mana points (-1 = use default, 0 = unit doesn't have mana) |
| `int` | map item table pointer (for dropped items on death) <br> if -1 => no item table used <br> if >= 0 => the item table with this number will be dropped on death |
| `int` | number "s" of dropped item sets (can only be greater 0 if the item table pointer was -1) <br> then we have s times a dropped item sets structures (see below) |
| `int` | gold amount (default = 12500) |
| `float` | target acquisition (-1 = normal, -2 = camp) |
| `int` | hero level (set to1 for non hero units and items) |
| `int` | strength of the hero (0 = use default) |
| `int` | agility of the hero (0 = use default) |
| `int` | intelligence of the hero (0 = use default) |
| `int` | number "n" of items in the inventory <br> then there is n times a inventory item structure (see below) |
| `int` | number "n" of modified abilities for this unit <br> then there is n times a ability modification structure (see below) |
| `int` | random unit/item flag "r" (for uDNR units and iDNR items) <br> 0 = Any neutral passive building/item, in this case we have <br> `byte[3]`  level of the random unit/item,-1 = any (this is actually interpreted as a 24-bit number) <br>   byte item class of the random item, 0 = any, 1 = permanent ... (this is 0 for units)<br> r is also 0 for non random units/items so we have these 4 bytes anyway (even if the id wasn't uDNR or iDNR)<br> 1 = random unit from random group (defined in the w3i), in this case we have<br> int unit group number (which group from the global table) <br>   int position number (which column of this group)<br>   the column should of course have the item flag set (in the w3i) if this is a random item<br> 2 = random unit from custom table, in this case we have<br>   int number "n" of different available units<br>   then we have n times a random unit structure
| `int` | custom color (-1 = none, 0 = red, 1=blue,...) |
| `int` | Waygate: active destination number (-1 = deactivated, else it's the creation number of the target rect as in war3map.w3r) |
| `int` | creation number |

## Flags
May be similar to the war3map.doo flags

## Dropped item set format
| Size | Description |
|------|------------|
| `int` | number "d" of dropable items |

"d" times dropable items structures:

| Size | Description |
|------|------------|
| `char[4]` | item ID ([00 00 00 00]h = none)<br>this can also be a random item id (see below) |
| `int` | % chance to be dropped |

## Inventory item formatf
| Size | Description |
|------|------------|
| `int` | inventory slot (this is the actual slot - 1, so 1 => 0) |
| `char[4]` | item id (as in ItemData.slk) '\0' = none |

this can also be a random item id (see below)

## Ability modification format
| Size | Description |
|------|------------|
| `char[4]` | ability id (as in AbilityData.slk) |
| `int` | active for autocast abilities, 0 = no, 1 = active |
| `int` | level for hero abilities |

## Random unit format
| Size | Description |
|------|------------|
| `char[4]` | unit id (as in UnitUI.slk)<br>this can also be a random unit id (see below) |
| `int` | percentual chance of choice |

## Random item ids
random item ids are of the type char[4] where the 1st letter is "Y" and the 3rd letter is "I"

the 2nd letter narrows it down to items of a certain item types

- "Y" = any type
- "i" to "o" = item of this type, the letters are in order of the item types in the dropdown box ("i" = charged)

the 4th letter narrows it down to items of a certain level

- "/" = any level (ASCII 47)
- "0" ... = specific level (this is ASCII 48 + level, so level 10 will be ":" and level 15 will be "?" and so on)

## Random unit ids
random unit ids are of the type char[4] where the 1st three letters are "YYU"

the 4th letter narrows it down to units of a certain level

- "/" = any level (ASCII 47)
- "0" ... = specific level (this is ASCII 48 + level, so level 10 will be ":" and level 15 will be "?" and so on)
