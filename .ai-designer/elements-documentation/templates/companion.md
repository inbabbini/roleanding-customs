# Companion Template

Companions represent creatures that accompany a character (familiars, animal companions, mounts, etc.).

## Companion Element

```xml
<element name="{Companion Name}" type="Companion" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_COMPANION_{NAME}">
    <supports>{Companion Category Tags}</supports>
    <description>
        <p>{Description}</p>
    </description>
    <setters>
        <set name="strength">{N}</set>
        <set name="dexterity">{N}</set>
        <set name="constitution">{N}</set>
        <set name="intelligence">{N}</set>
        <set name="wisdom">{N}</set>
        <set name="charisma">{N}</set>
        <set name="ac">{N}</set>
        <set name="hp">{N} ({die expression})</set>
        <set name="speed">{speed text}</set>
        <set name="senses">{senses text}</set>
        <set name="languages">{languages}</set>
        <set name="skills">{skill bonuses}</set>
        <set name="resistances">{resistances}</set>
        <set name="immunities">{immunities}</set>
        <set name="conditionImmunities">{condition immunities}</set>
        <set name="type">{Creature Type}</set>
        <set name="size">{Size}</set>
        <set name="alignment">{alignment}</set>
        <set name="challenge">{CR}</set>
        <set name="traits">{trait IDs, comma-separated}</set>
        <set name="actions">{action IDs, comma-separated}</set>
        <set name="reactions">{reaction IDs, comma-separated}</set>
    </setters>
    <rules>
        <stat name="companion:ac" value="{N}" />
        <stat name="companion:hp:max" value="{N}" bonus="base" />
        <stat name="companion:speed" value="{N}" bonus="base" />
        <stat name="companion:speed:fly" value="{N}" bonus="base" />
        <!-- Skill proficiencies -->
        <stat name="companion:{skill}:proficiency" value="companion:proficiency" bonus="base" />
    </rules>
</element>
```

## Required Setters
| Setter | Description |
|--------|-------------|
| `strength`–`charisma` | Ability scores (numeric) |
| `ac` | Armor class (numeric) |
| `hp` | Hit points: `{N} ({die expression})` |
| `speed` | Movement: `30 ft.` or `20 ft., fly 40 ft.` |
| `type` | Creature type: `Beast`, `Fiend`, `Fey`, `Celestial`, etc. |
| `size` | `Tiny`, `Small`, `Medium`, `Large`, `Huge`, `Gargantuan` |
| `alignment` | e.g., `lawful evil`, `unaligned` |
| `challenge` | Challenge rating: `0`, `1/8`, `1/4`, `1/2`, `1`, etc. |
| `traits` | Comma-separated list of Companion Trait element IDs |
| `actions` | Comma-separated list of Companion Action element IDs |

## Optional Setters
| Setter | Description |
|--------|-------------|
| `senses` | `darkvision 60 ft., passive Perception {N}` |
| `languages` | Languages the companion understands/speaks |
| `skills` | `Perception +3, Stealth +5` (display text) |
| `resistances` | Damage resistances |
| `immunities` | Damage immunities |
| `conditionImmunities` | Condition immunities |
| `reactions` | Comma-separated Companion Reaction IDs |
| `savingThrows` | `Dex +4, Wis +2` (display text) |

## Supports (Companion filters)
| Value | Used By |
|-------|---------|
| `Familiar` | Find Familiar spell |
| `Variant Familiar` | Pact of the Chain familiars |
| `Beast Companion` | Ranger Beast Master |
| `Mount` | Find Steed spell |

## Companion Trait Element

```xml
<element name="{Trait Name}" type="Companion Trait" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_COMPANION_TRAIT_{COMPANION}_{TRAIT}">
    <description>
        <p>{Trait description}</p>
    </description>
    <sheet>
        <description>{Sheet text}</description>
    </sheet>
</element>
```

## Companion Action Element

```xml
<element name="{Action Name}" type="Companion Action" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_COMPANION_ACTION_{COMPANION}_{ACTION}">
    <description>
        <p>{Action description}</p>
    </description>
    <sheet>
        <description>{Sheet text}</description>
    </sheet>
</element>
```

## Companion Reaction Element

```xml
<element name="{Reaction Name}" type="Companion Reaction" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_COMPANION_REACTION_{COMPANION}_{REACTION}">
    <description>
        <p>{Reaction description}</p>
    </description>
    <sheet>
        <description>{Sheet text}</description>
    </sheet>
</element>
```

## Example: Complete Companion

```xml
<element name="Imp" type="Companion" source="Monster Manual" id="ID_WOTC_MM_COMPANION_IMP">
    <supports>Familiar, Variant Familiar</supports>
    <description><p>Imps can be found in the service to mortal spellcasters...</p></description>
    <setters>
        <set name="strength">6</set>
        <set name="dexterity">17</set>
        <set name="constitution">13</set>
        <set name="intelligence">11</set>
        <set name="wisdom">12</set>
        <set name="charisma">14</set>
        <set name="ac">13</set>
        <set name="hp">10 (3d4+3)</set>
        <set name="speed">20 ft., fly 40 ft.</set>
        <set name="senses">darkvision 120 ft., passive Perception 11</set>
        <set name="languages">Infernal, Common</set>
        <set name="skills">Deception +4, Insight +3, Persuasion +4, Stealth +5</set>
        <set name="resistances">cold; bludgeoning, piercing, and slashing from nonmagical attacks not made with silvered weapons</set>
        <set name="immunities">fire, poison</set>
        <set name="type">Fiend</set>
        <set name="size">Tiny</set>
        <set name="alignment">lawful evil</set>
        <set name="challenge">1</set>
        <set name="traits">ID_WOTC_MM_COMPANION_TRAIT_IMP_SHAPECHANGER,ID_WOTC_MM_COMPANION_TRAIT_IMP_DEVILS_SIGHT,ID_WOTC_MM_COMPANION_TRAIT_IMP_MAGIC_RESISTANCE</set>
        <set name="actions">ID_WOTC_MM_COMPANION_ACTION_IMP_STING,ID_WOTC_MM_COMPANION_ACTION_IMP_INVISIBILITY</set>
    </setters>
    <rules>
        <stat name="companion:ac" value="13" />
        <stat name="companion:hp:max" value="10" bonus="base" />
        <stat name="companion:speed" value="20" bonus="base" />
        <stat name="companion:speed:fly" value="40" bonus="base" />
        <stat name="companion:deception:proficiency" value="companion:proficiency" bonus="base" />
        <stat name="companion:insight:proficiency" value="companion:proficiency" bonus="base" />
        <stat name="companion:persuasion:proficiency" value="companion:proficiency" bonus="base" />
        <stat name="companion:stealth:proficiency" value="companion:proficiency" bonus="base" />
    </rules>
</element>

<element name="Shapechanger" type="Companion Trait" source="Monster Manual" id="ID_WOTC_MM_COMPANION_TRAIT_IMP_SHAPECHANGER">
    <description><p>The imp can polymorph into a beast form...</p></description>
    <sheet><description>The imp can polymorph into a beast form...</description></sheet>
</element>

<element name="Sting (Bite in Beast Form)" type="Companion Action" source="Monster Manual" id="ID_WOTC_MM_COMPANION_ACTION_IMP_STING">
    <description><p>Melee Weapon Attack: +5 to hit, reach 5 ft., one target. Hit: 5 (1d4 + 3) piercing damage...</p></description>
    <sheet><description>Melee Weapon Attack: +5 to hit, reach 5 ft., one target. Hit: 5 (1d4 + 3) piercing damage...</description></sheet>
</element>
```

## File Structure Order
1. Companion element
2. Companion Trait elements (referenced in the `traits` setter)
3. Companion Action elements (referenced in the `actions` setter)
4. Companion Reaction elements (referenced in the `reactions` setter)

## Notes
- Companion Traits/Actions/Reactions are separate elements linked via comma-separated IDs in setters
- Rules use `companion:` prefix for stat names
- Skill proficiencies use `companion:{skill}:proficiency` stat set to `companion:proficiency`
- Multiple companions can share a single file (e.g., `companions.xml` per source book)
