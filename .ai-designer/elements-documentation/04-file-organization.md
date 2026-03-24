# File Organization & Index Files

## Folder Structure

AuroraLegacy organizes content by source book, with each source getting its own folder and index file.

```
root/
├── core.index                          # Top-level index pointing to core books
├── supplements.index                   # Top-level index pointing to supplements
├── core/
│   ├── internal.xml                    # Core internal elements (shared baseline)
│   ├── players-handbook.index          # PHB index file
│   ├── players-handbook/
│   │   ├── source.xml                  # Source metadata element
│   │   ├── race-dwarf.xml             # One file per race (includes subraces + traits)
│   │   ├── race-elf.xml
│   │   ├── class-fighter.xml          # One file per class (includes features)
│   │   ├── class-wizard.xml
│   │   ├── fighter-champion.xml       # One file per archetype (includes features)
│   │   ├── fighter-eldritch-knight.xml
│   │   ├── background-acolyte.xml     # One file per background
│   │   ├── feats.xml                  # All feats in one file
│   │   ├── spells.xml                 # All spells in one file
│   │   ├── items-weapons.xml          # Items grouped by category
│   │   ├── items-armor.xml
│   │   ├── items-gear.xml
│   │   ├── items-tools.xml
│   │   ├── items-packs.xml
│   │   ├── items-instrument.xml
│   │   ├── items-mounts.xml
│   │   ├── languages.xml              # All languages in one file
│   │   ├── companions.xml             # All companions in one file
│   │   ├── eldritch-invocations.xml   # Invocations in one file
│   │   └── deities.xml
│   ├── dungeon-masters-guide.index
│   ├── dungeon-masters-guide/
│   │   ├── source.xml
│   │   ├── items-weapons.xml          # Magic weapons
│   │   ├── items-armor.xml            # Magic armor
│   │   ├── items-wondrous.xml         # Wondrous items
│   │   ├── items-potions.xml
│   │   ├── items-rings.xml
│   │   ├── items-rods.xml
│   │   ├── items-staffs.xml
│   │   └── items-wands.xml
│   └── monster-manual/
└── supplements/
    ├── xanathars-guide-to-everything.index
    ├── xanathars-guide-to-everything/
    │   ├── source.xml
    │   ├── ... (same patterns as above)
    └── ...
```

## File Naming Conventions

| Content Type | File Name Pattern | Examples |
|-------------|-------------------|----------|
| Source metadata | `source.xml` | `source.xml` |
| Race | `race-{name}.xml` | `race-dwarf.xml`, `race-tiefling.xml` |
| Class | `class-{name}.xml` | `class-fighter.xml`, `class-wizard.xml` |
| Archetype | `{class}-{archetype}.xml` | `fighter-champion.xml`, `cleric-life.xml` |
| Background | `background-{name}.xml` | `background-acolyte.xml` |
| Feats | `feats.xml` (grouped) | `feats.xml` |
| Spells | `spells.xml` (grouped) | `spells.xml` |
| Weapons | `items-weapons.xml` | |
| Armor | `items-armor.xml` | |
| Gear | `items-gear.xml` | |
| Magic items | `items-{category}.xml` | `items-wondrous.xml`, `items-potions.xml` |
| Languages | `languages.xml` | |
| Companions | `companions.xml` | |
| Eldritch Invocations | `eldritch-invocations.xml` | |

### What goes in one file vs. separate files
- **One element per file**: Races (with subraces and traits), Classes (with features), Archetypes (with features), Backgrounds
- **Multiple elements per file**: Feats, Spells, Languages, Items/weapons/armor, Companions

## Index Files

Index files (`.index`) list the XML content files for a source and enable version tracking.

### Top-Level Index
```xml
<?xml version="1.0" encoding="utf-8"?>
<index>
    <info>
        <name>Core</name>
        <description>The content from the core rulebooks.</description>
        <author url="http://dnd.wizards.com">Wizards of the Coast</author>
        <update version="0.2.6">
            <file name="core.index" url="https://raw.githubusercontent.com/{user}/{repo}/main/core.index" />
        </update>
    </info>
    <files>
        <file name="internal.xml" url="https://raw.githubusercontent.com/{user}/{repo}/main/core/internal.xml" />
        <file name="players-handbook.index" url="https://raw.githubusercontent.com/{user}/{repo}/main/core/players-handbook.index" />
    </files>
</index>
```

### Source-Level Index
```xml
<?xml version="1.0" encoding="utf-8"?>
<index>
    <info>
        <name>Player's Handbook</name>
        <description>The Player's Handbook is the essential reference for every D&amp;D roleplayer.</description>
        <author url="http://dnd.wizards.com">Wizards of the Coast</author>
        <update version="0.2.2">
            <file name="players-handbook.index" url="https://raw.githubusercontent.com/{user}/{repo}/main/core/players-handbook.index" />
        </update>
    </info>
    <files>
        <file name="source.xml" url="https://...url.../source.xml" />

        <!-- races -->
        <file name="race-dwarf.xml" url="https://...url.../race-dwarf.xml" />
        <file name="race-elf.xml" url="https://...url.../race-elf.xml" />

        <!-- classes -->
        <file name="class-fighter.xml" url="https://...url.../class-fighter.xml" />

        <!-- archetypes -->
        <file name="fighter-champion.xml" url="https://...url.../fighter-champion.xml" />

        <!-- backgrounds -->
        <file name="background-acolyte.xml" url="https://...url.../background-acolyte.xml" />

        <!-- items -->
        <file name="items-weapons.xml" url="https://...url.../items-weapons.xml" />
        <file name="items-armor.xml" url="https://...url.../items-armor.xml" />

        <!-- other -->
        <file name="feats.xml" url="https://...url.../feats.xml" />
        <file name="spells.xml" url="https://...url.../spells.xml" />
        <file name="languages.xml" url="https://...url.../languages.xml" />
    </files>
</index>
```

## Info Section (in XML content files)

Every XML content file should have an `<info>` section inside the `<elements>` root tag:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<elements>
    <info>
        <name>Descriptive Name</name>
        <description>Optional description</description>
        <author url="http://author.url">Author Name</author>
        <update version="0.1.0">
            <file name="filename.xml" url="https://raw.githubusercontent.com/{user}/{repo}/main/path/filename.xml" />
        </update>
    </info>

    <!-- elements go here -->
</elements>
```

### Info Fields
| Field | Required | Description |
|-------|----------|-------------|
| `<name>` | Optional | Display name during loading |
| `<description>` | Optional | Description of file contents |
| `<author>` | Optional | Author name, with optional `url` attribute |
| `<update>` | Required | Must contain `version` attribute and a `<file>` child |

### Version Numbering
- Use semantic versioning: `MAJOR.MINOR.PATCH`
- Increment version when file content changes so Aurora knows to update
- Start at `0.1.0` or `1.0.0` for new content

### Marking Files Obsolete
When a file is no longer needed (e.g., merged into another):
```xml
<obsolete name="old-file.xml" url="https://...url.../old-file.xml" />
```
