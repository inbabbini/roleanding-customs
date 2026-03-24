# Adventuring Gear (Item) Template

## Item Element

```xml
<element name="{Item Name}" type="Item" source="{Source}" id="ID_{AUTHOR}_{SOURCE}_ITEM_{NAME}">
    <description>
        <p>{Description}</p>
    </description>
    <setters>
        <set name="category">{Category}</set>
        <set name="cost" currency="{gp|sp|cp}">{amount}</set>
        <set name="weight" lb="{N}">{N} lb.</set>
        <set name="stackable">true</set>
        <set name="type">{Type override}</set>
    </setters>
</element>
```

## Required Setters
| Setter | Attributes | Description |
|--------|-----------|-------------|
| `category` | — | Display category (see table below) |
| `cost` | `currency` (gp/sp/cp), optional `bulk` | Item cost. `bulk` attribute shows pack pricing |
| `weight` | `lb` (numeric) | Weight, text value is display format |

## Optional Setters
| Setter | Values | Description |
|--------|--------|-------------|
| `stackable` | `true` | Item can be stacked (most gear is stackable) |
| `type` | `Ammunition`, etc. | Overrides display category/type |

## Category Values
| Category | Used For |
|----------|----------|
| `Adventuring Gear` | General items |
| `Ammunition` | Arrows, bolts, bullets |
| `Arcane Focus` | Arcane foci |
| `Druidic Focus` | Druidic foci |
| `Holy Symbol` | Holy symbols |
| `Musical Instrument` | Instruments |
| `Gaming Set` | Gaming sets |
| `Artisan's Tools` | Artisan tools |
| `Mounts and Vehicles` | Mounts and vehicles |

## Cost Attribute Notes
- `currency`: `gp`, `sp`, `cp`
- `bulk`: For items sold in packs. The cost is per-unit but `bulk` shows the pack quantity with the pack price. E.g., `<set name="cost" currency="cp" bulk="50">2</set>` = 2 cp per unit, sold in packs of 50

## Examples

**Basic item**:
```xml
<element name="Abacus" type="Item" source="Player's Handbook" id="ID_WOTC_PHB_ITEM_ABACUS">
    <description><p>A standard tool used to make calculations.</p></description>
    <setters>
        <set name="category">Adventuring Gear</set>
        <set name="cost" currency="gp">2</set>
        <set name="weight" lb="2">2 lb.</set>
        <set name="stackable">true</set>
    </setters>
</element>
```

**Ammunition**:
```xml
<element name="Arrow" type="Item" source="Player's Handbook" id="ID_WOTC_PHB_ITEM_ARROW">
    <description><p>Arrows are used with a bow to make a ranged attack.</p></description>
    <setters>
        <set name="category">Ammunition</set>
        <set name="cost" currency="cp">5</set>
        <set name="weight" lb="0.05">1/20 lb.</set>
        <set name="type">Ammunition</set>
        <set name="stackable">true</set>
    </setters>
</element>
```

**Bulk pricing item**:
```xml
<element name="Blowgun Needle" type="Item" ...>
    <setters>
        <set name="category">Ammunition</set>
        <set name="cost" currency="cp" bulk="50">2</set>
        <set name="weight" lb="0.02">1/50 lb.</set>
        <set name="type">Ammunition</set>
        <set name="stackable">true</set>
    </setters>
</element>
```

## Notes
- Items do NOT have `<sheet>`, `<rules>`, or `<supports>` nodes
- Weight display text uses fractions for small items (`1/20 lb.`)
- The `lb` attribute must be the decimal equivalent of the display fraction
