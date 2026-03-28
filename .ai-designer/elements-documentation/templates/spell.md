# Spell Template

## Spell Element

```xml
<element name="{Spell Name}" type="Spell" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_SPELL_{NAME}">
    <supports>{Class1}, {Class2}, {Additional Tags}</supports>
    <description>
        <p>{Spell description}</p>
        <p class="indent"><b><i>At Higher Levels.</i></b> {Upcast text}</p>
    </description>
    <setters>
        <set name="keywords">{damage type or keyword tags}</set>
        <set name="level">{0-9}</set>
        <set name="school">{School}</set>
        <set name="time">{Casting time}</set>
        <set name="duration">{Duration}</set>
        <set name="range">{Range}</set>
        <set name="hasVerbalComponent">{true|false}</set>
        <set name="hasSomaticComponent">{true|false}</set>
        <set name="hasMaterialComponent">{true|false}</set>
        <set name="materialComponent">{Component text or empty}</set>
        <set name="isConcentration">{true|false}</set>
        <set name="isRitual">{true|false}</set>
    </setters>
</element>
```

## Required Setters
| Setter | Values | Description |
|--------|--------|-------------|
| `keywords` | `fire`, `cold`, `acid`, etc. | Damage/effect type keywords (can be empty) |
| `level` | `0`–`9` | Spell level (0 = cantrip) |
| `school` | See list below | School of magic |
| `time` | `1 action`, `1 bonus action`, `1 reaction`, `1 minute`, `10 minutes`, `1 hour`, `8 hours`, `24 hours` | Casting time |
| `duration` | `Instantaneous`, `1 round`, `1 minute`, `10 minutes`, `1 hour`, `8 hours`, `24 hours`, `Until dispelled`, `Concentration, up to {duration}` | Duration |
| `range` | `Self`, `Touch`, `30 feet`, `60 feet`, `120 feet`, `150 feet`, `300 feet`, `500 feet`, `1 mile`, `Unlimited`, `Self ({radius}-foot radius)`, `Self ({length}-foot line)`, `Self ({radius}-foot cone)` | Spell range |
| `hasVerbalComponent` | `true`/`false` | V component |
| `hasSomaticComponent` | `true`/`false` | S component |
| `hasMaterialComponent` | `true`/`false` | M component |
| `materialComponent` | text | Material component text (empty if none) |
| `isConcentration` | `true`/`false` | Concentration spell |
| `isRitual` | `true`/`false` | Ritual castable |

## Schools of Magic
- `Abjuration`
- `Conjuration`
- `Divination`
- `Enchantment`
- `Evocation`
- `Illusion`
- `Necromancy`
- `Transmutation`

## Supports (Class Spell Lists)
The `<supports>` node is a comma-separated list that determines which class spell lists include this spell. Common values:
- `Bard`
- `Cleric`
- `Druid`
- `Paladin`
- `Ranger`
- `Sorcerer`
- `Warlock`
- `Wizard`
- `Artificer`

### Additional Support Tags
Used for spell filtering in UI:
- `Spell Saving Throw` — spell requires a saving throw
- `Spell Attack` — spell requires an attack roll

### Example
```xml
<supports>Sorcerer, Wizard, Artificer, Spell Saving Throw</supports>
```

## Common Spell Examples

**Cantrip (level 0)**:
```xml
<element name="Acid Splash" type="Spell" source="Player's Handbook" id="ID_PHB_SPELL_ACID_SPLASH">
    <supports>Sorcerer, Wizard, Artificer, Spell Saving Throw</supports>
    <description>
        <p>You hurl a bubble of acid. Choose one or two creatures within range. A target must succeed on a Dexterity saving throw or take 1d6 acid damage.</p>
        <p class="indent">This spell's damage increases by 1d6 when you reach 5th level (2d6), 11th level (3d6), and 17th level (4d6).</p>
    </description>
    <setters>
        <set name="keywords">acid</set>
        <set name="level">0</set>
        <set name="school">Conjuration</set>
        <set name="time">1 action</set>
        <set name="duration">Instantaneous</set>
        <set name="range">60 feet</set>
        <set name="hasVerbalComponent">true</set>
        <set name="hasSomaticComponent">true</set>
        <set name="hasMaterialComponent">false</set>
        <set name="materialComponent" />
        <set name="isConcentration">false</set>
        <set name="isRitual">false</set>
    </setters>
</element>
```

**Leveled spell with concentration and material**:
```xml
<element name="Alter Self" type="Spell" source="Player's Handbook" id="ID_PHB_SPELL_ALTER_SELF">
    <supports>Sorcerer, Wizard, Artificer</supports>
    <description><p>You assume a different form...</p></description>
    <setters>
        <set name="keywords"></set>
        <set name="level">2</set>
        <set name="school">Transmutation</set>
        <set name="time">1 action</set>
        <set name="duration">Concentration, up to 1 hour</set>
        <set name="range">Self</set>
        <set name="hasVerbalComponent">true</set>
        <set name="hasSomaticComponent">true</set>
        <set name="hasMaterialComponent">false</set>
        <set name="materialComponent" />
        <set name="isConcentration">true</set>
        <set name="isRitual">false</set>
    </setters>
</element>
```

**Ritual spell**:
```xml
<setters>
    <set name="level">1</set>
    <set name="school">Abjuration</set>
    <set name="time">1 minute</set>
    <set name="duration">8 hours</set>
    <set name="range">30 feet</set>
    <set name="hasVerbalComponent">true</set>
    <set name="hasSomaticComponent">true</set>
    <set name="hasMaterialComponent">true</set>
    <set name="materialComponent">a tiny bell and a piece of fine silver wire</set>
    <set name="isConcentration">false</set>
    <set name="isRitual">true</set>
</setters>
```

## Notes
- Spells DO NOT have `<sheet>` or `<rules>` nodes — they are purely informational/selectable elements
- The `keywords` setter is used for search filtering (can be comma-separated for multiple keywords)
- When `hasMaterialComponent` is `false`, set `materialComponent` to empty: `<set name="materialComponent" />`
- Spells are typically grouped in large files per source (e.g., `spells.xml`, `spells-az.xml`)
