# Archetype & Archetype Feature Templates

An archetype file contains the Archetype element, its Archetype Feature elements, and Feature Replacement Grants.

## Archetype Element

```xml
<element name="{Archetype Name}" type="Archetype" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_ARCHETYPE_{NAME}">
    <supports>{Archetype Category}</supports>
    <description>
        <p>{Archetype description}</p>
        <!-- Inline feature descriptions -->
        <div element="ID_{...}_ARCHETYPE_FEATURE_{FEATURE1}" />
        <div element="ID_{...}_ARCHETYPE_FEATURE_{FEATURE2}" />
    </description>
    <sheet display="false">
        <description>{Short description}</description>
    </sheet>
    <rules>
        <grant type="Archetype Feature" id="ID_{...}_ARCHETYPE_FEATURE_{FEATURE1}" level="{N}" />
        <grant type="Archetype Feature" id="ID_{...}_ARCHETYPE_FEATURE_{FEATURE2}" level="{N}" />
        <!-- Features granted at levels defined by the parent class's archetype progression -->
    </rules>
</element>
```

### Key Points
- `<supports>` **MUST** match the parent class's archetype selection `supports` value exactly
  - Fighter → `Martial Archetype`
  - Rogue → `Roguish Archetype`
  - Wizard → `Arcane Tradition`
  - Cleric → `Divine Domain`
  - Paladin → `Sacred Oath`
  - Ranger → `Ranger Archetype`
  - Barbarian → `Primal Path`
  - Bard → `Bard College`
  - Druid → `Druid Circle`
  - Monk → `Monastic Tradition`
  - Sorcerer → `Sorcerous Origin`
  - Warlock → `Otherworldly Patron`
- `<sheet display="false" />` is standard (the archetype name shows in the class section)
- Level values in grants match the class's archetype feature levels (e.g., Fighter: 3, 7, 10, 15, 18)

## Archetype Feature Element

```xml
<element name="{Feature Name}" type="Archetype Feature" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_ARCHETYPE_FEATURE_{NAME}">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_{ARCHETYPE}_{FEATURE}</requirements>
    <description>
        <p>{Description}</p>
    </description>
    <sheet>
        <description>{Sheet text with {{stat}} placeholders}</description>
    </sheet>
    <rules>
        <!-- Mechanical effects -->
    </rules>
</element>
```

### Common Archetype Feature Patterns

**Simple feature (text only)**:
```xml
<element name="Improved Critical" type="Archetype Feature" source="Player's Handbook" id="ID_WOTC_PHB_ARCHETYPE_FEATURE_IMPROVEDCRITICAL">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_FIGHTER_CHAMPION_IMPROVED_CRITICAL</requirements>
    <description><p>Your weapon attacks score a critical hit on a roll of 19 or 20.</p></description>
    <sheet>
        <description>Your weapon attacks score a critical hit on a roll of 19 or 20.</description>
    </sheet>
</element>
```

**Feature with stat modifications**:
```xml
<element name="Remarkable Athlete" type="Archetype Feature" ...>
    <sheet>
        <description>When you make a running long jump, the distance increases by {{strength:modifier}} feet.</description>
    </sheet>
    <rules>
        <stat name="acrobatics:misc" value="proficiency:half:up" requirements="!ID_PROFICIENCY_SKILL_ACROBATICS" />
        <stat name="athletics:misc" value="proficiency:half:up" requirements="!ID_PROFICIENCY_SKILL_ATHLETICS" />
    </rules>
</element>
```

**Feature granting additional selection**:
```xml
<element name="Additional Fighting Style" type="Archetype Feature" ...>
    <sheet><description>You adopt a second style of fighting.</description></sheet>
    <rules>
        <select type="Class Feature" name="Additional Fighting Style" supports="Fighting Style, Fighter" level="10" />
    </rules>
</element>
```

**Feature with computed value**:
```xml
<element name="Survivor" type="Archetype Feature" ...>
    <sheet>
        <description>At the start of each turn, you regain {{survivor:hp}} hp if at half hp or less.</description>
    </sheet>
    <rules>
        <stat name="survivor:hp" value="5" />
        <stat name="survivor:hp" value="constitution:modifier" />
    </rules>
</element>
```

## Spellcasting Archetype (e.g., Eldritch Knight)

When an archetype grants spellcasting, the Archetype Feature that provides it uses the `<spellcasting>` node:

```xml
<element name="Spellcasting" type="Archetype Feature" source="{Source}" id="ID_{...}_ARCHETYPE_FEATURE_{NAME}_SPELLCASTING">
    <description>{Spellcasting description with table}</description>
    <sheet display="false" />
    <spellcasting name="{Archetype Name}" ability="{Intelligence|Wisdom|Charisma}" prepare="{true|false}" allowReplace="{true|false}">
        <list>{Class Spell List},{School Filter}</list>
    </spellcasting>
    <rules>
        <!-- Multiclass spellcasting slot contribution -->
        <grant type="Grants" id="ID_INTERNAL_GRANT_MULTICLASS_SPELLCASTING_SLOTS_THIRD" requirements="ID_INTERNAL_GRANT_MULTICLASS" />

        <!-- Spell slot stats -->
        <stat name="{archetype name lowercase}:spellcasting:slots:1" value="2" level="3" />
        <stat name="{archetype name lowercase}:spellcasting:slots:1" value="1" level="4" />
        <stat name="{archetype name lowercase}:spellcasting:slots:2" value="2" level="7" />
        <!-- etc. -->

        <!-- Cantrip selections -->
        <select type="Spell" name="Cantrip ({Archetype})" supports="{Class}, 0" level="3" number="2" spellcasting="{Archetype Name}" />

        <!-- Spell selections using spellcasting list variable -->
        <select type="Spell" name="Spellcasting ({Archetype})" supports="$(spellcasting:list), $(spellcasting:slots)" level="{N}" spellcasting="{Archetype Name}" />

        <!-- Unrestricted spell choices (any school) at certain levels -->
        <select type="Spell" name="Spellcasting ({Archetype})" supports="({Class}||$(spellcasting:list)), $(spellcasting:slots)" level="{N}" spellcasting="{Archetype Name}" />
    </rules>
</element>
```

### Spellcasting Node Attributes
| Attribute | Values | Description |
|-----------|--------|-------------|
| `name` | text | Display name for the spellcasting section |
| `ability` | `Intelligence`, `Wisdom`, `Charisma` | Spellcasting ability |
| `prepare` | `true`/`false` | Whether the caster prepares spells |
| `allowReplace` | `true`/`false` | Whether spells can be swapped on level up |
| `extend` | `true` | For extending an existing spellcasting list (e.g., domain spells) |

### Spellcasting List
The `<list>` child of `<spellcasting>` defines the filtered spell list:
- `Wizard` — full wizard list
- `Wizard,(Abjuration||Evocation)` — wizard spells, restricted to abjuration and evocation

### Spell Selection Supports Variables
- `$(spellcasting:list)` — resolves to the spellcasting list filter
- `$(spellcasting:slots)` — resolves to the max spell level with available slots

### Multiclass Spellcasting Slot Grants
| Grant ID | Caster Type |
|----------|-------------|
| `ID_INTERNAL_GRANT_MULTICLASS_SPELLCASTING_SLOTS_FULL` | Full caster (Wizard, Cleric, etc.) |
| `ID_INTERNAL_GRANT_MULTICLASS_SPELLCASTING_SLOTS_HALF` | Half caster (Paladin, Ranger) |
| `ID_INTERNAL_GRANT_MULTICLASS_SPELLCASTING_SLOTS_THIRD` | Third caster (Eldritch Knight, Arcane Trickster) |

## Feature Replacement Grants

Place at the end of the archetype file:

```xml
<!--Feature Replacement Grants-->
<element name="{Feature} Feature Replacement" type="Grants" source="Internal" id="ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_{ARCHETYPE}_{FEATURE}" />
```

## File Structure Order
1. Archetype element
2. Archetype Feature elements (in level order)
3. Feature Replacement Grants

## File Naming Convention
`{class}-{archetype-name}.xml`

Examples:
- `fighter-champion.xml`
- `fighter-eldritch-knight.xml`
- `rogue-yuki-assassin.xml`
