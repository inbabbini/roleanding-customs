# Magic Item Template

Magic items use `type="Magic Item"` and cover weapons, armor, wondrous items, potions, scrolls, etc.

## Magic Item Element

```xml
<element name="{Item Name}" type="Magic Item" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_MAGIC_ITEM_{NAME}">
    <description>
        <p>{Description with HTML formatting}</p>
    </description>
    <setters>
        <set name="keywords">{search keywords}</set>
        <set name="category">{Category}</set>
        <set name="cost" currency="gp">{amount}</set>
        <set name="weight" lb="{N}">{N} lb.</set>
        <set name="type" addition="{subtype}">{Base Type}</set>
        <set name="rarity">{Rarity}</set>
        <set name="attunement">{true|false|conditional text}</set>
        <set name="slot">{slot}</set>
        <!-- Type-specific setters -->
    </setters>
    <rules>
        <!-- Optional mechanical effects -->
    </rules>
</element>
```

## Common Setters
| Setter | Attributes | Values | Description |
|--------|-----------|--------|-------------|
| `keywords` | — | comma-separated tags | Search/filter keywords |
| `category` | — | See category table | Display category |
| `cost` | `currency` | `gp` | Cost (usually `0` for magic items) |
| `weight` | `lb` | number | Weight |
| `type` | `addition` | See type table | Item base type + subtype |
| `rarity` | — | See rarity table | Item rarity |
| `attunement` | — | `true`/custom text | Attunement requirement |
| `slot` | — | body slot | Where the item is equipped |

### Rarity Values
| Value | Rarity |
|-------|--------|
| `Common` | Common |
| `Uncommon` | Uncommon |
| `Rare` | Rare |
| `Very Rare` | Very Rare (note: capital R) |
| `Legendary` | Legendary |
| `Artifact` | Artifact |

### Category Values
| Category | Used For |
|----------|----------|
| `Magic Weapons` | Magic weapons |
| `Magic Armor` | Magic armor |
| `Wondrous Items` | Wondrous items |
| `Potions` | Potions |
| `Rings` | Rings |
| `Rods` | Rods |
| `Scrolls` | Scrolls |
| `Staffs` | Staffs |
| `Wands` | Wands |

### Type Values
| Type | Addition | Description |
|------|----------|-------------|
| `Weapon` | `any`, `any sword`, `javelin`, etc. | Magic weapon |
| `Armor` | `light`, `medium`, `heavy`, `shield`, specific armor | Magic armor |
| `Wondrous Item` | — | Wondrous item |
| `Potion` | — | Potion |
| `Ring` | — | Ring |
| `Rod` | — | Rod |
| `Scroll` | — | Scroll |
| `Staff` | — | Staff |
| `Wand` | — | Wand |

The `addition` attribute specifies what base item the magic item applies to.

### Slot Values
| Slot | Items |
|------|-------|
| `neck` | Amulets, necklaces |
| `head` | Helms, circlets |
| `ring` | Rings |
| `feet` | Boots |
| `hands` | Gauntlets, gloves |
| `waist` | Belts |
| `body` | Armor, robes |
| `onehand` | One-handed weapons |
| `twohand` | Two-handed weapons |

### Attunement Values
- `true` — requires attunement (no specific requirements)
- `true` with text content for class/alignment requirements: displayed as "Requires Attunement by a {class/condition}"

## Magic Weapon Setters
| Setter | Description |
|--------|-------------|
| `enhancement` | Enhancement bonus (+1, +2, +3) |
| `weapon` | Weapon filter: weapon name OR internal category/group IDs separated by `\|\|` |
| `name-format` | Display name format using `{{parent}}` and `{{enhancement}}` placeholders |

### Weapon Filter Patterns
- Specific weapon: `Javelin`, `Trident`
- Weapon group: `ID_INTERNAL_WEAPON_GROUP_SWORDS`
- Any weapon: `ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_MELEE||ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_RANGED||ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_MELEE||ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_RANGED`

### Name Format Patterns
- `{{parent}} +{{enhancement}}` → "Longsword +1"
- `{{parent}} of Vengeance` → "Longsword of Vengeance"
- `Javelin of Lightning` → Fixed name

## Magic Armor Setters
| Setter | Description |
|--------|-------------|
| `enhancement` | Enhancement bonus |
| `armor` | Armor filter: armor name OR internal group IDs |
| `name-format` | Display name template |

## Potion Setters
| Setter | Description |
|--------|-------------|
| `stackable` | `true` — potions are stackable |
| `charges` | Number of charges (if applicable) |
| `stash` | With `lb` and `weightless` attrs for container items |

## Examples

**Generic magic weapon** (+1/+2/+3):
```xml
<element name="Weapon, +1" type="Magic Item" source="Dungeon Master's Guide" id="ID_WOTC_DMG_MAGIC_ITEM_WEAPON_1">
    <description><p>You have a +1 bonus to attack and damage rolls.</p></description>
    <setters>
        <set name="category">Magic Weapons</set>
        <set name="cost" currency="gp">0</set>
        <set name="type" addition="any">Weapon</set>
        <set name="rarity">Uncommon</set>
        <set name="enhancement">1</set>
        <set name="weapon">ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_MELEE||ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_RANGED||ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_MELEE||ID_INTERNAL_WEAPON_CATEGORY_MARTIAL_RANGED</set>
        <set name="name-format">{{parent}} +{{enhancement}}</set>
    </setters>
</element>
```

**Specific magic weapon**:
```xml
<element name="Javelin of Lightning" type="Magic Item" source="Dungeon Master's Guide" id="ID_WOTC_DMG_MAGIC_ITEM_JAVELIN_OF_LIGHTNING">
    <description><p>This javelin is a magic weapon. When you hurl it and speak its command word...</p></description>
    <setters>
        <set name="keywords">javelin</set>
        <set name="category">Magic Weapons</set>
        <set name="cost" currency="gp">0</set>
        <set name="type" addition="javelin">Weapon</set>
        <set name="rarity">Uncommon</set>
        <set name="weapon">Javelin</set>
        <set name="name-format">Javelin of Lightning</set>
    </setters>
</element>
```

**Weapon group magic item** (applies to any sword):
```xml
<element name="Sword of Vengeance" type="Magic Item" ...>
    <setters>
        <set name="keywords">sword</set>
        <set name="category">Magic Weapons</set>
        <set name="cost" currency="gp">0</set>
        <set name="type" addition="any sword">Weapon</set>
        <set name="attunement">true</set>
        <set name="rarity">Uncommon</set>
        <set name="enhancement">1</set>
        <set name="weapon">ID_INTERNAL_WEAPON_GROUP_SWORDS</set>
        <set name="name-format">{{parent}} of Vengeance</set>
    </setters>
</element>
```

**Wondrous item (with attunement)**:
```xml
<element name="Amulet of Proof Against Detection and Location" type="Magic Item" ...>
    <setters>
        <set name="keywords">divination, scry</set>
        <set name="category">Wondrous Items</set>
        <set name="cost" currency="gp">0</set>
        <set name="weight" lb="0">0 lb.</set>
        <set name="slot">neck</set>
        <set name="type">Wondrous Item</set>
        <set name="attunement">true</set>
        <set name="rarity">Uncommon</set>
    </setters>
</element>
```

**Wondrous item (with storage)**:
```xml
<element name="Bag of Holding" type="Magic Item" ...>
    <setters>
        <set name="category">Wondrous Items</set>
        <set name="cost" currency="gp">0</set>
        <set name="weight" lb="15">15 lb.</set>
        <set name="stash" lb="500" weightless="true">true</set>
        <set name="type">Wondrous Item</set>
        <set name="rarity">Uncommon</set>
    </setters>
</element>
```

**Potion**:
```xml
<element name="Potion of Healing" type="Magic Item" source="Dungeon Master's Guide" id="ID_WOTC_DMG_MAGIC_ITEM_POTION_OF_HEALING">
    <description><p>You regain 2d4 + 2 hit points when you drink this potion.</p></description>
    <setters>
        <set name="keywords">healing</set>
        <set name="category">Potions</set>
        <set name="cost" currency="gp">50</set>
        <set name="weight" lb="0.5">½ lb.</set>
        <set name="type">Potion</set>
        <set name="rarity">Common</set>
        <set name="stackable">true</set>
    </setters>
</element>
```

**Charged item**:
```xml
<element name="Trident of Fish Command" type="Magic Item" ...>
    <setters>
        <set name="category">Magic Weapons</set>
        <set name="type" addition="trident">Weapon</set>
        <set name="attunement">true</set>
        <set name="rarity">Uncommon</set>
        <set name="weapon">Trident</set>
        <set name="name-format">Trident of Fish Command</set>
        <set name="charges">3</set>
    </setters>
</element>
```

## Notes
- Magic items typically have `cost` set to `0` (priceless)
- Potions always have `stackable` set to `true`
- For magic weapons/armor that apply to a base item, the `weapon`/`armor` setter and `name-format` are essential
- Magic items with mechanical effects (AC bonus, stat changes) include `<rules>` nodes
