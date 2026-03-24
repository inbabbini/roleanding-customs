# Class & Class Feature Templates

A class file contains the Class element, all its Class Feature elements, and Feature Replacement Grants at the bottom.

## Class Element

```xml
<element name="{Class Name}" type="Class" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_CLASS_{NAME}">
    <description>
        <p>{Flavor text}</p>
        <h4>{SECTION TITLE}</h4>
        <p>{Section content}</p>
        <h5>QUICK BUILD</h5>
        <p>{Quick build suggestion}</p>
        <h3>CLASS FEATURES</h3>
        <p>As a {class}, you gain the following class features.</p>
        <h5>HIT POINTS</h5>
        <ul class="unstyled">
            <li><strong>Hit Dice:</strong> 1d{N} per {class} level</li>
            <li><strong>Hit Points at 1st Level:</strong> {N} + your Constitution modifier</li>
            <li><strong>Hit Points at Higher Levels:</strong> 1d{N} (or {avg}) + your Constitution modifier per {class} level after 1st</li>
        </ul>
        <h5>PROFICIENCIES</h5>
        <ul class="unstyled mb">
            <li><strong>Armor:</strong> {armor proficiencies}</li>
            <li><strong>Weapons:</strong> {weapon proficiencies}</li>
            <li><strong>Tools:</strong> {tool proficiencies}</li>
        </ul>
        <ul class="unstyled">
            <li><strong>Saving Throws:</strong> {saves}</li>
            <li><strong>Skills:</strong> Choose {N} from {skill list}</li>
        </ul>
        <h5>EQUIPMENT</h5>
        <p>You start with the following equipment:</p>
        <ul>
            <li>{equipment choices}</li>
        </ul>
        <h5 class="caption">THE {CLASS NAME}</h5>
        <table class="class-features">
            <thead>
                <tr><td class="col-5">Level</td><td class="left">Features</td></tr>
            </thead>
            <tr><td> 1st</td><td class="left">{Feature 1}, {Feature 2}</td></tr>
            <tr><td> 2nd</td><td class="left">{Feature}</td></tr>
            <!-- ... all 20 levels ... -->
        </table>
        <!-- Feature descriptions inlined via div references -->
        <div element="ID_{...}_CLASS_FEATURE_{FEATURE}" />
        <div element="ID_{...}_CLASS_FEATURE_{FEATURE}" />
    </description>
    <sheet display="false">
        <description>{Short class description}</description>
    </sheet>
    <setters>
        <set name="short">{Short class description}</set>
        <set name="hd">d{N}</set>
    </setters>
    <rules>
        <!-- Proficiency grants (excluded for multiclass) -->
        <grant type="Proficiency" id="ID_PROFICIENCY_ARMOR_PROFICIENCY_{TYPE}" requirements="!ID_{...}_MULTICLASS_{CLASS}" />
        <grant type="Proficiency" id="ID_PROFICIENCY_WEAPON_PROFICIENCY_{TYPE}" requirements="!ID_{...}_MULTICLASS_{CLASS}" />
        <grant type="Proficiency" id="ID_PROFICIENCY_SAVINGTHROW_{ABILITY}" requirements="!ID_{...}_MULTICLASS_{CLASS}" />
        <select type="Proficiency" name="Skill Proficiency ({Class})" supports="Skill,{Class}" number="{N}" requirements="!ID_{...}_MULTICLASS_{CLASS}" />

        <!-- Class features granted at specific levels -->
        <grant type="Class Feature" id="ID_{...}_CLASS_FEATURE_{FEATURE}" level="1" />
        <grant type="Class Feature" id="ID_{...}_CLASS_FEATURE_{ARCHETYPE_SELECTION}" level="3" />
        <grant type="Class Feature" id="ID_{...}_CLASS_FEATURE_{ASI}" level="4" />
        <grant type="Class Feature" id="ID_{...}_CLASS_FEATURE_{FEATURE}" level="5" />
        <!-- ... -->
    </rules>
    <multiclass id="ID_{AUTHOR}_{SOURCE}_MULTICLASS_{CLASS}">
        <prerequisite>{Ability} 13</prerequisite>
        <requirements>[{ability}:13]</requirements>
        <setters>
            <set name="multiclass proficiencies">{Proficiency list text}</set>
        </setters>
        <rules>
            <grant type="Grants" id="ID_INTERNAL_GRANT_MULTICLASS" />
            <grant type="Proficiency" id="ID_PROFICIENCY_ARMOR_PROFICIENCY_{TYPE}" />
            <!-- Multiclass gets fewer proficiencies than primary class -->
        </rules>
    </multiclass>
</element>
```

## Class Setters
| Setter | Required | Description |
|--------|----------|-------------|
| `short` | Yes | Brief class description |
| `hd` | Yes | Hit die: `d6`, `d8`, `d10`, `d12` |

## Multiclass Node
- Has its own `id` attribute, used as requirement exclusion for primary-class-only grants
- `<prerequisite>` = human-readable text
- `<requirements>` = expression: `[str:13]`, `([str:13]\|\|[dex:13])`, `[cha:13],[str:13]` (AND)
- Always grants `ID_INTERNAL_GRANT_MULTICLASS`
- Grants a subset of the primary class proficiencies

## Class Feature Element

```xml
<element name="{Feature Name}" type="Class Feature" source="{Source}" id="ID_{...}_CLASS_FEATURE_{FEATURE}">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_{FEATURE}</requirements>
    <description>
        <p>{Description}</p>
    </description>
    <sheet action="{Action Type}" usage="{Usage}">
        <description>{Sheet text with {{stat:name}} placeholders}</description>
        <!-- Level-based variants -->
        <description level="{N}">{Text at this level and above}</description>
        <description level="{N}" usage="{New Usage}">{Text at higher level}</description>
    </sheet>
    <rules>
        <!-- Mechanical effects -->
    </rules>
</element>
```

### Common Class Feature Patterns

**Archetype Selection Feature**:
```xml
<element name="{Archetype Category}" type="Class Feature" source="{Source}" id="ID_{...}_CLASS_FEATURE_{ARCHETYPE_SELECTION}">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_{ARCHETYPE_SELECTION}</requirements>
    <description><p>At {N}rd level, you choose an archetype...</p></description>
    <sheet display="false" />
    <rules>
        <select type="Archetype" name="{Archetype Category}" supports="{Archetype Support Tag}" level="{N}" />
    </rules>
</element>
```

**Ability Score Improvement Feature** (with multiple levels):
```xml
<element name="Ability Score Improvement" type="Class Feature" source="{Source}" id="ID_{...}_CLASS_FEATURE_ABILITYSCOREIMPROVEMENT_{CLASS}">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_ABILITY_SCORE_IMPROVEMENT</requirements>
    <compendium display="false" />
    <description><p>When you reach 4th level, and again at {levels}...</p></description>
    <sheet display="false" />
    <rules>
        <select type="Class Feature" name="Improvement Option ({Class} 4)" supports="Improvement Option,{Class},4" level="4" />
        <select type="Class Feature" name="Improvement Option ({Class} 8)" supports="Improvement Option,{Class},8" level="8" />
        <select type="Class Feature" name="Improvement Option ({Class} 12)" supports="Improvement Option,{Class},12" level="12" />
        <select type="Class Feature" name="Improvement Option ({Class} 16)" supports="Improvement Option,{Class},16" level="16" />
        <select type="Class Feature" name="Improvement Option ({Class} 19)" supports="Improvement Option,{Class},19" level="19" />
    </rules>
</element>
```

**Fighting Style Selection Feature**:
```xml
<element name="Fighting Style" type="Class Feature" source="{Source}" id="ID_{...}_CLASS_FEATURE_FIGHTINGSTYLE">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_FIGHTING_STYLE</requirements>
    <description><p>You adopt a particular style of fighting as your specialty...</p></description>
    <rules>
        <select type="Class Feature" name="Fighting Style" supports="Fighting Style, {Class}" level="1" />
    </rules>
</element>
```

**Fighting Style Option** (selectable, shared between classes):
```xml
<element name="{Style Name}" type="Class Feature" source="{Source}" id="ID_{...}_CLASS_FEATURE_FIGHTINGSTYLE_{STYLE}">
    <supports>Fighting Style, Fighter, Paladin, Ranger</supports>
    <description><p>{Description}</p></description>
    <sheet><description>{Sheet text}</description></sheet>
    <rules>
        <!-- Stat bonuses if applicable -->
    </rules>
</element>
```

**Scaling Feature** (value increases with level):
```xml
<element name="Indomitable" type="Class Feature" source="{Source}" id="...">
    <sheet usage="{{indomitable:usage}}/Long Rest">
        <description>{Description}</description>
    </sheet>
    <rules>
        <stat name="indomitable:usage" value="1" level="9" />
        <stat name="indomitable:usage" value="1" level="13" />
        <stat name="indomitable:usage" value="1" level="17" />
    </rules>
</element>
```

**Extra Attack Feature** (overrides with bonus category):
```xml
<rules>
    <stat name="extra attack:count" value="2" level="5" bonus="extra attack" />
    <stat name="extra attack:count" value="3" level="11" bonus="extra attack" />
    <stat name="extra attack:count" value="4" level="20" bonus="extra attack" />
</rules>
```

## Sheet Node Attributes
| Attribute | Values | Description |
|-----------|--------|-------------|
| `display` | `true`/`false` | Whether to show on character sheet |
| `action` | `Action`, `Bonus Action`, `Reaction`, `Free Action` | Action type |
| `usage` | `1/Short Rest`, `2/Long Rest`, `{{stat}}/Day`, etc. | Usage display |
| `alt` | text | Alternative display name |

### Sheet Level-Based Descriptions
Multiple `<description>` children within `<sheet>` — each with a `level` attribute. The system uses the highest level that applies:
```xml
<sheet>
    <description level="5">Attack twice per turn.</description>
    <description level="11">Attack three times per turn.</description>
    <description level="20">Attack four times per turn.</description>
</sheet>
```

## Feature Replacement Grants

Every Class Feature should have a corresponding replacement grant at the end of the file. This allows other elements (archetypes, homebrew) to replace the feature.

```xml
<!--Feature Replacement Grants-->
<element name="{Feature Name} Feature Replacement" type="Grants" source="Internal" id="ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_{FEATURE}" />
```

The Class Feature checks `<requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_{CLASS}_{FEATURE}</requirements>` — when the replacement grant is given, the original feature is disabled.

## File Structure Order
1. Class element
2. Class Feature elements (in level order)
3. Selectable option elements (fighting styles, etc.)
4. Feature Replacement Grants (at the very end)
