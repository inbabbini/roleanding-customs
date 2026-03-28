# Setters Reference

Complete reference of all `<set>` nodes organized by element type.

## Source Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `abbreviation` | — | Short abbreviation for IDs (e.g., `PHB`) |
| `url` | — | URL for more info |
| `image` | — | Source image/cover URL |
| `author` | `abbreviation`, `url` | Author name, abbreviation for IDs |
| `official` | — | `true` for official WotC content |
| `supplement` | — | `true` if this is a supplement |
| `playtest` | — | `true` for Unearthed Arcana/playtest |
| `release` | — | Release date: `YYYYMMDD` |
| `errata` | — | Errata date: `YYYYMMDD` |
| `core` | — | `true` for core rulebooks |
| `information` | — | `true` for informational content |
| `league` | — | `true` for Adventurers League content |
| `third-party` | — | `true` for third-party content |
| `homebrew` | — | `true` for homebrew content |

## Race Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `names` | `type` (`male`, `female`, `clan`, `family`, `virtue`, `child`) | Comma-separated name lists |
| `names-format` | — | Name format: `{{name}} {{clan}}`, `{{name}} "{{virtue}}" {{clan}}` |

## Sub Race Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `height` | `modifier` (die) | Base height (e.g., `3'8"`) with random modifier |
| `weight` | `modifier` (die) | Base weight (e.g., `115 lb.`) with random modifier |

## Class Setters
| Setter | Description |
|--------|-------------|
| `short` | Brief class description |
| `hd` | Hit die: `d6`, `d8`, `d10`, `d12` |
| `multiclass proficiencies` | Text description of multiclass proficiencies (inside `<multiclass>` node) |

## Background Setters
| Setter | Description |
|--------|-------------|
| `short` | Summary of proficiencies: `"Insight, Religion, 2 Languages"` |

## Spell Setters
| Setter | Values | Description |
|--------|--------|-------------|
| `keywords` | comma-separated | Damage types, tags for search |
| `level` | `0`–`9` | Spell level (0 = cantrip) |
| `school` | Abjuration, Conjuration, Divination, Enchantment, Evocation, Illusion, Necromancy, Transmutation | School of magic |
| `time` | `1 action`, `1 bonus action`, `1 reaction`, `1 minute`, `10 minutes`, `1 hour`, `8 hours`, `24 hours` | Casting time |
| `duration` | `Instantaneous`, `1 round`, `1 minute`, `Concentration, up to {time}`, etc. | Duration |
| `range` | `Self`, `Touch`, `{N} feet`, `Self ({N}-foot {shape})` | Spell range |
| `hasVerbalComponent` | `true`/`false` | Verbal component |
| `hasSomaticComponent` | `true`/`false` | Somatic component |
| `hasMaterialComponent` | `true`/`false` | Material component |
| `materialComponent` | text or empty | Material component description |
| `isConcentration` | `true`/`false` | Requires concentration |
| `isRitual` | `true`/`false` | Can be cast as ritual |

## Weapon Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `category` | — | Always `Weapons` |
| `cost` | `currency` (gp/sp/cp) | Cost |
| `weight` | `lb` (numeric) | Weight |
| `slot` | — | `onehand` or `twohand` |
| `range` | — | `{short}/{long}` for thrown/ranged |
| `damage` | `type` (bludgeoning/piercing/slashing) | Damage die |
| `proficiency` | — | Proficiency ID |

## Armor Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `category` | — | Always `Armor` |
| `cost` | `currency` | Cost |
| `weight` | `lb` | Weight |
| `slot` | — | `body` (armor) or `onehand` (shield) |
| `armor` | — | `Light`, `Medium`, `Heavy`, `Shield` |
| `armorClass` | — | AC formula text |
| `stealth` | — | `Disadvantage` |
| `strength` | — | Min strength requirement (number) |
| `proficiency` | — | Proficiency ID |

## Item (Gear) Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `category` | — | Display category (Adventuring Gear, Ammunition, etc.) |
| `cost` | `currency`, `bulk` | Cost with optional bulk quantity |
| `weight` | `lb` | Weight |
| `stackable` | — | `true` for consumables/generic items |
| `type` | — | Type override (e.g., `Ammunition`) |

## Magic Item Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `keywords` | — | Search/filter keywords |
| `category` | — | Magic Weapons, Magic Armor, Wondrous Items, Potions, Rings, Rods, Scrolls, Staffs, Wands |
| `cost` | `currency` | Cost (usually `0`) |
| `weight` | `lb` | Weight |
| `type` | `addition` | Base type + subtype |
| `rarity` | — | Common, Uncommon, Rare, Very Rare, Legendary, Artifact |
| `attunement` | — | `true` or requirement text |
| `slot` | — | Equipment slot |
| `enhancement` | — | Enhancement bonus number |
| `weapon` | — | Weapon filter (name or IDs) |
| `armor` | — | Armor filter (name or IDs) |
| `name-format` | — | Display name with `{{parent}}`, `{{enhancement}}` |
| `stackable` | — | `true` for potions/consumables |
| `charges` | — | Number of charges |
| `stash` | `lb`, `weightless` | Container capacity |

## Language Setters
| Setter | Description |
|--------|-------------|
| `standard` | `true` for Standard, `false` for Exotic |
| `speakers` | Typical speakers |
| `script` | Writing script |

## Companion Setters
| Setter | Description |
|--------|-------------|
| `strength`–`charisma` | Ability scores |
| `ac` | Armor class |
| `hp` | Hit points: `{N} ({die expression})` |
| `speed` | Movement speeds |
| `senses` | Senses |
| `languages` | Languages |
| `skills` | Skill bonuses text |
| `resistances` | Damage resistances |
| `immunities` | Damage immunities |
| `conditionImmunities` | Condition immunities |
| `savingThrows` | Saving throw bonuses |
| `type` | Creature type |
| `size` | Size category |
| `alignment` | Alignment |
| `challenge` | Challenge rating |
| `traits` | Companion Trait IDs (comma-separated) |
| `actions` | Companion Action IDs (comma-separated) |
| `reactions` | Companion Reaction IDs (comma-separated) |

## Option Setters
| Setter | Description |
|--------|-------------|
| `short` | Summary text for the options panel |
