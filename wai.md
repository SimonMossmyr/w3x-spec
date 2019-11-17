# The AI file (war3map.wai)

## File format
| Bit | Description |
|----|-----------|
| `int` |  wai file format version: 2 |
| `string` |  AI name |
| `int` |  race: 0=Custom, 1=Human, 2=Orc, 3=Undead, 4=Night Elf |
| `int` |  options (see section) |
| `int` |  number of following workers and buildings. If there are less than 4 workers and buildings specified, WorldEdit will choose default values. Should be: 4. |
| `char[4]` |  gold worker |
| `char[4]` |  wood worker |
| `char[4]` |  base building |
| `char[4]` |  mine building (If none, use the same identifer as base building) |
| `int` |  number "NCOND" of conditions |
| `int` |  unknown: 7 (format version?) |
| `condition[NCOND]` |"NCOND" times a conditions definition structure |
| `char[4]` |  First Hero Used (if none set these values to null otherwise set it to Unit ID) |
| `char[4]` |  Second Hero Used (if none set these values to null otherwise set it to Unit ID) |
| `char[4]` |  Third Hero Used (if none set these values to null otherwise set it to Unit ID) |
| `int` |  Training Order % Chance(1.FirstHero,2.SecondHero,3.ThirdHero) |
| `int` |  Training Order % Chance(1.FirstHero,2.ThirdHero,3.SecondHero) |
| `int` |  Training Order % Chance(1.SecondHero,2.FirstHero,3.ThirdHero) |
| `int` |  Training Order % Chance(1.SecondHero,2.ThirdHero,3.FirstHero) |
| `int` |  Training Order % Chance(1.ThirdHero,2.FirstHero,3.SecondHero) |
| `int` |  Training Order % Chance(1.ThirdHero,2.SecondHero,3.FirstHero) |
| `char[4*10]` |  Ten Skill IDs for First Hero(as first hero) |
| `char[4*10]` |  Ten Skill IDs for First Hero(as second hero) |
| `char[4*10]` |  Ten Skill IDs for First Hero(as third hero) |
| `char[4*10]` |  Ten Skill IDs for Second Hero(as first hero) |
| `char[4*10]` |  Ten Skill IDs for Second Hero(as second hero) |
| `char[4*10]` |  Ten Skill IDs for Second Hero(as third hero) |
| `char[4*10]` |  Ten Skill IDs for Third Hero(as first hero) |
| `char[4*10]` |  Ten Skill IDs for Third Hero(as second hero) |
| `char[4*10]` |  Ten Skill IDs for Third Hero(as third hero) |
| `int` |  number "NBPR" of Build Priorities |
| `build_prior[NBPR]` | "NBPR" times build priorities structure |
| `int` |  number "NHPR" of Harvest Priorities |
| `harvest_prio[NHPR]` | "NHPR" times harvest priorities structure |
| `int` |  number "NTPR" of Target Priorities |
| `target_prio[NTPR]` | "NTPR" times target priorities structure |
| `int` |  repeats waves |
| `int` |  minimum forces: attack group index (for First Hero Only set this value to 1095319880 (i.e 0x48414941, char[4] 'HAIA') |
| `int` |  initial delay |
| `int` |  number "NAG" of Attack Groups |
| `attack_group[NAG]` | "NAG" times attack groups structure |
| `int` |  number "NAW" of Attack Waves |
| `attack_wave[NAW]` | "NAW" times attack waves structure |
| `int` |  unknown: 1 |
| `int` |  game options |
| `int` |  regular game speed |
| `string` |  path to map file |
| `int` |  number "NP" of Players (0-2) |
| `player[NP]` | "NP" times players structure |
| `int` |  unknown |

### Condition Structure
| Bit | Description |
|----|-----------|
| `int` |  condition index |
| `String` |  condition name |
| `bool` | "COND" contains condition |

if COND is true:

| Bit | Description |
|----|-----------|
| `String` |  operator function name |
| `int` |  begin function: 1 |
| `parameter[NPARAM]` | "NPARAM" times a Parameters Structure. NPARAMS depends on the function and can be found in TriggerData.txt. |
| `int` |  end function: 0 |

### Parameters Structure
The documentation for this structure is found in [wtg.md](https://github.com/SimonMossmyr/w3x-spec/blob/master/wtg.md)

### Build Priorities Structure
| Bit | Description |
|----|-----------|
| `int` |  priorities type: 0 |
| `int` |  type: 0=unit, 1=upgrade, 2=expansion town |
| `char[4]` |  Unit/Upgrade ID(if it is expansion town this value should be set to: XEIA) |
| `int` |  town: 0=main, 1-9=Expansion #1-9, 0xFFFFFFFD-0xFFFFFFF5=current mine #1-9, 0xFFFFFFFF=any |
| `int` |  condition index(if none set this value to 0xFFFFFFFF, if custom set this value to 0xFFFFFFFE) |
| `condition` | condition structure (without condition index!) |

### Harvest Priorities Structure
| Bit | Description |
|----|-----------|
| `int` |  priorities type: 1 |
| `int` |  harvest type: 0=gold, 1=lumber |
| `int` |  town: 0=main, 1-9=Expansion #1-9, 0xFFFFFFFD-0xFFFFFFF5=current mine #1-9, 0xFFFFFFFF=any |
| `int` |  workers: 0-90=fixed value #0-90, 0xFFFFFFFF=all, 0xFFFFFFFE=all not attacking |
| `int` |  condition index(if none, set this value to 0xFFFFFFFF, if custom, set this value to 0xFFFFFFFE) |
| `condition` | condition structure (without condition index!) |

### Target Priorities Structure
| Bit | Description |
|----|-----------|
| `int` |  priorities type: 2 |
| `int` |  target: 0=common alliance target, 1=new expansion location, 2=enemy major assault, 3=enemy expansion, 4=enemy any town, 5=creep camp, 6=purchase goblin zeppelin |
| `int` |  creep min strength(if target is other than 5 set this value to 0xFFFFFFFF) |

if target = 5

| Bit | Description |
|----|-----------|
| `int` | creep max strength |
| `int` | allow flyers: 0=no, 1=yes |

Always followed by:

| Bit | Description |
|----|-----------|
| `int` |  condition index(if none, set this value to 0xFFFFFFFF, if custom, set this value to 0xFFFFFFFE) |
| `condition` | condition structure (without condition index!) |

### Attack Groups Structure
| Bit | Description |
|----|-----------|
| `int` |  attack group index |
| `string` |  attack group name |
| `int` |  number "NCG" of Current Group |
| `current_group[NCG]` | "NCG" times current group structure |

### Current Group Structure
| Bit | Description |
|----|-----------|
| `char[4]` |  Unit ID (FirstHero: 1HIA, SecondHero: 2HIA, ThirdHero: 3HIA) |
| `int` |  quantity value: 0-90=quantity #0-90, 0xFFFFFFFF=All |
| `int` |  maximum quantity: 0-90=quantity #0-90, 0xFFFFFFFF=All(if quantity value is 0xFFFFFFFF, maximum quantity means all except #0-90) |
| `int` |  condition index(if none, set this value to 0xFFFFFFFF, if custom, set this value to 0xFFFFFFFE) |
| `condition` | condition structure (without condition index!) |

### Attack Waves Structure
| Bit | Description |
|----|-----------|
| `int` |  attack group index |
| `int` |  delay |

### Players Structure
| Bit | Description |
|----|-----------|
| `int` |  player index |
| `int` |  team number |
| `int` |  race: 1=human, 2=orc, 8=undead, 4=night elf, 20=random |
| `int` |  color: 0=red, 1=blue, 2=teal, 3=purple, 4=yellow, 5=orange, 6=green, 7=pink, 8=gray, 9=light blue, 10=dark green, 11=brown |
| `int` |  handicap (0-100) |
| `int` |  ai: 0=standard, 1=user, 4=custom, 12=current |
| `int` |  ai difficulty: 0=easy, 1=normal, 2=insane |
| `string` |  path to custom ai script |

## Options
Unless otherwise noted all of the options are contained in HiWord of options integer.
Check for the presence of options by using a mask with following values:

| Bit | Description |
|----|-----------|
| `0x2000` | SetPlayerName |
| `0x0001` | Melee |
| `0x8000` | DefendUsers |
| `0x4000` | RandomPaths |
| `0x0002` | TargetHeroes |
| `0x0004` | RepairStructures |
| `0x0008` | HeroesFlee |
| `0x0010` | UnitsFlee |
| `0x0020` | GroupsFlee |
| `0x0040` | HaveNoMercy |
| `0x0080` | IgnoreInjured |
| `0x1000` | RemoveInjuries |
| `0x0100` | TakeItems |
| `0x0001` LoWord | BuyItems |
| `0x0200` | SlowHarvesting |
| `0x0400` | AllowHomeChanges |
| `0x0800` | SmartAltillery |

## Game options
Unless otherwise noted all of the options are contained in HiWord of options integer.
Check for the presence of options by using a mask with following values:

| Bit | Description |
|----|-----------|
| `0x0001` | Disable Fog Of War |
| `0x0002` | Disable Victory/Defeat Conditions |
