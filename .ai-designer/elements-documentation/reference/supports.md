# Supports Reference

The `<supports>` node defines what an element matches against. It serves two purposes:
1. **Filtering**: For elements selected via `<select>`, supports determines what appears in the selection
2. **Classification**: For items/weapons, supports defines categories and properties

## How Supports Matching Works

A `<select>` rule has a `supports` attribute that defines a filter expression. An element matches if its `<supports>` node satisfies the expression.

### Match Rules
- Comma-separated values in `supports` attribute = AND (all must match)
- `||` in the supports attribute = OR (at least one must match)
- The element's `<supports>` node contains comma-separated tags

### Example
```xml
<!-- In the Fighter class: -->
<select type="Class Feature" name="Fighting Style" supports="Fighting Style, Fighter" />

<!-- This matches elements where supports contains BOTH "Fighting Style" AND "Fighter": -->
<element name="Archery" type="Class Feature" ...>
    <supports>Fighting Style, Fighter, Ranger</supports>
</element>
<!-- ✓ Matches: has "Fighting Style" AND "Fighter" -->

<element name="Blessed Warrior" type="Class Feature" ...>
    <supports>Fighting Style, Paladin</supports>
</element>
<!-- ✗ Does NOT match: has "Fighting Style" but NOT "Fighter" -->
```

## Common Supports Patterns by Element Type

### Archetype
Match the parent class's archetype selection name:
```xml
<supports>Martial Archetype</supports>       <!-- Fighter -->
<supports>Roguish Archetype</supports>        <!-- Rogue -->
<supports>Arcane Tradition</supports>          <!-- Wizard -->
<supports>Divine Domain</supports>             <!-- Cleric -->
<supports>Sacred Oath</supports>               <!-- Paladin -->
<supports>Ranger Archetype</supports>          <!-- Ranger -->
<supports>Primal Path</supports>               <!-- Barbarian -->
<supports>Bard College</supports>              <!-- Bard -->
<supports>Druid Circle</supports>              <!-- Druid -->
<supports>Monastic Tradition</supports>        <!-- Monk -->
<supports>Sorcerous Origin</supports>          <!-- Sorcerer -->
<supports>Otherworldly Patron</supports>       <!-- Warlock -->
```

### Class Feature (Selectable)
Multi-tag supports for sharing between classes:
```xml
<supports>Fighting Style, Fighter</supports>
<supports>Fighting Style, Fighter, Ranger</supports>
<supports>Fighting Style, Fighter, Paladin, Ranger</supports>
```

### Sub Race
Match the parent race name:
```xml
<supports>Dwarf</supports>
<supports>Elf</supports>
<supports>Halfling</supports>
```

### Spell
Class spell lists + optional tags:
```xml
<supports>Wizard</supports>
<supports>Cleric, Paladin</supports>
<supports>Sorcerer, Wizard, Artificer, Spell Saving Throw</supports>
<supports>Bard, Cleric, Druid, Paladin, Ranger, Sorcerer, Warlock, Wizard</supports>
```

### Language
```xml
<supports>Standard</supports>
<supports>Exotic</supports>
<supports>Custom Race Language</supports>    <!-- Added via append for Tasha's option -->
```

### Background Feature
```xml
<supports>Background Feature</supports>
<supports>Optional Background Feature</supports>
```

### Companion
```xml
<supports>Familiar</supports>
<supports>Familiar, Variant Familiar</supports>
<supports>Beast Companion</supports>
```

### Weapon
Internal IDs for category, damage type, properties, and group:
```xml
<supports>ID_INTERNAL_WEAPON_CATEGORY_SIMPLE_MELEE, ID_INTERNAL_DAMAGE_TYPE_BLUDGEONING, ID_INTERNAL_WEAPON_PROPERTY_LIGHT, ID_INTERNAL_WEAPON_GROUP_CLUBS</supports>
```

### Armor
Internal ID for armor group:
```xml
<supports>ID_INTERNAL_ARMOR_GROUP_LIGHT</supports>
<supports>ID_INTERNAL_ARMOR_GROUP_MEDIUM</supports>
<supports>ID_INTERNAL_ARMOR_GROUP_HEAVY</supports>
<supports>ID_INTERNAL_ARMOR_GROUP_SHIELD</supports>
```

## Select Supports Expressions

### Skill Selection with Class Filter
```xml
<select type="Proficiency" name="Skill Proficiency (Fighter)" supports="Skill,Fighter" number="2" />
```
Matches Proficiency elements that have both `Skill` and `Fighter` in their supports.

### Language Selection
```xml
<select type="Language" name="Language" supports="Standard||Exotic" />
```
Matches languages that have `Standard` OR `Exotic` in their supports.

### Ability Score Improvement
```xml
<select type="Ability Score Improvement" name="Athlete" supports="ID_PHB_FEAT_ASI_STRENGTH|ID_PHB_FEAT_ASI_DEXTERITY" />
```
The `|` in select supports is used for matching specific element IDs (differs from `||` OR logic).

### Improvement Option (ASI/Feat)
```xml
<select type="Class Feature" name="Improvement Option (Fighter 4)" supports="Improvement Option,Fighter,4" level="4" />
```

### Spell Selection with Spellcasting Variables
```xml
<!-- Restricted to the spellcasting list (school-filtered) -->
<select type="Spell" supports="$(spellcasting:list), $(spellcasting:slots)" spellcasting="Eldritch Knight" />

<!-- Unrestricted (any school from the class list) -->
<select type="Spell" supports="(Wizard||$(spellcasting:list)), $(spellcasting:slots)" spellcasting="Eldritch Knight" />

<!-- Cantrips from a class list -->
<select type="Spell" supports="Wizard, 0" spellcasting="Eldritch Knight" />
```

## Parenthetical Grouping
Supports expressions support parentheses for grouping:
```xml
supports="(Wizard||$(spellcasting:list)), $(spellcasting:slots)"
```
This means: (Wizard OR the spellcasting list filter) AND the max available spell level.

## Adding Supports via Append
You can add supports to existing elements without modifying the original:
```xml
<append id="ID_LANGUAGE_COMMON">
    <supports>Custom Race Language</supports>
</append>
```
This adds `Custom Race Language` to Common's existing supports, so it now matches `supports="Custom Race Language"` selections.
