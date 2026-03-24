# Description HTML Reference

HTML classes, tags, and formatting patterns used in `<description>` nodes.

## Standard HTML Tags

### Paragraphs
```html
<p>Normal paragraph text.</p>
<p class="indent">Indented paragraph (used for body text under headings).</p>
<p class="flavor">Italic flavor text (used at the start of descriptions).</p>
```

### Headings
```html
<h3>MAJOR SECTION HEADING</h3>         <!-- Rare, used for "CLASS FEATURES" -->
<h4>SECTION HEADING</h4>               <!-- Standard section heading -->
<h5>SUBSECTION HEADING</h5>            <!-- Subsection heading -->
<h5 class="caption">TABLE CAPTION</h5> <!-- Used above tables -->
```

### Text Formatting
```html
<strong>Bold text</strong>
<em>Italic text</em>
<strong><em>Bold italic</em></strong>   <!-- Used for trait names in feature lists -->
<i>Italicized text</i>                  <!-- Used for equipment choice labels like (a)/(b) -->
<b><i>At Higher Levels.</i></b>         <!-- Spell upcast text label -->
```

### Lists
```html
<!-- Standard bullet list -->
<ul>
    <li>Item one</li>
    <li>Item two</li>
</ul>

<!-- Unstyled list (no bullets, used for proficiency/equipment lists) -->
<ul class="unstyled">
    <li><strong>Armor:</strong> All armor, shields</li>
    <li><strong>Weapons:</strong> Simple weapons, martial weapons</li>
</ul>

<!-- Unstyled list with margin-bottom -->
<ul class="unstyled mb">
    <li>...</li>
</ul>
```

### Tables
```html
<!-- Standard table -->
<table>
    <thead>
        <tr><td>Column 1</td><td>Column 2</td></tr>
    </thead>
    <tr><td>Data 1</td><td>Data 2</td></tr>
</table>

<!-- Table with tbody -->
<table>
    <thead>
        <tr><td class="col-20">d8</td><td>Creature</td></tr>
    </thead>
    <tbody>
        <tr><td>1</td><td>Weasel</td></tr>
    </tbody>
</table>

<!-- Class feature table -->
<table class="class-features">
    <thead>
        <tr><td class="col-5">Level</td><td class="left">Features</td></tr>
    </thead>
    <tr><td> 1st</td><td class="left">Feature 1, Feature 2</td></tr>
</table>
```

### Table Column Classes
| Class | Width |
|-------|-------|
| `col-5` | 5% |
| `col-10` | 10% |
| `col-20` | 20% |
| `left` | Left-aligned text |

### Inline Element References
Used to embed another element's description into the current one:
```html
<div element="ID_{...}_CLASS_FEATURE_{FEATURE}" />
```
This renders the referenced element's full description block inline.

### Centering
```html
<center>
    <p><strong>Spell save DC</strong> = 8 + your proficiency bonus + your Intelligence modifier</p>
</center>
```

## Common Formatting Patterns

### Racial Trait Description
```html
<p class="indent"><strong><em>Ability Score Increase.</em></strong> Your Constitution score increases by 2.</p>
<p class="indent"><strong><em>Age.</em></strong> Dwarves mature at the same rate as humans...</p>
<p class="indent"><strong><em>Size.</em></strong> Dwarves stand between 4 and 5 feet tall. Your size is Medium.</p>
```

### Feat Benefit List
```html
<p>You gain the following benefits:</p>
<ul>
    <li>Increase your Strength or Dexterity score by 1, to a maximum of 20.</li>
    <li>When you are prone, standing up uses only 5 feet of your movement.</li>
</ul>
```

### Spell Upcast Text
```html
<p class="indent"><b><i>At Higher Levels.</i></b> When you cast this spell using a spell slot of 3rd level or higher, the damage increases by 1d8 for each slot level above 2nd.</p>
```

### Prerequisite Line (for feats)
```html
<p><i>Prerequisite: Dexterity 13 or higher</i></p>
```

### Name Lists (for races)
```html
<ul class="unstyled">
    <li><strong>Male Names:</strong> Adrik, Alberich, Baern, Barendd</li>
    <li><strong>Female Names:</strong> Amber, Artin, Audhild, Bardryn</li>
    <li><strong>Clan Names:</strong> Balderk, Battlehammer, Brawnanvil</li>
</ul>
```

### Background Proficiency Summary
```html
<ul class="unstyled">
    <li><strong>Skill Proficiencies:</strong> Insight, Religion</li>
    <li><strong>Languages:</strong> Two of your choice</li>
    <li><strong>Equipment:</strong> A holy symbol, a prayer book, vestments, a set of common clothes, and a belt pouch containing 15 gp</li>
</ul>
```

### Class Feature Table with Spellcasting
```html
<table class="class-features">
    <thead>
        <tr>
            <td class="col-10">Fighter Level</td>
            <td class="col-10">Cantrips Known</td>
            <td class="col-10">Spells Known</td>
            <td>1st</td><td>2nd</td><td>3rd</td><td>4th</td>
        </tr>
    </thead>
    <tr><td> 3rd</td><td>2</td><td> 3</td><td>2</td><td>—</td><td>—</td><td>—</td></tr>
</table>
```

### Magic Item Charge/Property Table
```html
<table>
    <thead>
        <tr><td>Liquid</td><td>Max Amount</td></tr>
    </thead>
    <tr><td>Acid</td><td>8 ounces</td></tr>
    <tr><td>Beer</td><td>4 gallons</td></tr>
</table>
```

## Special Characters
| Character | HTML Entity |
|-----------|-------------|
| `&` | `&amp;` |
| `<` | `&lt;` |
| `>` | `&gt;` |
| `—` (em dash) | `—` (literal UTF-8) |
| `½` | `½` (literal UTF-8) |

## Notes
- Always use `&amp;` for the ampersand character in XML content
- The `<div element="..." />` pattern is self-closing
- Table cells use `<td>` (not `<th>`) even in header rows (inside `<thead>`)
- Empty descriptions are `<p></p>` or simply omitted
- The `mb` class on `<ul>` adds a margin-bottom for spacing between lists
