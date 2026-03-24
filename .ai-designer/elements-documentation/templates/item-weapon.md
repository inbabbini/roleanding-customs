# Weapon Template

## Weapon Element

```xml
<element name="{Weapon Name}" type="Weapon" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_WEAPON_{NAME}">
    <supports>{Category ID}, {DamageType ID}, {Property IDs}, {Group ID}</supports>
    <description>
        <p>{Description or empty}</p>
    </description>
    <setters>
        <set name="category">Weapons</set>
        <set name="cost" currency="{gp|sp|cp}">{amount}</set>
        <set name="weight" lb="{N}">{N} lb.</set>
        <set name="slot">{onehand|twohand}</set>
        <set name="range">{short/long}</set>
        <set name="damage" type="{bludgeoning|piercing|slashing}">{die}</set>
        <set name="proficiency">{Proficiency ID}</set>
    </setters>
</element>
```

## Required Setters
| Setter | Attributes | Values | Description |
|--------|-----------|--------|-------------|
| `category` | — | `Weapons` | Always "Weapons" |
| `cost` | `currency` | `gp`, `sp`, `cp` | Cost with currency attribute |
| `weight` | `lb` | number | Weight (numeric lb attr + display text) |
| `slot` | — | `onehand`, `twohand` | Weapon grip type |
| `damage` | `type` | `bludgeoning`, `piercing`, `slashing` | Damage die and type |
| `proficiency` | — | ID | Proficiency ID for this weapon |
| `range` | — | `20/60`, `30/120`, etc. | Only for thrown/ranged weapons |

## Supports (Weapon Classification)

The `<supports>` node contains comma-separated IDs that classify the weapon.

### Weapon Categories
| ID | Category |
|----|----------|
| `ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_MELEE` | Simple Melee |
| `ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_RANGED` | Simple Ranged |
| `ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_MELEE` | Martial Melee |
| `ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_RANGED` | Martial Ranged |

### Damage Types
| ID | Type |
|----|------|
| `ID_INTERNAL_DAMAGE_TYPE_BLUDGEONING` | Bludgeoning |
| `ID_INTERNAL_DAMAGE_TYPE_PIERCING` | Piercing |
| `ID_INTERNAL_DAMAGE_TYPE_SLASHING` | Slashing |

### Weapon Properties
| ID | Property |
|----|----------|
| `ID_INTERNAL_WEAPON_PROPERTY_AMMUNITION` | Ammunition |
| `ID_INTERNAL_WEAPON_PROPERTY_FINESSE` | Finesse |
| `ID_INTERNAL_WEAPON_PROPERTY_HEAVY` | Heavy |
| `ID_INTERNAL_WEAPON_PROPERTY_LIGHT` | Light |
| `ID_INTERNAL_WEAPON_PROPERTY_LOADING` | Loading |
| `ID_INTERNAL_WEAPON_PROPERTY_REACH` | Reach |
| `ID_INTERNAL_WEAPON_PROPERTY_SPECIAL` | Special |
| `ID_INTERNAL_WEAPON_PROPERTY_THROWN` | Thrown |
| `ID_INTERNAL_WEAPON_PROPERTY_TWOHANDED` | Two-Handed |
| `ID_INTERNAL_WEAPON_PROPERTY_VERSATILE` | Versatile |

### Weapon Groups
| ID | Group |
|----|-------|
| `ID_INTERNAL_WEAPON_GROUP_AXES` | Axes |
| `ID_INTERNAL_WEAPON_GROUP_CLUBS` | Clubs |
| `ID_INTERNAL_WEAPON_GROUP_FLAILS` | Flails |
| `ID_INTERNAL_WEAPON_GROUP_HAMMERS` | Hammers |
| `ID_INTERNAL_WEAPON_GROUP_MACES` | Maces |
| `ID_INTERNAL_WEAPON_GROUP_PICKS` | Picks |
| `ID_INTERNAL_WEAPON_GROUP_POLEARMS` | Polearms |
| `ID_INTERNAL_WEAPON_GROUP_SPEARS` | Spears |
| `ID_INTERNAL_WEAPON_GROUP_STAFFS` | Staffs |
| `ID_INTERNAL_WEAPON_GROUP_SWORDS` | Swords |
| `ID_INTERNAL_WEAPON_GROUP_WHIPS` | Whips |
| `ID_INTERNAL_WEAPON_GROUP_CROSSBOWS` | Crossbows |
| `ID_INTERNAL_WEAPON_GROUP_BOWS` | Bows |

## Examples

**Simple melee weapon**:
```xml
<element name="Club" type="Weapon" source="Player's Handbook" id="ID_WOTC_PHB_WEAPON_CLUB">
    <supports>ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_MELEE, ID_INTERNAL_DAMAGE_TYPE_BLUDGEONING, ID_INTERNAL_WEAPON_PROPERTY_LIGHT, ID_INTERNAL_WEAPON_GROUP_CLUBS</supports>
    <description><p></p></description>
    <setters>
        <set name="category">Weapons</set>
        <set name="cost" currency="sp">1</set>
        <set name="weight" lb="2">2 lb.</set>
        <set name="slot">onehand</set>
        <set name="damage" type="bludgeoning">1d4</set>
        <set name="proficiency">ID_PROFICIENCY_WEAPON_PROFICIENCY_CLUB</set>
    </setters>
</element>
```

**Thrown weapon with range**:
```xml
<element name="Dagger" type="Weapon" source="Player's Handbook" id="ID_WOTC_PHB_WEAPON_DAGGER">
    <supports>ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_MELEE, ID_INTERNAL_DAMAGE_TYPE_PIERCING, ID_INTERNAL_WEAPON_PROPERTY_FINESSE, ID_INTERNAL_WEAPON_PROPERTY_LIGHT, ID_INTERNAL_WEAPON_PROPERTY_THROWN</supports>
    <description><p></p></description>
    <setters>
        <set name="category">Weapons</set>
        <set name="cost" currency="gp">2</set>
        <set name="weight" lb="1">1 lb.</set>
        <set name="slot">onehand</set>
        <set name="range">20/60</set>
        <set name="damage" type="piercing">1d4</set>
        <set name="proficiency">ID_PROFICIENCY_WEAPON_PROFICIENCY_DAGGER</set>
    </setters>
</element>
```

**Two-handed martial weapon**:
```xml
<element name="Greataxe" type="Weapon" ...>
    <supports>ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_MELEE, ID_INTERNAL_DAMAGE_TYPE_SLASHING, ID_INTERNAL_WEAPON_PROPERTY_HEAVY, ID_INTERNAL_WEAPON_PROPERTY_TWOHANDED, ID_INTERNAL_WEAPON_GROUP_AXES</supports>
    <setters>
        <set name="category">Weapons</set>
        <set name="cost" currency="gp">30</set>
        <set name="weight" lb="7">7 lb.</set>
        <set name="slot">twohand</set>
        <set name="damage" type="slashing">1d12</set>
        <set name="proficiency">ID_PROFICIENCY_WEAPON_PROFICIENCY_GREATAXE</set>
    </setters>
</element>
```

## Notes
- Weapons usually have empty `<description>` (`<p></p>`)
- Weapons do NOT have `<sheet>` or `<rules>` nodes
- The weapon group ID is used by magic items to filter applicable weapon types
- `proficiency` setter links to the corresponding weapon proficiency grant ID
