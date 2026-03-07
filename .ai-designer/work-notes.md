# Zareth Homebrew Project - Work Notes

## Project Scope
**Focus**: Create Aurora-compatible XML resources (race, archetype, feats, spells, items) that allow building Zareth as a playable character. NOT building Zareth himself, but the tools to build him.

### Core Principles
1. **Duplicity Forms**: Both celestial and infernal manifestations have Zareth's base stats with half HP, but different available abilities
   - Celestial: Advantage on Persuasion, Charm/Fear resistance, ally damage reduction reaction, prioritizes ally defense
   - Infernal: Advantage on Intimidation/Shove/Grapple, no ally-support abilities, +1d4 fire damage on melee
2. **Arkotropia**: Now a separate Feat (not archetype feature) - Uses custom Forma Bestial stat block
3. **Fire Absorption**: Simple fire-extinguishing feature for now (may evolve to spell slot recovery)
4. **Spellcasting**: Pyromancy uses **Wisdom** as casting ability (locked for automation)

### ✅ COMPLETED
1. **Work notes file created** - Foundation for tracking progress and knowledge base
2. **Crossbreed Celestial/Fiend Race** - Base template with Large size, dual heritage resistances, Duplicity trait, Longevity trait
3. **Hellish Knight Fighter Archetype** - Base template with Pyromancy, Midas Touch, Infernal Bond, Infernal Presence, Infernal Sentinel
4. **9 Custom Spells** - Created for Pyromancy:
   - Red-Flame Blade (Cantrip) - Green-Flame Blade reskin, fire theme
   - Explosive Jumps (1st) - Tripled jump distance via propulsion
   - Explosive Step (2nd) - Detonation teleport
   - Fire Syphon (3rd) - Reaction absorption of fire damage
   - Fiery Weapon (3rd) - 2d8 fire damage weapon imbue
   - Scorching Earth (3rd) - 20-ft cube geyser with difficult terrain
   - Exploding Flames (1st) - Reaction enhancement of allies' fire attacks/spells
   - Flame Strike (4th) - Vertical column fire+radiant damage
   - Fire Form (4th) - Fire aura dealing 2d8 damage
5. **5 Feats** - Created/refined by user:
   - **Rune Mastery** - 3 runes, Rune Carver options, 1/day inscribe
   - **Thrower** - Grapple/throw up to 2x STR, collision damage (1d6 per 10 ft), DEX save or prone for hostile targets
   - **Fire Avatar** - Fire immunity, +Prof to fire damage/spell DC, bonus action fire cantrip ({{proficiency}}/day)
   - **Mateador** - Prepare one round per short/long rest benefiting up to {{proficiency}} creatures
   - **Arkotropia** - Bear Force (1/turn Bestial Form stats, {{proficiency}}/long rest) + Animality (10-min transform, 1/short rest)

### 🔄 IN REVIEW/REFINED
1. **Hellish Knight Fighter Archetype** - Refined with detailed mechanics:
   - **3rd Level - Pyromantic Spellcasting**: Wisdom-based casting (DC/attack auto-calculated). Fire Absorption (action, 15-ft sphere). 4(1st), 2(2nd), 2(3rd), 1(4th) spell slots
   - **3rd Level - Midas Touch**: Prof. Bonus continuous objects, {{proficiency}} sq meters max material. Infernal Forge (short rest ritual), Transfiguration (6 options: Iron Sphere, Solidification, Extend, Colossal +1d4, Metal Curtain, Modify Object)
   - **7th Level - Infernal Bond**: Fire resistance, +Wisdom modifier to fire spell damage, Hellish Presence aura ({{proficiency}}/long rest)
   - **10th Level - Infernal Presence**: Blazing Aura (auto-activates in combat, 10-ft radius), Infernal Resilience (short rest HP recovery + {{proficiency*2}} temp HP per turn)
   - **15th Level - Infernal Sentinel**: Opportunity attacks reduce speed to 0, provoke even with Disengage, protective reaction vs ally attacks, fire-damaged creatures have disadvantage on next pyromantic save

2. **5 Feats** - Created/refined:
   - **Rune Mastery** - 3 runes, Rune Carver options, 1/day inscribe
   - **Thrower** - Grapple/throw up to 2x STR, collision damage (1d6 per 10 ft), DEX save or prone
   - **Fire Avatar** - Fire immunity, +Prof to fire damage/spell DC, bonus action fire cantrip ({{proficiency}}/day)
   - **Mateador** - Prepare one round per short/long rest for up to {{proficiency}} creatures (Restoration/HD/advantage/Bless)
   - **Arkotropia** (NEW) - Bear Force ({{proficiency}}/long rest) + Animality (10-min transform, 1/short rest, CON ST DC 20 or exhaustion)

### 📝 REMAINING TASKS
1. **Custom Spells** (8+ fire-based spells):
   - Control Flames, Fire Bolt, Red-Flame Blade, Burning Hands, Explosive Jumps
   - Aganazzar's Scorcher, Scorching Ray, Explosive Step
   - Scorching Earth, Fireball, Wall of Fire, Fire Form
   - Flame Strike
   - Custom spells: Fire Syphon, Fiery Weapon (if not standard versions)

2. **Race Refinements**:
   - Verify Duplicity mechanics work correctly (shared base stats, different abilities per form)
   - Confirm ability score distribution for Crossbreed Celestial/Fiend

3. **Magic Items** (Optional but flavor-rich):
   - Warhammer Menmonita +2 (thunder, earthquake ability)
   - Shield Menmonita +2 (deploy, vibranium, shockwave)
   - Plate Armor Menmonita +2 (electric resistance)
   - Festo's Armor (legendary, sentient, conscious)
   - Cannon Menmonita +1 (special ammunition)

4. **Bestial Form Integration**:
   - Verify stat block is properly accessible/integrated with Arkotropia feature

## Character Overview: Zareth

### Lineage & Background
- **Race**: Crossbreed Celestial/Fiend (Unique origin)
- **Age**: 1000+ years old
- **Father**: Azaziel - Infernal General (SemiDgod), strategic, pragmatic, honorable, revolutionary thinker
- **Mother**: Kaeleem - Celestial Arcane Angel (pure heart), elite archivist, healer, historian, keeper of celestial knowledge
- **Meeting**: Enemies-to-lovers during celestial-infernal war, met multiple times in combat, developed respect and passion
- **Nature**: Inherits duality of both celestial and infernal nature in conflict

### Physical Description
- **Size**: Large (3 meters/10 feet tall)
- **Build**: Muscular, wide-shouldered, powerful legs
- **Skin**: Dark gray with red/blue patterns (birthmarks that glow in certain situations), small black marks on back
- **Left Arm**: Covered in hard scales, ends in powerful claws capable of supporting full bodyweight
- **Right Arm**: Luminous white patches that emit bright light voluntarily
- **Face**: Dual nature reflected - two different eyes, two different horns, marked jaw with thick braided beard
- **Hair**: Black and gray, varies with emotional state/manifestation
- **Personality**: Dichotomous/conflicted - infernal and celestial sides in constant tension. Templado, good-humored (ironic/cynical/dark humor), sometimes chaotic/hyperactive or quiet/contemplative. Deep, powerful voice makes him excellent speaker/negotiator. Can seem lunatic one moment, composed the next.
- **Equipment**: Full plate armor (tempered steel plates + chainmail), shield (gift from mother), double-bladed axe (gift from father)

### Core Mechanics & Abilities

#### Duplicity (Racial)
- Can manifest physical separation into two entities representing infernal and celestial aspects
- Each manifestation gains abilities tied to that nature
- Cannot stray too far from each other (tether-bounded)
- Can reintegrate into main form or critical situations force reabsorption

#### Pyromancy (Archetype-related)
- **Fire Control**: Expand, extinguish, modify flame shape/color; create small fires with effort
- **Fire Attacks**: Flame jets/cones, explosive fireballs, geysers from surfaces
- **Fire Explosions**: Controlled detonations for jumping, self-propulsion, enemy repulsion
- **Fire Form**: Full-body flame covering without damage; emits light/heat; damages melee attackers
- **Fire Immunity**: Infernal fire essence makes external flames ineffective
- **Fire Absorption**: Can absorb external flames to fuel abilities (possibly as spell slot recovery mechanic)

#### Midas Touch (Weapon Bond Evolution)
- **Origin**: Infernal military technique for marshal adaptation
- **Function**: Manipulate inert materials (especially metals) - reconfigure shape/density while maintaining original function
- **Mechanics**: 
  - Requires direct contact; effects revert when contact broken (few seconds based on scale)
  - Advanced practitioners can do high-precision work or affect multiple objects/large surfaces
- **Features**:
  - **Forja Infernal (Ritual)**: Complete object reconfiguration while preserving function
  - **Transfiguración (Instantaneous)**: Quick partial/temporary modifications

#### Arkotropia (Ancestral Bear Spirit)
- **Origin**: Ancient mountain bear ancestor blood flowing through veins
- **Mechanics**: Two forms of manifestation requiring careful use (physical/mental cost)
- **Features**:
  - **Animalidad (Full Transformation)**: Complete transformation into massive bear with separate creature sheet; retains personality but influenced by ancestral energy; full bear stats apply
  - **Fuerza Oso (Partial)**: Momentary channeling for ability checks/saving throws (recovery: proficiency bonus/long rest, usable 1/short rest currently in notes)

#### Rune Mastery
- Ancient art of temporary runic inscriptions with various effects
- Can inscribe temporary runes with different benefits
- Recovery and mechanics need definition

#### Mate Preparation
- Ancestral knowledge of infused mate preparation
- Effects can include healing, affliction removal, temporary boosts
- Acts as healing/restoration feature with beneficial effects
- Mechanics: Minor Restoration, Hit Dice recovery, advantage on checks

### Class & Fighting Style

#### Class: Fighter (Level 21)
- Features: Fighting Style, Second Wind, Action Surge, Extra Attack, Indomitable (w/ multiple uses)
- ASI: 8 Ability Score Improvements available

#### Archetype: Hellish Knight (Custom)
- **Nature**: Warrior-mage hybrid forged in infernal fires
- **Spellcasting**: 
  - Focused pyromancy (fire-only spell list)
  - Spell Slots: 4(1st), 2(2nd), 2(3rd), 1(4th)
  - Can recover spell slots by consuming fire (mechanics TBD)
- **Features to Define**:
  - Enhanced Weapon Bond (Midas)
  - Pyromantic Spellcasting
  - War Magic evolution into something unique (Arkotropia-based?)
  - Infernal Sentinel (replaces Eldritch Strike)

### Important Notes
- Zareth is extremely rare/unique - others find him curious or abhorrent
- Prefers full armor to conceal dual nature for safety/comfort
- Deep connection to both celestial archives and infernal military knowledge
- 1000+ years of experience provides extensive skill/knowledge base
- Character is playable in different "states": integrated, split forms, bear-transformed

### Translation Context Notes
- Original concepts in Spanish translated to D&D 5e terminology
- "Maestro de Runas" → Rune Mastery
- "Toque de Midas" → Midas Touch (weapon bond variant)
- "Arkotropia" → Bear ancestral bloodline transformation
- "Duplicidad" → Duplicity (supernatural separation ability)
- "Piromancia" → Pyromancy (fire-based magic)

---

## SESSION SUMMARY - February 27, 2026

### Work Completed This Session

**Archetype Finalization**
- Fixed corrupted XML between Midas Touch and Infernal Bond (orphaned text cleanup)
- Implemented Wisdom-locked spellcasting with automated DC/attack calculations (stat rules: {{wisdom:modifier}})
- Corrected spell level placements: Fire Form 3rd→4th, Red-Flame Blade to cantrips
- Added custom spells (Fire Syphon, Fiery Weapon) to 3rd-level lists

**Custom Spells Created (8 total)**
1. Red-Flame Blade (Cantrip) - Green-Flame Blade reskin, fire theme
2. Explosive Jumps (1st) - Tripled jump distance via propulsion
3. Explosive Step (2nd) - Detonation teleport (30 ft)
4. Fire Syphon (3rd) - Reaction absorption of incoming fire damage
5. Fiery Weapon (3rd) - 2d8 fire damage weapon imbue, scalable
6. Scorching Earth (3rd) - 20-ft cube geyser (3d12), difficult terrain
7. Flame Strike (4th) - Vertical column (4d6 fire + 4d6 radiant)
8. Fire Form (4th) - Fire aura (2d8 damage on melee hits)

**Race Fixes (Aurora Testing)**
- Created Ability Score Improvement trait with +2/+1 distribution (enforced)
- Fixed Longevity trait to include rules-level skill selection
- Constrained skill selection to 7-skill subset (Insight, History, Religion, Deception, Intimidation, Persuasion, Survival)
- All three Aurora issues resolved: ASI selectable, Duplicity description visible, proficiency lists populated

**Items Created**
- Didgeridoo musical instrument: Properly structured Item + Proficiency pair for Aurora selection

### Architecture Decisions Made
1. **Wisdom-locking**: Enables Aurora automation for complex calculations
2. **Arkotropia separation**: Keeps archetype thematically infernal; bear power as optional feat
3. **Skill constraint in trait**: Moved from race level to Longevity trait for clarity and proper scoping
4. **Red-Flame tracking Green-Flame**: Maintains mechanical compatibility while respecting thematic reskin

### Files Status - All Production Ready
| File | Type | Status |
|------|------|--------|
| race-crossbreed-celestial-fiend.xml | Race | ✅ Aurora-tested, working |
| fighter-hellish-knight-archetype.xml | Archetype | ✅ Complete, spell-locked |
| custom-spells.xml | Spells | ✅ 9 spells, all formatted |
| feat-*.xml (5 files) | Feats | ✅ All independent, selectable |
| custom-instruments.xml | Items | ✅ Didgeridoo ready |

### Next Session Priorities
1. Create items/custom-weapons.xml (Menmonita items, Cannon)
2. Create items/custom-armor.xml (Plate, optional sentient piece)
3. Integration testing: Build sample character in Aurora to validate all components together
4. Optional: Duplicity form ability refinement pending user feedback
