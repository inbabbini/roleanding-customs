# Rules System

The `<rules>` node is where mechanical effects are defined. There are three rule types: **grant**, **select**, and **stat**.

## Grant Rule

Grants a specific element to the character.

```xml
<grant type="{ElementType}" id="{ElementID}" />
```

| Attribute | Required | Description |
|-----------|----------|-------------|
| `type` | Yes | The type of the granted element |
| `id` | Yes | The ID of the granted element |
| `level` | No | Minimum level required for this grant |
| `requirements` | No | Dynamic requirements expression (same syntax as element requirements) |

### Examples
```xml
<!-- Grant a language -->
<grant type="Language" id="ID_LANGUAGE_COMMON" />

<!-- Grant a class feature at level 3 -->
<grant type="Class Feature" id="ID_WOTC_PHB_CLASS_FEATURE_MARTIALARCHETYPE" level="3" />

<!-- Conditional grant -->
<grant type="Proficiency" id="ID_PROFICIENCY_ARMOR_PROFICIENCY_LIGHT_ARMOR" 
       requirements="!ID_WOTC_PHB_MULTICLASS_FIGHTER" />

<!-- Grant a racial trait -->
<grant type="Racial Trait" id="ID_RACIAL_TRAIT_DWARVEN_RESILIENCE" />

<!-- Grant a size -->
<grant type="Size" id="ID_SIZE_MEDIUM" />

<!-- Grant a vision type -->
<grant type="Vision" id="ID_VISION_DARKVISION" />

<!-- Grant a condition/resistance -->
<grant type="Condition" id="ID_INTERNAL_CONDITION_DAMAGE_RESISTANCE_POISON" />

<!-- Grant a spell -->
<grant type="Spell" id="ID_PHB_SPELL_MAGE_ARMOR" />

<!-- Grant an internal flag -->
<grant type="Grants" id="ID_INTERNAL_GRANT_MULTICLASS" />
```

## Select Rule

Creates a selection dropdown for the player to choose from filtered elements.

```xml
<select type="{ElementType}" name="{Display Name}" supports="{Filter}" />
```

| Attribute | Required | Description |
|-----------|----------|-------------|
| `type` | Yes | The type of elements to select from |
| `name` | Yes | Display name on the selection control |
| `supports` | No | Filter expression for elements. Uses supports tags or explicit IDs with `\|` separator |
| `level` | No | Minimum level required for this selection |
| `requirements` | No | Dynamic requirements expression |
| `number` | No | Number of selections allowed (default: 1) |
| `default` | No | ID of element to select by default |
| `optional` | No | `"true"` if the selection is optional |
| `spellcasting` | No | Name of the spellcasting context (for spell selections) |

### Supports Filter Syntax
- **Simple tag**: `"Skill"` — matches elements with `<supports>Skill</supports>`
- **Multi-tag (AND)**: `"Skill,Fighter"` — element must support BOTH tags
- **OR within tag**: `"Standard||Exotic"` — matches either
- **Explicit IDs**: `"ID_A|ID_B|ID_C"` — pipe-separated list of specific IDs
- **Negation**: `"!Tag"` — must NOT have this support
- **Spellcasting variable**: `"$(spellcasting:list)"` — resolved from spellcasting context

### Examples
```xml
<!-- Select a sub race -->
<select type="Sub Race" name="Dwarven Subrace" supports="Dwarf" />

<!-- Select an archetype -->
<select type="Archetype" name="Martial Archetype" supports="Martial Archetype" level="3" />

<!-- Select multiple skills -->
<select type="Proficiency" name="Skill Proficiency (Fighter)" supports="Skill,Fighter" number="2" />

<!-- Select from specific IDs -->
<select type="Proficiency" name="Dwarven Tool Proficiency" 
        supports="ID_PROFICIENCY_TOOL_PROFICIENCY_SMITHS_TOOLS|ID_PROFICIENCY_TOOL_PROFICIENCY_BREWERS_SUPPLIES|ID_PROFICIENCY_TOOL_PROFICIENCY_MASONS_TOOLS" />

<!-- Select a language -->
<select type="Language" name="Language (Acolyte)" number="2" supports="Standard||Exotic" />

<!-- Select a fighting style -->
<select type="Class Feature" name="Fighting Style" supports="Fighting Style, Fighter" level="1" />

<!-- Select an ASI or Feat at class level -->
<select type="Class Feature" name="Improvement Option (Fighter 4)" 
        supports="Improvement Option,Fighter,4" level="4" />

<!-- Optional variant selection -->
<select type="Background Feature" name="Variant Feature" supports="Optional Background Feature" optional="true" />

<!-- Select a feat sub-option -->
<select type="Feat Feature" name="Elemental Adept" supports="Elemental Adept" />

<!-- Select an ability score -->
<select type="Ability Score Improvement" name="Athlete" 
        supports="ID_PHB_FEAT_ASI_STRENGTH|ID_PHB_FEAT_ASI_DEXTERITY" />

<!-- Spell selection with spellcasting context -->
<select type="Spell" name="Cantrip (Eldritch Knight)" supports="Wizard, 0" 
        level="3" number="2" spellcasting="Eldritch Knight" />
<select type="Spell" name="Spellcasting (Eldritch Knight)" 
        supports="$(spellcasting:list), $(spellcasting:slots)" 
        level="4" spellcasting="Eldritch Knight" />

<!-- Background personality lists -->
<select type="List" name="Personality Trait" number="2">
    <item id="1">First trait option.</item>
    <item id="2">Second trait option.</item>
</select>
```

## Stat Rule

Modifies a statistic value on the character.

```xml
<stat name="{StatName}" value="{Value}" />
```

| Attribute | Required | Description |
|-----------|----------|-------------|
| `name` | Yes | The statistic name (case-sensitive). See [Statistics Reference](reference/statistics.md) |
| `value` | Yes | Numeric value OR name of another statistic |
| `bonus` | No | Bonus category for non-stacking. `"base"` for base values, custom names to prevent stacking |
| `equipped` | No | Condition on equipped items: `"[armor:heavy]"`, `"![armor:none]"`, `"[primary:any]"` |
| `level` | No | Minimum level required |
| `requirements` | No | Dynamic requirements expression |
| `inline` | No | `"true"` for non-numeric inline text replacement in sheet descriptions |
| `alt` | No | Alternative description text for the stat on the sheet |

### Examples
```xml
<!-- Simple ability score increase -->
<stat name="strength" value="2" />

<!-- Conditional ASI (for Tasha's customization option) -->
<stat name="constitution" value="2" requirements="!ID_WOTC_TCOE_OPTION_CUSTOMIZED_ASI" />

<!-- Base speed -->
<stat name="innate speed" value="30" bonus="base" />

<!-- Flying speed with armor restriction -->
<stat name="innate speed:fly" value="30" bonus="base" equipped="![armor:heavy]" />

<!-- Speed bonus -->
<stat name="innate speed:misc" value="10" bonus="unarmored movement" />

<!-- AC bonus when dual wielding -->
<stat name="ac:misc" value="1" equipped="[primary:any],[secondary:any],![primary:versatile]" />

<!-- Skill proficiency doubling -->
<stat name="acrobatics:proficiency" value="proficiency" bonus="double" />

<!-- Initiative bonus -->
<stat name="initiative" value="5" />

<!-- HP bonus per level -->
<stat name="hp" value="level" />

<!-- Custom calculated stat for sheet display -->
<stat name="survivor:hp" value="5" />
<stat name="survivor:hp" value="constitution:modifier" />

<!-- Inline text replacement for sheet -->
<stat name="feature:damage type" value="Force" inline="true" />

<!-- Spellcasting slots -->
<stat name="eldritch knight:spellcasting:slots:1" value="2" level="3" />

<!-- Set ability score (magic items) -->
<stat name="strength:score:set" value="19" bonus="base" />
```

### Bonus Categories
When multiple rules set the same stat with the same `bonus` name, only the **highest** value is used (they don't stack). This is crucial for:
- `bonus="base"` — for base values like speed
- `bonus="proficiency"` or `bonus="double"` — for proficiency bonuses
- `bonus="calculation"` — for AC calculations
- Custom names like `bonus="unarmored movement"` — to prevent stacking with similar features

### Equipped Conditions
- `[armor:none]` / `[armor:light]` / `[armor:medium]` / `[armor:heavy]`
- `![armor:heavy]` — NOT heavy armor
- `[primary:any]` — any weapon in primary hand
- `[secondary:any]` — any weapon in secondary hand
- `[shield:any]` — shield equipped

## Custom Stats for Sheet Descriptions

You can create custom stat names and reference them in `<sheet>` descriptions using `{{stat:name}}` syntax. Custom stats are computed by adding all matching `<stat>` rules:

```xml
<rules>
    <stat name="survivor:hp" value="5" />
    <stat name="survivor:hp" value="constitution:modifier" />
</rules>

<!-- In the sheet description: -->
<sheet>
    <description>You regain {{survivor:hp}} hp at the start of each turn...</description>
</sheet>
```

## Spellcasting Node

Declares that this element grants spellcasting ability.

```xml
<spellcasting name="{Name}" ability="{Ability}" prepare="false" allowReplace="true">
    <list>{SpellList},(School1||School2)</list>
</spellcasting>
```

| Attribute | Description |
|-----------|-------------|
| `name` | Name of the spellcasting class (must match stat naming) |
| `ability` | Spellcasting ability: `Intelligence`, `Wisdom`, or `Charisma` |
| `prepare` | Whether this is a prepared caster (`"true"`) or known caster (`"false"`) |
| `allowReplace` | Whether spells can be swapped on level up |

### Extending a Spell List
```xml
<spellcasting name="Wizard" extend="true">
    <extend>Cleric</extend>
</spellcasting>
```
