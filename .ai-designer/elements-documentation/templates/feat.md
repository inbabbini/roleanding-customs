# Feat & Feat Feature Templates

## Feat Element

```xml
<element name="{Feat Name}" type="Feat" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_FEAT_{NAME}">
    <prerequisite>{Human-readable prerequisite text}</prerequisite>
    <requirements>{Expression}</requirements>
    <description>
        <p><i>Prerequisite: {prerequisite text}</i></p>
        <p>{Description or intro}</p>
        <ul>
            <li>{Benefit 1}</li>
            <li>{Benefit 2}</li>
            <li>{Benefit 3}</li>
        </ul>
    </description>
    <sheet>
        <description>{Sheet text with {{stat}} placeholders}</description>
    </sheet>
    <rules>
        <!-- Stat increases, grants, selections -->
    </rules>
</element>
```

### Feats with No Prerequisites
Omit both `<prerequisite>` and `<requirements>`:
```xml
<element name="Alert" type="Feat" source="Player's Handbook" id="ID_PHB_FEAT_ALERT">
    <description>
        <p>Always on the lookout for danger, you gain the following benefits:</p>
        <ul>
            <li>You gain a +5 bonus to initiative.</li>
            <li>You can't be surprised while you are conscious.</li>
            <li>Other creatures don't gain advantage on attack rolls against you as a result of being unseen.</li>
        </ul>
    </description>
    <sheet>
        <description>You can't be surprised while you are conscious.
        Other creatures don't gain advantage on attack rolls against you from being unseen.</description>
    </sheet>
    <rules>
        <stat name="initiative" value="5" />
    </rules>
</element>
```

### Feats with Prerequisites

**Ability score prerequisite**:
```xml
<prerequisite>Dexterity 13 or higher</prerequisite>
<requirements>[dex:13]</requirements>
```

**Race prerequisite**:
```xml
<prerequisite>Dwarf</prerequisite>
<requirements>ID_RACE_DWARF||ID_SRD_RACE_DWARF</requirements>
```

**Spellcasting prerequisite**:
```xml
<prerequisite>The ability to cast at least one spell</prerequisite>
<requirements>ID_INTERNAL_GRANT_SPELLCASTING||ID_INTERNAL_GRANT_PACT_MAGIC</requirements>
```

**Class/feature prerequisite**:
```xml
<prerequisite>Proficiency with heavy armor</prerequisite>
<requirements>ID_PROFICIENCY_ARMOR_PROFICIENCY_HEAVY_ARMOR</requirements>
```

### Requirement Expressions
| Pattern | Meaning |
|---------|---------|
| `[str:13]` | Strength 13 or higher |
| `[dex:13]` | Dexterity 13 or higher |
| `([str:13]\|\|[dex:13])` | Strength OR Dexterity 13+ |
| `ID_A\|\|ID_B` | Has element A OR element B |
| `ID_A,ID_B` | Has element A AND element B |
| `!ID_A` | Does NOT have element A |

## Common Feat Rule Patterns

**Direct ability score increase**:
```xml
<rules>
    <stat name="charisma" value="1" />
</rules>
```

**Choice of ability score increase** (using ASI elements):
```xml
<rules>
    <select type="Ability Score Improvement" name="Athlete" supports="ID_PHB_FEAT_ASI_STRENGTH|ID_PHB_FEAT_ASI_DEXTERITY" />
</rules>
```

**Granting proficiency**:
```xml
<rules>
    <grant type="Proficiency" id="ID_PROFICIENCY_ARMOR_PROFICIENCY_HEAVY_ARMOR" />
</rules>
```

**Granting a feat feature (sub-element)**:
```xml
<rules>
    <grant type="Feat Feature" id="ID_{...}_FEAT_FEATURE_{NAME}" />
</rules>
```

## Feat Feature Element

For feats that have sub-components or selectable parts:

```xml
<element name="{Feature Name}" type="Feat Feature" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_FEAT_FEATURE_{NAME}">
    <supports>{Parent Feat Support Tag}</supports>
    <description>
        <p>{Description}</p>
    </description>
    <sheet>
        <description>{Sheet text}</description>
    </sheet>
    <rules>
        <!-- Mechanical effects -->
    </rules>
</element>
```

## Feats Granting Spells

```xml
<element name="Magic Initiate" type="Feat" ...>
    <rules>
        <select type="Feat Feature" name="Magic Initiate" supports="Magic Initiate" />
    </rules>
</element>

<!-- One Feat Feature per class choice -->
<element name="Magic Initiate (Bard)" type="Feat Feature" ...>
    <supports>Magic Initiate</supports>
    <rules>
        <select type="Spell" name="Cantrip (Magic Initiate)" supports="0,Bard" number="2" />
        <select type="Spell" name="1st-level Spell (Magic Initiate)" supports="1,Bard" />
    </rules>
</element>
```

## File Structure
- Simple feats: Can be grouped in a single file (e.g., `feats.xml`)
- Complex feats with many sub-elements: Consider a dedicated file (e.g., `feat-{name}.xml`)

## File Naming Convention
- Grouped: `feats.xml` or `feats-{source-abbrev}.xml`
- Individual: `feat-{name}.xml`
