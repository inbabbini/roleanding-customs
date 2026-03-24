# Option Template

Options are toggleable campaign/character customization choices that appear in the Options panel. They enable or disable variant rules.

## Option Element

```xml
<element name="{Option Name}" type="Option" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_OPTION_{NAME}">
    <description>
        <p>{Description of the optional rule}</p>
    </description>
    <setters>
        <set name="short">{Brief summary of the option}</set>
    </setters>
</element>
```

## Required Setter
| Setter | Description |
|--------|-------------|
| `short` | Summary text displayed in the options panel |

## How Options Work
Options are simple toggle elements. They don't have `<rules>` themselves — instead, other elements reference the Option's ID in their `requirements` to conditionally enable/disable behavior.

### Pattern: Other elements check for the option
```xml
<!-- In a race element: standard ASI -->
<stat name="constitution" value="2" requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />

<!-- In a race element: customized ASI (only active when option is toggled) -->
<select type="Ability Score Improvement" name="Custom Ability Score Improvement +2 (Dwarf)"
        supports="Custom Ability Score Increase 2" requirements="ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />
```

When the user enables the option in the builder, `ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI` becomes active, so:
- Lines with `requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI"` are **disabled**
- Lines with `requirements="ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI"` are **enabled**

## Examples

**Variant rule option (Tasha's Customized ASI)**:
```xml
<element name="Customized Ability Score Increases" type="Option" source="Tasha's Cauldron of Everything" id="ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI">
    <description>
        <p>If you'd like your character to follow their own path, you may ignore your Ability Score Increase trait and assign ability score increases tailored to your character.</p>
    </description>
    <setters>
        <set name="short">If you'd like your character to follow their own path, you may ignore your Ability Score Increase trait and assign ability score increases tailored to your character.</set>
    </setters>
</element>
```

**Content-enabling option (Firearms)**:
```xml
<element name="Firearms" type="Option" source="Dungeon Master's Guide" id="ID_WOTC_DMG_OPTION_FIREARMS">
    <description>
        <p>You can introduce gunpowder weapons to your campaign associated with the Renaissance.</p>
    </description>
    <setters>
        <set name="short">You can introduce gunpowder, futuristic, or modern firearms to your campaign.</set>
    </setters>
</element>
```

**Race restriction option** (e.g., restricting an archetype to elves):
```xml
<element name="Bladesinger" type="Option" source="Sword Coast Adventurer's Guide" id="ID_WOTC_SCAG_OPTION_BLADESINGING">
    <description>
        <p>Styles of bladesinging are broadly associated with the various subraces of elves...</p>
    </description>
    <setters>
        <set name="short">Styles of bladesinging are broadly associated with the various subraces of elves.</set>
    </setters>
</element>
```

## Notes
- Options are often used alongside `<append>` to extend other elements:
  ```xml
  <!-- Adding Custom Race Language support when the option is toggled -->
  <append id="ID_LANGUAGE_COMMON">
      <supports>Custom Race Language</supports>
  </append>
  ```
- Options have no `<sheet>`, `<rules>`, or `<supports>` nodes
- The Option itself is a passive toggle — all logic is in the consuming elements' `requirements`
