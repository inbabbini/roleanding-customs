# Armor Template

## Armor Element

```xml
<element name="{Armor Name}" type="Armor" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_ARMOR_{WEIGHT}_{NAME}">
    <supports>{Armor Group ID}</supports>
    <description>
        <p>{Description}</p>
    </description>
    <setters>
        <set name="category">Armor</set>
        <set name="cost" currency="gp">{amount}</set>
        <set name="weight" lb="{N}">{N} lb.</set>
        <set name="slot">body</set>
        <set name="armor">{Light|Medium|Heavy}</set>
        <set name="armorClass">{AC formula text}</set>
        <set name="stealth">{Disadvantage}</set>
        <set name="strength">{N}</set>
        <set name="proficiency">{Proficiency ID}</set>
    </setters>
    <rules>
        <grant type="Grants" id="ID_INTERNAL_GRANTS_STEALTH_DISADVANTAGE" />
        <stat name="ac:armored:armor" value="{base AC number}" />
    </rules>
</element>
```

## Required Setters
| Setter | Values | Description |
|--------|--------|-------------|
| `category` | `Armor` | Always "Armor" |
| `cost` | number | Cost in gp |
| `weight` | number + text | Weight |
| `slot` | `body` | Always "body" for armor |
| `armor` | `Light`, `Medium`, `Heavy` | Armor weight class |
| `armorClass` | descriptive text | AC formula display (e.g., `11 + Dex modifier`) |
| `proficiency` | ID | Armor proficiency ID |

### Optional Setters
| Setter | Values | Description |
|--------|--------|-------------|
| `stealth` | `Disadvantage` | If the armor imposes stealth disadvantage |
| `strength` | number | Minimum strength requirement (heavy armor) |

## Supports (Armor Groups)
| ID | Group |
|----|-------|
| `ID_INTERNAL_ARMOR_GROUP_LIGHT` | Light Armor |
| `ID_INTERNAL_ARMOR_GROUP_MEDIUM` | Medium Armor |
| `ID_INTERNAL_ARMOR_GROUP_HEAVY` | Heavy Armor |
| `ID_INTERNAL_ARMOR_GROUP_SHIELD` | Shields |

## Rules
Armor always has a `<rules>` node setting the base AC:

```xml
<rules>
    <stat name="ac:armored:armor" value="{base AC number}" />
</rules>
```

The `ac:armored:armor` stat represents the base armor number. The system adds the Dexterity modifier automatically based on armor type.

### Stealth Disadvantage
```xml
<rules>
    <grant type="Grants" id="ID_INTERNAL_GRANTS_STEALTH_DISADVANTAGE" />
    <stat name="ac:armored:armor" value="{N}" />
</rules>
```

## Examples

**Light Armor**:
```xml
<element name="Leather" type="Armor" source="Player's Handbook" id="ID_WOTC_ARMOR_LIGHT_LEATHER">
    <supports>ID_INTERNAL_ARMOR_GROUP_LIGHT</supports>
    <description><p>The breastplate and shoulder protectors are made of leather boiled in oil.</p></description>
    <setters>
        <set name="category">Armor</set>
        <set name="cost" currency="gp">10</set>
        <set name="weight" lb="10">10 lb.</set>
        <set name="slot">body</set>
        <set name="armor">Light</set>
        <set name="armorClass">11 + Dex modifier</set>
        <set name="proficiency">ID_PROFICIENCY_ARMOR_PROFICIENCY_LEATHER</set>
    </setters>
    <rules>
        <stat name="ac:armored:armor" value="11" />
    </rules>
</element>
```

**Medium Armor (with stealth disadvantage)**:
```xml
<element name="Half Plate" type="Armor" source="Player's Handbook" id="ID_WOTC_ARMOR_MEDIUM_HALF_PLATE">
    <supports>ID_INTERNAL_ARMOR_GROUP_MEDIUM</supports>
    <setters>
        <set name="category">Armor</set>
        <set name="cost" currency="gp">750</set>
        <set name="weight" lb="40">40 lb.</set>
        <set name="slot">body</set>
        <set name="armor">Medium</set>
        <set name="armorClass">15 + Dex modifier (max 2)</set>
        <set name="stealth">Disadvantage</set>
        <set name="proficiency">ID_PROFICIENCY_ARMOR_PROFICIENCY_HALF_PLATE</set>
    </setters>
    <rules>
        <grant type="Grants" id="ID_INTERNAL_GRANTS_STEALTH_DISADVANTAGE" />
        <stat name="ac:armored:armor" value="15" />
    </rules>
</element>
```

**Heavy Armor (with strength requirement and stealth)**:
```xml
<element name="Chain Mail" type="Armor" source="Player's Handbook" id="ID_WOTC_ARMOR_HEAVY_CHAIN_MAIL">
    <supports>ID_INTERNAL_ARMOR_GROUP_HEAVY</supports>
    <setters>
        <set name="category">Armor</set>
        <set name="cost" currency="gp">75</set>
        <set name="weight" lb="55">55 lb.</set>
        <set name="slot">body</set>
        <set name="armor">Heavy</set>
        <set name="armorClass">16</set>
        <set name="stealth">Disadvantage</set>
        <set name="strength">13</set>
        <set name="proficiency">ID_PROFICIENCY_ARMOR_PROFICIENCY_CHAIN_MAIL</set>
    </setters>
    <rules>
        <grant type="Grants" id="ID_INTERNAL_GRANTS_STEALTH_DISADVANTAGE" />
        <stat name="ac:armored:armor" value="16" />
    </rules>
</element>
```

**Shield**:
```xml
<element name="Shield" type="Armor" source="Player's Handbook" id="ID_WOTC_ARMOR_SHIELD">
    <supports>ID_INTERNAL_ARMOR_GROUP_SHIELD</supports>
    <setters>
        <set name="category">Armor</set>
        <set name="cost" currency="gp">10</set>
        <set name="weight" lb="6">6 lb.</set>
        <set name="slot">onehand</set>
        <set name="armor">Shield</set>
        <set name="armorClass">+2</set>
        <set name="proficiency">ID_PROFICIENCY_ARMOR_PROFICIENCY_SHIELDS</set>
    </setters>
    <rules>
        <stat name="ac:shield" value="2" bonus="shield" />
    </rules>
</element>
```

### Shield Note
Shields use `slot="onehand"` (not "body") and `ac:shield` stat (not `ac:armored:armor`).

## Armor Class Display Text Convention
| Armor Type | armorClass Format |
|-----------|-------------------|
| Light | `{N} + Dex modifier` |
| Medium | `{N} + Dex modifier (max 2)` |
| Heavy | `{N}` |
| Shield | `+2` |
