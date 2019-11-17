# The trigger names file (war3map.wtg)

This file defines the "trigger objects" in the Trigger Editor environment in the World Editor.

## File format
| Size | Description |
|------|----------|
| `char[4]` | file ID (WTG!) |
| `int` | wtg file format version = 7 |
| `int` | number "NCD" of triggers categories |
| `category[NCD]` | "NCD" times a trigger category structure |
| `int` | unknown |
| `int` | number "NVARS" of variables |
| `variable[NVARS]` | "NVARS" times a variable structure |
| `int` | number "NTRG" of triggers |
| `trigger[NTRG]` | NTRG times a trigger structure |

### Category
| Size | Description |
|------|----------|
| `int` | category index/ID |
| `String` | category name |
| `bool` | Is a comment |

### Variable
| Size | Description |
|------|----------|
| `string` | variable name |
| `string` | variable type |
| `int` | unknown |
| `bool` | is an array |
| `int` | array size |
| `bool` | is initialized |
| `string` | initial value |

### Trigger
| Size | Description |
|------|----------|
| `string` | name |
| `string` | description |
| `bool` | is comment |
| `bool` | is enabled |
| `bool` | use custom trigger text defined in war3map.wct |
| `bool` | is initially off |
| `bool` | run on map initialization |
| `int` | trigger category id |
| `int` | number "NECA" of ECA function |
| `ECA[NECA]` | NECA times an ECA function |


### Event-Condition-Action (ECA) function
| Size | Description |
|------|----------|
| `int` | type: 0=event, 1=condition, 2=action |
| `int` | Only exists if this is a child-ECA. Group for if/then/else (0 = condition, 1 = then-action, 2 = else-action).  |
| `string` | function name "NAME" |
| `bool` | is enabled |
| `parameters[NPARAM]` | NPARAM times the parameter structure. NPARAM depends on "NAME" and is hardcoded. |
| `int` | number "NCHILD" of child-ECA functions |
| `ECA[NECA]` | NCHILD times the ECA function structure |

### Parameter
| Size | Description |
|------|----------|
| `int` | Parameter type. 0=preset, 1=variable, 2=function, 3=string, -1=invalid |
| `string` | parameter value |
| `bool` | has subparameters |

If has sub parameters:

| Size | Description |
|------|----------|
| `int` | type: 3 |
| `string` | Parameter name "NAME". The same as parameter value |
| `int` | begin parameters: 1 |
| `parameters[NPARAM]` | NPARAM times the parameters structure. NPARAM depends on "NAME". |

Always followed by:

| Size | Description |
|------|----------|
| `bool` | is array |
| `parameter` | array index parameter |

## Number of parameters in an ECA or sub parameter (NPARAM)

To find the number of parameters an ECA uses, look in [TriggerData.txt](https://github.com/SimonMossmyr/w3x-spec/blob/master/TriggerDataTxt.md) under the sections

  - \[TriggerEvents\],
  - \[TriggerConditions\],
  - \[TriggerActions\],
  - \[TriggerCalls\].

Count the number of "argument types", but exclude all types that are equal to "0", "1", "nothing", or "" (empty).

For example, the line
```
OperatorCompareBoolean=0,boolean,EqualNotEqualOperator,boolean
```
in TriggerData.txt tells us that the ECA with name "OperatorCompareBoolean" has three parameters (boolean, EqualNotEqualOperator, and boolean).

The line
```
BlzIsTargetIndicatorEnabled=0,1,boolean
```
tells us that the ECA function with name "BlzIsTargetIndicatorEnabled" *doesn't have any parameters*: this ECA is defined under \[TriggerCalls\], where the argument types start after the third value ("boolean"). 
