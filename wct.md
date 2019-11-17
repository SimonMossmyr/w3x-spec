# The custom text trigger file (war3map.wct)

## File format
| Size | Description |
|----|---------|
| `int` |  file version: 1 |
| `String` |  custom script code comment |
| `custom_text_trigger` | a custom text trigger structure |
| `int` |  number "NCTT" of triggers |
| `custom_text_trigger[NCTT]` | NCTT number of custom text trigger structures |

### Custom Text Trigger
| Size | Description |
|----|---------|
| `int` |  size "LEN" of the text (including the null terminating char)
| `String` |  custom text trigger string (contains LEN chars including the null terminating char)

## Note
Custom text trigger structures are defined using the same order as triggers they belong to in the WTG.

Each trigger must have its custom text part, even if it has not been converted to a custom text trigger; in this case, the custom text size is set to 0 (only 4 bytes for the size int).
