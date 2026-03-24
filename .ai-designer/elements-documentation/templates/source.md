# Source Element Template

A Source element defines metadata for a content collection (published book, supplement, or homebrew).

## Template

```xml
<element name="{Source Name}" type="Source" source="Core" id="ID_{AUTHOR}_{SOURCE_ABBREV}_SOURCE_{NAME}">
    <description>
        <p><strong>{Tagline}</strong></p>
        <p>{Description of the source material.}</p>
    </description>
    <setters>
        <set name="abbreviation">{ABBREV}</set>
        <set name="url">{URL to product page}</set>
        <set name="image">{URL to cover image}</set>
        <set name="errata">{URL to errata PDF}</set>
        <set name="author" abbreviation="{AUTHOR_ABBREV}" url="{Author URL}">{Author Name}</set>
        <set name="official">true</set>         <!-- true for official WotC content -->
        <set name="core">true</set>             <!-- true for core rulebooks only -->
        <set name="release">{YYYYMMDD}</set>    <!-- release date -->
        <!-- For supplements, add: -->
        <set name="supplement">true</set>
    </setters>
</element>
```

## Setters Reference

| Setter | Required | Description |
|--------|----------|-------------|
| `abbreviation` | Yes | Short code used in the builder (e.g., `PHB`, `DMG`) |
| `url` | Yes | Link to the product page |
| `image` | No | URL to cover art image |
| `errata` | No | URL to errata document |
| `author` | Yes | Author name, with `abbreviation` and `url` attributes |
| `official` | No | `"true"` for official WotC content |
| `core` | No | `"true"` for core rulebooks (PHB, DMG, MM) |
| `supplement` | No | `"true"` for supplement books |
| `release` | No | Release date in `YYYYMMDD` format |

## Example (Official)

```xml
<element name="Player's Handbook" type="Source" source="Core" id="ID_WOTC_SOURCE_PLAYERS_HANDBOOK">
    <description>
        <p><strong>Everything a player needs to create heroic characters.</strong></p>
    </description>
    <setters>
        <set name="abbreviation">PHB</set>
        <set name="url">http://dnd.wizards.com/products/tabletop-games/rpg-products/rpg_playershandbook/</set>
        <set name="image">https://raw.githubusercontent.com/AuroraLegacy/elements/master/core/players-handbook/PHB.png</set>
        <set name="author" abbreviation="WOTC" url="http://dnd.wizards.com">Wizards of the Coast</set>
        <set name="official">true</set>
        <set name="core">true</set>
        <set name="release">20140819</set>
    </setters>
</element>
```

## Example (Homebrew)

```xml
<element name="Roleanding Customs" type="Source" source="Custom" id="ID_RDLND_SOURCE_ROLEANDING_CUSTOMS">
    <description>
        <p>Custom homebrew content for our campaign.</p>
    </description>
    <setters>
        <set name="abbreviation">RDLND</set>
        <set name="url">https://github.com/inbabbini/roleanding-customs</set>
        <set name="author" abbreviation="RDLND" url="https://github.com/inbabbini">Roleanding</set>
        <set name="release">20240101</set>
    </setters>
</element>
```

## Notes
- The `source` attribute on a Source element is typically `"Core"`, `"Supplement"`, or `"Custom"`
- All other elements reference this Source by matching their `source` attribute to the Source's `name`
- The Source element is always in its own `source.xml` file
