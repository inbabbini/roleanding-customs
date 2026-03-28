# Element Anatomy

Every Aurora element follows a consistent XML structure. This document covers the universal parts of an element.

## Basic Structure

```xml
<element name="{Name}" type="{Type}" source="{Source Name}" id="{Unique ID}">
    <compendium display="false" />              <!-- optional -->
    <prerequisite>{Human-readable prereq}</prerequisite> <!-- optional -->
    <requirements>{Machine-readable prereqs}</requirements> <!-- optional -->
    <supports>{Comma-separated support tags}</supports> <!-- optional -->
    <description>
        <!-- HTML content for the builder panel -->
    </description>
    <sheet display="true" alt="{Alt Name}" action="{Action Type}" usage="{Usage}">
        <description>{Plain text for the character sheet}</description>
        <description level="6">{Level-dependent description}</description>
    </sheet>
    <setters>
        <set name="{key}">{value}</set>
    </setters>
    <spellcasting name="{Name}" ability="{Ability}"> <!-- only for spellcasting classes/archetypes -->
        <list>{Spell List}</list>
    </spellcasting>
    <multiclass id="{Multiclass ID}">            <!-- only for classes -->
        <prerequisite>{Text}</prerequisite>
        <requirements>{Expression}</requirements>
        <setters>...</setters>
        <rules>...</rules>
    </multiclass>
    <rules>
        <grant type="{Type}" id="{ID}" level="{N}" requirements="{Expr}" />
        <select type="{Type}" name="{Name}" supports="{Filter}" number="{N}" level="{N}" />
        <stat name="{Stat}" value="{Value}" bonus="{Bonus}" level="{N}" />
    </rules>
</element>
```

## Required Attributes (on `<element>`)

| Attribute | Description |
|-----------|-------------|
| `name`    | Display name in the builder and character sheet. Can be any text. |
| `type`    | Determines where the element appears in the builder. Must be a known type (see Element Types below). |
| `source`  | The name of the published source. Must match the `name` attribute of a Source element. |
| `id`      | Globally unique identifier. Format: `ID_{AUTHOR}_{SOURCE}_{TYPE}_{NAME}`. Only letters, numbers, and underscores. |

## Known Element Types

| Type | Description |
|------|-------------|
| `Source` | Metadata about a content source (book, supplement, homebrew) |
| `Race` | A playable race |
| `Sub Race` | A subrace option for a race |
| `Racial Trait` | A feature granted by a race or subrace |
| `Class` | A playable class |
| `Class Feature` | A feature granted by a class |
| `Archetype` | A subclass for a class |
| `Archetype Feature` | A feature granted by an archetype |
| `Feat` | A feat |
| `Feat Feature` | A sub-option within a feat (e.g., Elemental Adept damage types) |
| `Spell` | A spell |
| `Background` | A character background |
| `Background Feature` | A feature granted by a background |
| `Language` | A language |
| `Proficiency` | A proficiency (skill, weapon, armor, tool, saving throw) |
| `Weapon` | A mundane weapon |
| `Armor` | A mundane armor piece |
| `Item` | A mundane gear/item |
| `Magic Item` | A magical item (weapon, armor, wondrous, potion, etc.) |
| `Companion` | A companion creature |
| `Companion Trait` | A passive trait of a companion |
| `Companion Action` | An action a companion can take |
| `Companion Reaction` | A reaction a companion can take |
| `Option` | A character option (campaign rules, variant features) |
| `Grants` | An internal element for feature replacement flags |
| `Information` | A display-only element for reference text |
| `Ability Score Improvement` | An ASI selection option |
| `Vision` | A vision type (Darkvision, etc.) |
| `Size` | A size category |
| `Condition` | A condition or resistance |

## Child Nodes

### `<compendium>`
Hides the element from compendium search results. Used for internal/helper elements.
```xml
<compendium display="false" />
```

### `<prerequisite>`
Human-readable prerequisite text displayed to the user.
```xml
<prerequisite>Dexterity 13 or higher</prerequisite>
```

### `<requirements>`
Machine-readable requirement expression. Supports:
- Element IDs: `ID_SOME_ELEMENT`
- AND: `,` or `&&`  
- OR: `||`
- NOT: `!` prefix
- Ability scores: `[str:13]`, `[dex:13]`, `[con:13]`, `[int:13]`, `[wis:13]`, `[cha:13]`
- Level: `[level:9]`
- Type check: `[type:spell]`
- Parenthesized groups: `([str:13]||[dex:13])`

```xml
<requirements>ID_RACE_ELF,[dex:13]</requirements>
<requirements>([str:13]||[dex:13]),(ID_CLASS_FIGHTER||ID_CLASS_RANGER)</requirements>
<requirements>!ID_SOME_OPTION</requirements>
```

### `<supports>`
Comma-separated tags used for filtering in `<select>` rules. An element can match multiple support categories.
```xml
<supports>Martial Archetype</supports>
<supports>Sorcerer, Wizard, Artificer</supports>
<supports>Skill,Fighter</supports>
```

### `<description>`
HTML content for the builder's right panel. Uses basic HTML with Aurora-specific CSS classes.
See [Description HTML Reference](reference/description-html.md) for formatting details.

### `<sheet>`
Plain text description for the character sheet. Attributes:
- `display` — `"true"` (default) or `"false"` to hide from sheet
- `alt` — Alternative name to display on the sheet
- `action` — Action type: `"Action"`, `"Bonus Action"`, `"Reaction"`, `"Special"`
- `usage` — Usage frequency: `"1/Short Rest"`, `"2/Long Rest"`, `"1/Turn"`, etc.

Multiple `<description>` children can have `level` attributes for level-dependent text.

```xml
<sheet action="Bonus Action" usage="1/Short Rest">
    <description>You regain 1d10+{{level:fighter}} hp.</description>
    <description level="17" usage="2/Short Rest">You regain 1d10+{{level:fighter}} hp.</description>
</sheet>
```

**Inline values** use `{{key}}` syntax referencing stat names or custom stat values.

### `<setters>`
Key-value pairs specific to the element type. Format: `<set name="{key}">{value}</set>`.
Some setters have additional attributes like `type`, `currency`, `lb`.
See [Setters Reference](reference/setters.md) for all setter names by element type.

## The `<append>` Node

Used to extend existing elements without overriding them. Placed at the same level as `<element>`.
```xml
<append id="ID_OF_EXISTING_ELEMENT">
    <supports>New Support Tag</supports>
    <rules>
        <grant type="Proficiency" id="ID_SOME_PROFICIENCY" />
    </rules>
</append>
```

## Feature Replacement Pattern

Many official features include a `requirements` check for a "Feature Replacement" grants element. This allows homebrew/variant features to replace official ones by granting the replacement ID.

```xml
<!-- Original feature checks for replacement -->
<element name="Second Wind" type="Class Feature" ... id="ID_FEATURE_SECOND_WIND">
    <requirements>!ID_INTERNAL_FEATURE_REPLACEMENT_FIGHTER_SECOND_WIND</requirements>
    ...
</element>

<!-- The replacement grant element (usually at bottom of file) -->
<element name="Second Wind Feature Replacement" type="Grants" source="Internal" 
         id="ID_INTERNAL_FEATURE_REPLACEMENT_FIGHTER_SECOND_WIND" />
```

To replace a feature, create your new feature and grant the replacement ID:
```xml
<rules>
    <grant type="Grants" id="ID_INTERNAL_FEATURE_REPLACEMENT_FIGHTER_SECOND_WIND" />
</rules>
```
