# Language Template

## Language Element

```xml
<element name="{Language Name}" type="Language" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_LANGUAGE_{NAME}">
    <supports>{Standard|Exotic}</supports>
    <description>
        <p>Typically spoken by {speakers}.</p>
    </description>
    <setters>
        <set name="standard">{true|false}</set>
        <set name="speakers">{Speaker races/creatures}</set>
        <set name="script">{Script name}</set>
    </setters>
</element>
```

## Required Setters
| Setter | Values | Description |
|--------|--------|-------------|
| `standard` | `true`/`false` | `true` for Standard languages, `false` for Exotic |
| `speakers` | text | Who typically speaks this language |
| `script` | text | Writing system used (can be another language's script) |

## Supports
- `Standard` — Available to most races' language selections
- `Exotic` — Requires special access
- `Custom Race Language` — For Tasha's Customized Language option

Standard languages match `supports="Standard||Exotic"` selections.

## Examples

**Standard language**:
```xml
<element name="Common" type="Language" source="Player's Handbook" id="ID_LANGUAGE_COMMON">
    <supports>Standard</supports>
    <description><p>Typically spoken by humans.</p></description>
    <setters>
        <set name="standard">true</set>
        <set name="speakers">Humans</set>
        <set name="script">Common</set>
    </setters>
</element>
```

**Exotic language**:
```xml
<element name="Abyssal" type="Language" source="Player's Handbook" id="ID_LANGUAGE_ABYSSAL">
    <supports>Exotic</supports>
    <description><p>Typically spoken by demons.</p></description>
    <setters>
        <set name="standard">false</set>
        <set name="speakers">Demons</set>
        <set name="script">Infernal</set>
    </setters>
</element>
```

**Shared script** (multiple languages can use the same script):
- Dwarvish script: used by Dwarvish, Giant, Gnomish
- Elvish script: used by Elvish, Sylvan, Undercommon
- Infernal script: used by Infernal, Abyssal

## Notes
- Languages have no `<sheet>` or `<rules>` nodes
- ID convention: `ID_LANGUAGE_{NAME}` (often without author/source prefix for PHB base languages)
- Custom/homebrew languages should use full ID prefix: `ID_{AUTHOR}_{SOURCE}_LANGUAGE_{NAME}`
