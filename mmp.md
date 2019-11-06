# The menu minimap (war3map.mmp)

## File format
### Header
| Size | Description |
|-----|--------|
| `int` | unknown (usually 0, maybe the file format) |
| `int` | number of data blocks |

### Data
| Size | Description |
|-----|--------|
| `int` | icon type |
| `int` | X coordinate of the icon on the map |
| `int` | Y coordinate of the icon on the map |
| `byte` | player icon color blue |
| `byte` | player icon color green |
| `byte` | player icon color red |
| `byte` | player icon color alpha |

## Icon types
| Number | Description |
|------|--------|
|0| gold mine |
|1| house |
|2| player start |

## Miniap coordinates
| X | Y | Description |
|------|----|--------|
| 0x10 | 0x10 | top left |
| 0x80 | 0x80 | center |
| 0xF0 | 0xF0 | bottom right |

## Player colors
| Player number | Name | Red | Green | Blue | Alpha |
|----------|--------|------|----|-----|-------|
| 1 | Red | 03 | 03 | FF | FF |
| 2 | Blue | FF | 42 | 00 | FF |
| 3 | Teal | B9 | E8 | 19 | FF |
| 4 | Purple | 81 | 00 | 54 | FF |
| 5 | Yellow | 01 | FC | FF | FF |
| 6 | Orange | 0E | 8A | FE | FF |
| 7 | Green | 00 | C0 | 20 | FF |
| 8 | Pink | B0 | 5A | E6 | FF |
| 9 | Gray | 97 | 96 | 95 | FF |
| 10 | Light blue | F1 | BF | 7E | FF |
| 11 | Dark green | 46 | 62 | 10 | FF |
| 12 | Brown | 04 | 2A | 4E | FF |
| 13 | Maroon | 00 | 00 | 9B | FF |
| 14 | Navy | C3 | 00 | 00 | FF |
| 15 | Turquoise | FF | EA | 00 | FF |
| 16 | Violet | FE | 00 | BE | FF |
| 17 | Wheat | 87 | CD | EB | FF |
| 18 | Peach | 8B | A4 | F8 | FF |
| 19 | Mint | 80 | FF | BF | FF |
| 20 | Lavender | EB | B9 | DC | FF |
| 21 | Coal | 28 | 28 | 28 | FF |
| 22 | Snow | FF | F0 | EB | FF |
| 23 | Emerald | 1E | 78 | 00 | FF |
| 24 | Peanut | 33 | 6F | A4 | FF |
