# The Trigger Data file (TriggerData.txt)

The Trigger Data file configures the Trigger Editor environment in the World Editor. The config file, TriggerData.txt, is found in WarCraft III's [CASC](http://www.zezula.net/en/casc/main.html). While this repository only defines the W3X file format, TriggerData.txt is required to interpret `war3map.wtg`.

The file is pretty much self explanatory. Extract ([CascView](http://www.zezula.net/en/casc/main.html) is recommended) and open it with a text editor.

## File format
The file is encoded as readable text interpreted line-by-line.

An empty line or a line starting with double slash `//` is ignored.

The file is divided into 10 sections. The start of a section is marked with `[EncasingBrackets]` which are surrounded with developer notes. The currently defined sections are, in order:

  - [TriggerCategories]
  - [TriggerTypes]
  - [TriggerTypeDefaults]
  - [TriggerParameters]
  - [TriggerEvents]
  - [TriggerConditions]
  - [TriggerActions]
  - [TriggerCalls]
  - [DefaultTriggerCategories]
  - [DefaultTriggers]

Each section contains a list of key-value(s) mappings separated by an equal sign `=`. The value mapping can contain several values, which are separated by comma signs `,`. For example, the line
```
TC_NEUTRALBUILDING=WESTRING_TRIGCAT_NEUTRALBUILDING,ReplaceableTextures\WorldEditUI\Actions-Goldmine
```
defines the mapping from the key TC_NEUTRALBUILDING to the values WESTRING_TRIGCAT_NEUTRALBUILDING and ReplaceableTextures\WorldEditUI\Actions-Goldmine.

The file can also define extensions to these mappings. Any key prefixed with an underscore `_` and suffixed with an underscore followed by a name `_Name` will belong to the previous line's key. For example, the lines
```
TriggerRegisterGameStateEventTimeOfDay=0,limitop,real
_TriggerRegisterGameStateEventTimeOfDay_Defaults=LimitOpEqual,12
```
defines a mapping from the key TriggerRegisterGameStateEventTimeOfDay to the values 0, limitop, real, LimitOpEqual, and 12.

The section [DefaultTriggerCategories] defines a single key NumCategories followed by that number of key-value mappings.

Similarly, the section [DefaultTriggerCategories] defines a single key NumTriggers followed by that number of triggers, where a trigger is a list of key-value mappings that follow the format
```
Trigger##Foo##=<value>
```
