# Race, Sub Race & Racial Trait Templates

Races are among the most complex elements. A typical race file contains:
1. The Race element (base race)
2. Multiple Racial Trait elements (features of the race)
3. One or more Sub Race elements
4. Additional Racial Traits for each sub race

## Race Element

```xml
<element name="{Race Name}" type="Race" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_RACE_{NAME}">
    <description>
        <p class="flavor">{Flavor text}</p>
        <h4>{SECTION TITLE}</h4>
        <p>{Section content}</p>
        <h4>{RACE NAME} NAMES</h4>
        <ul class="unstyled">
            <li><strong>Male Names:</strong> {comma-separated names}</li>
            <li><strong>Female Names:</strong> {comma-separated names}</li>
            <li><strong>Clan Names:</strong> {comma-separated names}</li>
        </ul>
        <h4>{RACE NAME} TRAITS</h4>
        <p>Your {race} character has the following traits.</p>
        <p class="indent"><strong><em>Ability Score Increase.</em></strong> Your {Ability} score increases by {N}.</p>
        <p class="indent"><strong><em>Age.</em></strong> {Age description}.</p>
        <p class="indent"><strong><em>Size.</em></strong> {Size description}. Your size is {Medium/Small}.</p>
        <p class="indent"><strong><em>Speed.</em></strong> Your base walking speed is {N} feet.</p>
        <p class="indent"><strong><em>{Trait Name}.</em></strong> {Trait description}.</p>
        <p class="indent"><strong><em>Languages.</em></strong> You can speak, read, and write {Languages}.</p>
        <p class="indent"><strong><em>Subrace.</em></strong> {Subrace description}.</p>
    </description>
    <sheet display="false" />
    <setters>
        <set name="names" type="male">{Comma-separated names}</set>
        <set name="names" type="female">{Comma-separated names}</set>
        <set name="names" type="clan">{Comma-separated names}</set>
        <set name="names-format">{{name}} {{clan}}</set>
    </setters>
    <rules>
        <!-- Ability Score Increase -->
        <stat name="{ability}" value="{N}" requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />
        <select type="Ability Score Improvement" name="Custom Ability Score Improvement +{N} ({Race})" 
                supports="Custom Ability Score Increase {N}" requirements="ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />

        <!-- Speed -->
        <stat name="innate speed" value="{30}" bonus="base" />

        <!-- Size -->
        <grant type="Size" id="ID_SIZE_MEDIUM" />

        <!-- Vision -->
        <grant type="Vision" id="ID_VISION_DARKVISION" />

        <!-- Languages -->
        <grant type="Language" id="ID_LANGUAGE_COMMON" requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_LANGUAGE" />
        <grant type="Language" id="ID_LANGUAGE_{RACE_LANG}" requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_LANGUAGE" />
        <select type="Language" name="Customized Language" supports="Custom Race Language" number="2" 
                requirements="ID_WOTC_TCOE_OPTION_CUSTOMIZED_LANGUAGE" />

        <!-- Racial Traits -->
        <grant type="Racial Trait" id="ID_{...}_RACIAL_TRAIT_{TRAIT_NAME}" />

        <!-- Subrace selection -->
        <grant type="Racial Trait" id="ID_{...}_RACIAL_TRAIT_{RACE}_SUBRACE" />
    </rules>
</element>
```

## Racial Trait Element

```xml
<element name="{Trait Name}" type="Racial Trait" source="{Source}" id="ID_{...}_RACIAL_TRAIT_{TRAIT_NAME}">
    <description>
        <p>{Full HTML description}</p>
    </description>
    <sheet display="{true/false}">
        <description>{Plain text for character sheet}</description>
    </sheet>
    <rules>
        <!-- Mechanical effects: grants, stats, etc. -->
    </rules>
</element>
```

### Trait Patterns

**Simple trait (displayed on sheet)**:
```xml
<element name="Dwarven Resilience" type="Racial Trait" source="Player's Handbook" id="ID_RACIAL_TRAIT_DWARVEN_RESILIENCE">
    <description><p>You have advantage on saving throws against poison, and you have resistance against poison damage.</p></description>
    <sheet>
        <description>You have advantage on saving throws against poison, and you have resistance against poison damage.</description>
    </sheet>
    <rules>
        <grant type="Condition" id="ID_INTERNAL_CONDITION_DAMAGE_RESISTANCE_POISON" />
    </rules>
</element>
```

**Proficiency-granting trait (hidden from sheet since proficiencies show elsewhere)**:
```xml
<element name="Dwarven Combat Training" type="Racial Trait" source="Player's Handbook" id="ID_RACIAL_TRAIT_DWARVEN_COMBAT_TRAINING">
    <description><p>You have proficiency with the battleaxe, handaxe, light hammer, and warhammer.</p></description>
    <sheet display="false" />
    <rules>
        <grant type="Proficiency" id="ID_PROFICIENCY_WEAPON_PROFICIENCY_BATTLEAXE" />
        <grant type="Proficiency" id="ID_PROFICIENCY_WEAPON_PROFICIENCY_HANDAXE" />
    </rules>
</element>
```

**Subrace selection trait**:
```xml
<element name="Dwarven Subrace" type="Racial Trait" source="Player's Handbook" id="ID_RACIAL_TRAIT_DWARVEN_SUBRACE">
    <description><p>Choose a subrace.</p></description>
    <sheet display="false" />
    <rules>
        <select type="Sub Race" name="Dwarven Subrace" supports="Dwarf" />
    </rules>
</element>
```

## Sub Race Element

```xml
<element name="{Subrace Name}" type="Sub Race" source="{Source}" id="ID_{...}_SUB_RACE_{NAME}">
    <supports>{Parent Race Name}</supports>
    <description>
        <p>{Description}</p>
        <p class="indent"><strong><em>Ability Score Increase.</em></strong> Your {Ability} score increases by {N}.</p>
        <p class="indent"><strong><em>{Feature}.</em></strong> {Description}.</p>
    </description>
    <sheet display="false" />
    <setters>
        <set name="height" modifier="2d4">3'8"</set>
        <set name="weight" modifier="2d6">115 lb.</set>
    </setters>
    <rules>
        <!-- Ability Score Increase -->
        <stat name="{ability}" value="{N}" requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />
        <select type="Ability Score Improvement" name="Custom Ability Score Improvement +{N} ({Subrace})" 
                supports="Custom Ability Score Increase {N}" requirements="ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />

        <!-- Subrace traits -->
        <grant type="Racial Trait" id="ID_{...}_RACIAL_TRAIT_{TRAIT_NAME}" />
    </rules>
</element>
```

### Key Points
- `<supports>` must match the parent Race's name exactly (e.g., `Dwarf`, `Elf`)
- The subrace selection in the Race uses `<select type="Sub Race" supports="{Race Name}">`
- `height` and `weight` setters with `modifier` attribute define random generation
- Sub Race usually has `<sheet display="false" />`

## Required Setters (Race)
| Setter | Description |
|--------|-------------|
| `names` (type="male") | Male first names, comma-separated |
| `names` (type="female") | Female first names, comma-separated |
| `names` (type="clan"/"family") | Family/clan names, comma-separated |
| `names-format` | Name display format using `{{name}}`, `{{clan}}`, `{{family}}` placeholders |

## Required Setters (Sub Race)
| Setter | Description |
|--------|-------------|
| `height` | Base height string (e.g., `3'8"`) with `modifier` attribute for die roll |
| `weight` | Base weight string (e.g., `115 lb.`) with `modifier` attribute for die roll |

## File Structure

A race file contains ALL related elements in order:
1. Race element
2. Racial Traits for the base race
3. First Sub Race
4. Racial Traits for the first sub race
5. Second Sub Race
6. Racial Traits for the second sub race
7. (Optional) `<append>` nodes for extending other elements
