# The trigger names file

## File format
### Header
| Size | Description |
|------|----------|
| `char[4]` | file ID (WTG!) |
| `int` | wtg file format version = 7 |
| `int` | number "NCD" of triggers categories |
| `category[NCD]` | "NCD" times a category definition structure |
| `int` | unknown |
| `int` | number "NVD" of variables |
| `variable[NVD]` | "NVD" times a variable definition structure |
| `int` | number "NTRG" of triggers |
| `trigger[NTRG]` | NTRG times a trigger definition structure |

### Category
| Size | Description |
|------|----------|
| `int` | category index |
| `String` | category name |
| `int` | Category type: 0=normal, 1=comment |

### Variable
| Size | Description |
|------|----------|
| `String` | variable name |
| `String` | variable type |
| `int` | number "e" ??? |
| `int` | array status: 0=not an array, 1=array |
| `int` | array size |
| `int` | initialisation status: 0=not initialized, 1=initialized |
| `String` | initial value (string) |

### Trigger
| Size | Description |
|------|----------|
| `String` | trigger name |
| `String` | trigger description |
| `int` | trigger type: 0=normal, 1=comment |
| `int` | enable state: 0=disabled, 1=enabled |
| `int` | custom text trigger state: 0=not a custom text trigger, 1=custom text trigger (use data in the WCT) |
| `int` | initial state: 0=initially on, 1=not initially on |
| `int` | run on map initialization: 0=no, 1=yes |
| `int` | index of the category the trigger belongs to |
| `int` | number "NECA" of event-condition-action (ECA) function |
| `ECA[NECA]` | NECA times an ECA function  |


### ECA function
| Size | Description |
|------|----------|
| `int` | function type: 0=event, 1=condition, 2=action |
| `String` | function name |
| `int` | enabled flag: 0=function disabled, 1=function enabled |
| `parameters[NPARAM]` | NPARAM times a parameters structure. NPARAM depends on the function and is hardcoded. |
| `int` | ??? |
| `int` | number "NECA" of event-condition-action (ECA) function |
| `ECA[NECA]` | NECA times an ECA function definition structure (if this trigger doesn't have multiple actions it should be set to 0 so we don't have this section) |

### Parameters
| Size | Description |
|------|----------|
| `int` | type which can be 0=preset, 1=variable, 2=function, 3=string |
| `String` | parameter value |
| `int` | begin function flag |

If begin function is set to 1:

| Size | Description |
|------|----------|
| `int` | type: 3 |
| `String` | the same as parameter value |
| `int` | begin function: 1 |
| `parameters[NPARAM]` | NPARAM times a parameters structure. NPARAM depends on the function and can be calculated from UI\\TriggerData.txt. [More information](https://www.hiveworkshop.com/threads/warcraft-3-trigger-format-specification-wtg.294491/) |

Always followed by:

| Size | Description |
|------|----------|
| `int` | end function (always set to 0) |
