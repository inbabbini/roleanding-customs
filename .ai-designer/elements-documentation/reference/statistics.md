# Statistics Reference

All stat names used in `<stat>` rules and `{{stat}}` placeholders.

## Ability Scores
| Stat Name | Description |
|-----------|-------------|
| `strength` | Strength score |
| `dexterity` | Dexterity score |
| `constitution` | Constitution score |
| `intelligence` | Intelligence score |
| `wisdom` | Wisdom score |
| `charisma` | Charisma score |

### Ability Modifiers (read-only, computed)
| Stat Name | Description |
|-----------|-------------|
| `strength:modifier` | Strength modifier |
| `dexterity:modifier` | Dexterity modifier |
| `constitution:modifier` | Constitution modifier |
| `intelligence:modifier` | Intelligence modifier |
| `wisdom:modifier` | Wisdom modifier |
| `charisma:modifier` | Charisma modifier |

## Proficiency
| Stat Name | Description |
|-----------|-------------|
| `proficiency` | Proficiency bonus |
| `proficiency:half` | Half proficiency (rounded down) |
| `proficiency:half:up` | Half proficiency (rounded up) |

## Hit Points
| Stat Name | Description |
|-----------|-------------|
| `hp` | Total hit points |
| `hp:max` | Maximum HP |

## Armor Class
| Stat Name | Bonus Category | Description |
|-----------|---------------|-------------|
| `ac` | — | Total AC |
| `ac:armored:armor` | — | Base armor AC value |
| `ac:shield` | `shield` | Shield AC bonus |
| `ac:misc` | (varies) | Miscellaneous AC bonuses |
| `ac:unarmored` | — | Unarmored AC calculation |
| `ac:armored:enhancement` | — | Magic armor enhancement |
| `ac:calculation` | — | AC calculation mode |

## Speed
| Stat Name | Bonus Category | Description |
|-----------|---------------|-------------|
| `innate speed` | `base` | Base walking speed |
| `speed` | — | Current walking speed |
| `innate speed:fly` | `base` | Base fly speed |
| `innate speed:swim` | `base` | Base swim speed |
| `innate speed:climb` | `base` | Base climb speed |
| `innate speed:burrow` | `base` | Base burrow speed |
| `speed:fly` | — | Current fly speed |
| `speed:swim` | — | Current swim speed |
| `speed:climb` | — | Current climb speed |
| `speed:burrow` | — | Current burrow speed |

## Combat
| Stat Name | Description |
|-----------|-------------|
| `initiative` | Initiative modifier |
| `melee:attack` | Melee attack modifier |
| `melee:damage` | Melee damage modifier |
| `ranged:attack` | Ranged attack modifier |
| `ranged:damage` | Ranged damage modifier |
| `extra attack:count` | Number of attacks (Extra Attack) |

## Skills
| Stat Name | Description |
|-----------|-------------|
| `acrobatics:misc` | Acrobatics misc bonus |
| `animal handling:misc` | Animal Handling misc bonus |
| `arcana:misc` | Arcana misc bonus |
| `athletics:misc` | Athletics misc bonus |
| `deception:misc` | Deception misc bonus |
| `history:misc` | History misc bonus |
| `insight:misc` | Insight misc bonus |
| `intimidation:misc` | Intimidation misc bonus |
| `investigation:misc` | Investigation misc bonus |
| `medicine:misc` | Medicine misc bonus |
| `nature:misc` | Nature misc bonus |
| `perception:misc` | Perception misc bonus |
| `performance:misc` | Performance misc bonus |
| `persuasion:misc` | Persuasion misc bonus |
| `religion:misc` | Religion misc bonus |
| `sleight of hand:misc` | Sleight of Hand misc bonus |
| `stealth:misc` | Stealth misc bonus |
| `survival:misc` | Survival misc bonus |

### Passive Skills
| Stat Name | Description |
|-----------|-------------|
| `passive:perception` | Passive Perception |
| `passive:investigation` | Passive Investigation |
| `passive:insight` | Passive Insight |

## Saving Throws
| Stat Name | Description |
|-----------|-------------|
| `strength:save:misc` | Strength save bonus |
| `dexterity:save:misc` | Dexterity save bonus |
| `constitution:save:misc` | Constitution save bonus |
| `intelligence:save:misc` | Intelligence save bonus |
| `wisdom:save:misc` | Wisdom save bonus |
| `charisma:save:misc` | Charisma save bonus |

## Level Stats
| Stat Name | Description |
|-----------|-------------|
| `level` | Total character level |
| `level:{class}` | Level in specific class (lowercase: `level:fighter`) |

## Spellcasting Stats
| Stat Name | Description |
|-----------|-------------|
| `spellcasting:dc:{N}` | Spell save DC for Nth spellcasting |
| `spellcasting:attack` | Spell attack modifier |
| `{name}:spellcasting:slots:{N}` | Spell slots for level N of named spellcasting |

## Companion Stats
| Stat Name | Description |
|-----------|-------------|
| `companion:ac` | Companion armor class |
| `companion:hp:max` | Companion max HP |
| `companion:speed` | Companion walking speed |
| `companion:speed:fly` | Companion fly speed |
| `companion:proficiency` | Companion proficiency bonus |
| `companion:{skill}:proficiency` | Companion skill proficiency |

## Custom Stats
Custom stats can be created for use in `{{stat}}` sheet placeholders:
```xml
<stat name="survivor:hp" value="5" />
<stat name="survivor:hp" value="constitution:modifier" />
<!-- Usage: {{survivor:hp}} -->

<stat name="indomitable:usage" value="1" level="9" />
<stat name="indomitable:usage" value="1" level="13" />
<!-- Usage: {{indomitable:usage}} -->
```

### Naming Convention for Custom Stats
- Use `{feature}:{property}` format
- Lowercase
- Use colons to separate namespaces
- Examples: `survivor:hp`, `indomitable:usage`, `ki:points`, `channel divinity:usage`

## Special Stat Values
When setting a stat value, you can reference other stats:
```xml
<stat name="ac:misc" value="constitution:modifier" />
<stat name="melee:attack" value="proficiency" />
<stat name="acrobatics:misc" value="proficiency:half:up" />
```
