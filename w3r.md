# The regions file (war3map.w3r)

## File format
| Size | Description |
|-----|------|
| `int` | file format version = 5 |
| `int` | number "NREG" of region structures |
| `region[NREG]` | NREG number of regions |

### Region
| Size | Description |
|-----|------|
| `float` | left (jass coordinates) |
| `float` | right (jass coordinates) |
| `float` | bottom (jass coordinates) |
| `float` | top (jass coordinates) |
| `string` | region name |
| `int` | Region index number (creation number) |
| `char[4]` | weather effect ID (ex.: "RLlr" for "Rain Lordaeron Light Rain") If all the chars are set to 0, then weather effect is disabled. |
| `String` | ambient sound (a sound ID name defined in the w3s file like "gg_snd_HumanGlueScreenLoop1") |
| `byte[4]` | region color (used by the World Editor) (BB GG RR AA, alpha unused) |
