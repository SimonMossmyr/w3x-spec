# The sounds file (war3map.w3s)

## File format

| Size | Description |
|-----|-------|
| `int` | file format version = 1 |
| `int` | number "NSND" of sound structures |
| `sound[NSND]` | NSND number of sound structures |

### Sound structure:
| Size | Description |
|-----|-------|
| `String` |  sound ID name (like "gg_snd_HumanGlueScreenLoop1") |
| `String` |  sound file (like "Sound\Ambient\HumanGlueScreenLoop1.wav") |
| `String` |  EAX effects (see section) |
| `int` |  sound flags (see section) |
| `int` |  fade in rate |
| `int` |  fade out rate |
| `int` |  volume (-1=use default value) |
| `float` |  pitch |
| `float` |  unknown |
| `int` |  unknown (-1 or 8) |
| `int` |  channel: |
| `float` |  min. distance |
| `float` |  max. distance |
| `float` |  distance cutoff |
| `float` |  unknown |
| `float` |  unknown |
| `int` |  unknown (-1 or 127) |
| `float` |  unknown |
| `float` |  unknown |
| `float` |  unknown |

## List of EAX effects

| Value | Description |
|-----|-------|
| DefaultEAXON | Default |
| CombatSoundsEAX | combat |
| KotoDrumsEAX | drums |
| SpellsEAX | spells |
| MissilesEAX | missiles |
| HeroAcksEAX | hero speech |
| DoodadsEAX | doodads |

## Sound flags
| Bit | Flag |
|----|-----|
| `0x01` | looping |
| `0x02` | 3D sound |
| `0x04` | stop when out of range |
| `0x08` | music |
| `0x10` | unknown |

## Channel list
| Value | Channel |
|------|-------|
| 0  | General |
| 1  | Unit Selection |
| 2  | Unit Acknowledgement |
| 3  | Unit Movement |
| 4  | Unit Ready |
| 5  | Combat |
| 6  | Error |
| 7  | Music |
| 8  | User Interface |
| 9  | Looping Movement |
| 10 | Looping Ambient |
| 11 | Animations |
| 12 | Constructions |
| 13 | Birth |
| 14 | Fire |

## A note on Floats
Floats value can be set or left unset (default value will be used)
When a float is not set, the value 0x4F800000 = 4.2949673e+009 is used.
