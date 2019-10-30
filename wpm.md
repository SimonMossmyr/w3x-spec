# war3map.wpm (The Path Map File)

## File format

The WPM file consists of a header block followed by (map_height\*4)\*(map_with\*4) bytes of tile data.

### Header
| Size | Description | Default value |
|----|------|-----|
| `char[4]` | file ID | `MP3W` |
| `int` | file version | 0 |
| `int` | path map width (map_width\*4) |
| `int` | path map height (map_height\*4) |

### Tile Data
Each tile is divided into 4\*4 = 16 parts ("pixels"). Each byte in the tile data block represents a single pixel of a tile.

Flags table:

| Byte value | Flags |
|-------|----------|
| `0x01` | 0 (unused) |
| `0x02` | 1=no walk, 0=walk ok |
| `0x04` | 1=no fly, 0=fly ok |
| `0x08` | 1=no build, 0=build ok |
| `0x10` | 0 (unused) |
| `0x20` | 1=blight, 0=normal |
| `0x40` | 1=no water, 0=water |
| `0x80` | 1=unknown, 0=normal |

## Examples
| Byte value | Use |
|------|-----|
| `0x00` | bridge doodad |
| `0x08` | shallow water |
| `0x0A` | deep water |
| `0x40` | normal ground |
| `0x48` | water ramp, unbuildable grounds, unbuildable parts of doodads |
| `0xCA` | cliff edges, solid parts of doodads (no build and no walk) |
| `0xCE` | edges of the map (boundaries) |
