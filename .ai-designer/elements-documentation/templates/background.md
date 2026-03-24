# Background & Background Feature Templates

## Background Element

```xml
<element name="{Background Name}" type="Background" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_BACKGROUND_{NAME}">
    <description>
        <p>{Background description}</p>
        <ul class="unstyled">
            <li><strong>Skill Proficiencies:</strong> {skills}</li>
            <li><strong>Tool Proficiencies:</strong> {tools, if any}</li>
            <li><strong>Languages:</strong> {languages, if any}</li>
            <li><strong>Equipment:</strong> {equipment list}</li>
        </ul>
        <div element="ID_{...}_BACKGROUND_FEATURE_{FEATURE}" />
        <h5>SUGGESTED CHARACTERISTICS</h5>
        <p>{Characteristics intro}</p>
    </description>
    <setters>
        <set name="short">{Skill 1}, {Skill 2}, {Tool/Language summary}</set>
    </setters>
    <rules>
        <!-- Skill proficiencies -->
        <grant type="Proficiency" id="ID_PROFICIENCY_SKILL_{SKILL1}" />
        <grant type="Proficiency" id="ID_PROFICIENCY_SKILL_{SKILL2}" />

        <!-- Tool proficiencies (if any) -->
        <grant type="Proficiency" id="ID_PROFICIENCY_TOOL_PROFICIENCY_{TOOL}" />
        <select type="Proficiency" name="Tool Proficiency ({Background})" supports="{Filter}" />

        <!-- Language selections (if any) -->
        <select type="Language" name="Language ({Background})" number="{N}" supports="Standard||Exotic" />

        <!-- Background feature -->
        <grant type="Background Feature" id="ID_{...}_BACKGROUND_FEATURE_{FEATURE}" requirements="!ID_INTERNAL_GRANT_OPTIONAL_BACKGROUND_FEATURE" />
        <select type="Background Feature" name="Variant Feature" supports="Optional Background Feature" optional="true" />

        <!-- Personality characteristics -->
        <select type="List" name="Personality Trait" number="2">
            <item id="1">{Trait 1}</item>
            <item id="2">{Trait 2}</item>
            <item id="3">{Trait 3}</item>
            <item id="4">{Trait 4}</item>
            <item id="5">{Trait 5}</item>
            <item id="6">{Trait 6}</item>
            <item id="7">{Trait 7}</item>
            <item id="8">{Trait 8}</item>
        </select>
        <select type="List" name="Ideal">
            <item id="1">{Ideal 1} ({Alignment})</item>
            <item id="2">{Ideal 2} ({Alignment})</item>
            <item id="3">{Ideal 3} ({Alignment})</item>
            <item id="4">{Ideal 4} ({Alignment})</item>
            <item id="5">{Ideal 5} ({Alignment})</item>
            <item id="6">{Ideal 6} ({Alignment})</item>
        </select>
        <select type="List" name="Bond">
            <item id="1">{Bond 1}</item>
            <item id="2">{Bond 2}</item>
            <item id="3">{Bond 3}</item>
            <item id="4">{Bond 4}</item>
            <item id="5">{Bond 5}</item>
            <item id="6">{Bond 6}</item>
        </select>
        <select type="List" name="Flaw">
            <item id="1">{Flaw 1}</item>
            <item id="2">{Flaw 2}</item>
            <item id="3">{Flaw 3}</item>
            <item id="4">{Flaw 4}</item>
            <item id="5">{Flaw 5}</item>
            <item id="6">{Flaw 6}</item>
        </select>
    </rules>
</element>
```

## Required Setter
| Setter | Description |
|--------|-------------|
| `short` | Summary of proficiencies: `"Insight, Religion, 2 Languages"` |

## Background Feature Element

```xml
<element name="Feature: {Feature Name}" type="Background Feature" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_BACKGROUND_FEATURE_{NAME}">
    <supports>Background Feature</supports>
    <description>
        <p>{Feature description}</p>
    </description>
    <sheet alt="{Feature Name}" />
</element>
```

### Key Points
- The `name` often starts with `Feature: ` prefix
- `<supports>Background Feature</supports>` is required for the grant to work
- `<sheet alt="{name}" />` displays the feature name on the sheet without the "Feature: " prefix
- Background features are almost always display-only (no rules)

## Variant Feature Support
The background grants the feature with a check against `ID_INTERNAL_GRANT_OPTIONAL_BACKGROUND_FEATURE`:
```xml
<grant type="Background Feature" id="..." requirements="!ID_INTERNAL_GRANT_OPTIONAL_BACKGROUND_FEATURE" />
<select type="Background Feature" name="Variant Feature" supports="Optional Background Feature" optional="true" />
```
This allows players to swap the default feature for an optional one from supplements.

## List Selections
The `<select type="List">` with `<item>` children creates dropdown choices for roleplaying characteristics:
- **Personality Traits**: `number="2"` (select 2)
- **Ideals**: Select 1, items include alignment tag in parentheses
- **Bonds**: Select 1
- **Flaws**: Select 1

Item `id` values are sequential numbers starting from `"1"`.

## Example: Complete Background File

```xml
<?xml version="1.0" encoding="utf-8" ?>
<elements>
    <info>
        <name>{Background Name}</name>
        <update version="0.0.1">
            <file name="background-{name}.xml" url="{url}" />
        </update>
    </info>

    <element name="Acolyte" type="Background" source="Player's Handbook" id="ID_BACKGROUND_ACOLYTE">
        <description>
            <p>You have spent your life in the service of a temple...</p>
            <ul class="unstyled">
                <li><strong>Skill Proficiencies:</strong> Insight, Religion</li>
                <li><strong>Languages:</strong> Two of your choice</li>
                <li><strong>Equipment:</strong> A holy symbol, prayer book...</li>
            </ul>
            <div element="ID_BACKGROUND_FEATURE_SHELTER_OF_THE_FAITHFUL" />
            <h5>SUGGESTED CHARACTERISTICS</h5>
            <p>Acolytes are shaped by their experience...</p>
        </description>
        <setters>
            <set name="short">Insight, Religion, 2 Languages</set>
        </setters>
        <rules>
            <grant type="Proficiency" id="ID_PROFICIENCY_SKILL_INSIGHT" />
            <grant type="Proficiency" id="ID_PROFICIENCY_SKILL_RELIGION" />
            <select type="Language" name="Language (Acolyte)" number="2" supports="Standard||Exotic" />
            <grant type="Background Feature" id="ID_BACKGROUND_FEATURE_SHELTER_OF_THE_FAITHFUL" requirements="!ID_INTERNAL_GRANT_OPTIONAL_BACKGROUND_FEATURE" />
            <select type="Background Feature" name="Variant Feature" supports="Optional Background Feature" optional="true" />
            <select type="List" name="Personality Trait" number="2">
                <item id="1">I idolize a particular hero of my faith...</item>
                <!-- ... -->
            </select>
            <select type="List" name="Ideal">
                <item id="1">Tradition. The ancient traditions must be preserved. (Lawful)</item>
                <!-- ... -->
            </select>
            <select type="List" name="Bond">
                <item id="1">I would die to recover an ancient relic of my faith.</item>
                <!-- ... -->
            </select>
            <select type="List" name="Flaw">
                <item id="1">I judge others harshly, and myself even more severely.</item>
                <!-- ... -->
            </select>
        </rules>
    </element>

    <element name="Feature: Shelter of the Faithful" type="Background Feature" source="Player's Handbook" id="ID_BACKGROUND_FEATURE_SHELTER_OF_THE_FAITHFUL">
        <supports>Background Feature</supports>
        <description><p>You command the respect of those who share your faith...</p></description>
        <sheet alt="Shelter of the Faithful" />
    </element>
</elements>
```

## File Naming Convention
`background-{name}.xml`
