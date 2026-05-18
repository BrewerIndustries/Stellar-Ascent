# Stellar Ascent

A browser-based incremental idle RPG. You are an amateur scientist in your garage who, across many lifetimes, builds humanity's path to the stars — until you encounter an alien species who hand you a small black cube. You touch it. You wake up back in the garage. You've done this before.

A space-themed reimagining of *Progress Knight: Reborn*.

## Concept

Cycle through lives as different roles, from scrap scavenger to starship captain to cube-bearer. Each life resets but trace knowledge persists as **Cosmic Insight**. The aliens are testing you. Eventually you realize the test isn't whether you pass — it's what you do when you do.

**Tone:** Starts grounded near-future hard sci-fi, gradually drifts into cosmic strangeness. Real physics gives way to wonder.

## Tech

- Single-file HTML, React + Babel via CDN
- No build step — open `index.html` and it runs
- Deployed via **GitHub Pages** (push to `main`, live in ~30 seconds)
- localStorage for save/load (file export/import deferred to v0.2)

## Core Features (v0.1)

- **25 careers across 5 tiers** — Garage → Institutions → Industry → Captain → Ascended
- **16 skills across 5 categories** — Fundamentals, Hands-On, Theoretical, Command, Cosmic
- **25 shop items** — Living Quarters, Equipment, Misc (lifestyle)
- **Rebirth loop** — die of old age (~70 years), gain Cosmic Insight, restart in the garage
- **Tier 5 gating** — Ascended careers unlock only after the first rebirth
- **The Cube** — appears in Misc shop after first rebirth
- **Auto-save** — localStorage, every 30 seconds
- **Reborn-fidelity tick feel** — game-days tick at Reborn's pace; ~30-45 minute first run

## Backlog

### Story & flavor
- Anomaly events in early game (mysterious signals, weird readings)
- **Pre-contact rebirth framing** — first rebirth should be explained without referencing aliens or The Cube (player hasn't seen them yet); needs an in-world reason (unexplained déjà vu, a dream, a compulsion) that only retroactively makes sense after first contact
- First contact event triggering the rebirth mechanic narratively
- Endgame revelation: many species, structured galaxy
- Final career arc: decode the Cube, find a younger species to pass it to
- Story event popups at career/skill milestones

### Mechanics
- **Lifespan extension / Time Dilation system** — FTL and relativistic travel slow your aging tick. Sources: Endurance (baseline), Tier 4 jobs (passive dilation), Cryostasis shop item, Cosmic Insight upgrades, Cube Attunement (endgame).
- **Auto-learn / Auto-promote toggles** — sidebar toggles that automatically assign skill training to the highest unlocked skill and promote to the next available career when the current one is ready; each toggle is independent. Add per-skill "skip" checkboxes (visible post-rebirth) so players can exclude skills from the auto-learn rotation.
- **Happiness baseline = 1.0× by default** — currently Cramped Apartment starts at 0.5× XP, making the base feel like a penalty. Change default happiness so no Living Quarters = 1.0× multiplier, and all Living Quarters upgrades add above that (e.g. Cramped Apartment = 1.1×, penthouse = 2.0×). Happiness should only ever be a bonus, never a debuff.
- **Logarithmic income scaling with career level** — PKR uses `1 + log₁₀(level + 1)` so income grows meaningfully as you level but doesn't explode. Audit current SA income formula and align to this.
- **Expense-reducing skill** — PKR has Bargaining (`1 − log₇(level+1) / 10`, min 0.1). SA has no expense reduction path. Add an equivalent skill (e.g. *Resourcefulness* or *Black Market Contacts*) that reduces SC/day costs for shop items, capped at 90% off.
- **Bankruptcy / housing downgrade** — if SC balance goes negative, auto-cancel all active shop items and drop to cheapest Living Quarters. Adds real stakes to overspending without hard game-overs.
- **Age-gated UI reveals** — progressively reveal sections of the UI as the player ages, mirroring PKR's approach (automation at age 20, rebirth at 25). Keeps the interface from being overwhelming on day 1 and makes early-game feel like discovery.
- **Passive income buildings / installations** — PKR has town buildings that generate income independently of jobs. SA equivalent: research labs, orbital platforms, manufacturing bays. These persist through rebirth, providing a long-term investment track separate from career income.
- **Second prestige path (Alignment)** — PKR has a two-tier rebirth: normal rebirth preserves maxLevel, Dark Rebirth resets it but unlocks a shadow skill tree. SA equivalent: after a threshold of rebirths, the player can choose to *align with the aliens* (surrendering autonomy, gains power multipliers) or *resist* (harder path, unlocks hidden careers and lore). Each alignment has its own persistent currency and skill tree.
- **Career/skill level memory across rebirths** — track the highest level ever reached per career and skill; on subsequent lives, XP gain for that career/skill is multiplied by `1 + (previousMaxLevel / 10)` (PKR formula: lv10 past = 2× XP, lv20 = 3×, etc.). `maxLevel` persists through rebirth; current level resets to 0 as normal. No hardcoded cap — scales linearly with past investment.
- **Large number formatting** — SI notation (k / M / B / T / q) for SC balances, income, and XP values once they get large. PKR uses this throughout; currently SA likely shows raw numbers.
- Cosmic Insight upgrade tree (spend Insight on permanent buffs)
- Achievements
- Statistics tab (total lives, total SC earned, longest career, etc.)

### Codex tab
In-game reference and lore discovery system. Unlocks entries as the player reaches milestones.
- **Mechanics definitions** — plain-language explanations of every stat, multiplier, and system (Happiness, Cosmic Insight, XP rate, SC/day, path bonuses, rebirth loop, etc.)
- **Career & skill entries** — flavour description for each career and skill; what it means in the world, not just what it does in the numbers
- **Lore fragments** — hidden entries that unlock at specific milestones (first rebirth, reaching The Ascended, buying The Cube, hitting certain Cosmic Insight thresholds). Fragments hint at the alien civilisation, the nature of the loop, what the cube actually is, and why the test is happening
- **Signal log** — a running log of "anomalous readings" and intercepted transmissions that appear in early game, building dread before first contact. Entries are short, cryptic, never explained directly
- **The Cube entry** — intentionally vague. Grows more detailed with each rebirth. By loop 5 it contradicts itself

### Polish
- Patch Notes tab (in-game)
- Audio (Web Audio API, ambient + click feedback)
- Save export/import to file (base64)
- Mobile-friendly layout
- Visual polish: animations on level-up, rebirth cinematic, particle effects

### Platform
- GitHub Pages live deploy
- itch.io mirror release once beta-stable

## Changelog

### v0.1.4 — *Pacing*
- Day tick slowed 4× (TICK_MS 50 → 200ms). A first life at 1× speed is now ~68 minutes instead of ~17

### v0.1.3 — *Equipment & Stability*
- Equipment items now stack — multiple can be active simultaneously, bonuses combine, each costs SC/day
- Fixed blank screen crash when loading saves from previous versions (new career/skill IDs merged with saved data on load)

### v0.1.2 — *Paths & Happiness*
- **4 career paths** — The Garage (always), The Academy (Electronics lv30), The Corps (Hobbyist lv25), The Syndicate (Inventor lv20), plus The Ascended (post-rebirth)
- **Happiness system** — Living Quarters set happiness (50–100); happiness/100 multiplies all XP gain. Cramped Apartment = 0.5× XP; upgrades accelerate progression
- **Better labels** — Career rows show "Needs [Career] lv X" when locked, explicit SC/day pay, XP/day rates; Skills show unlock requirements and numeric effect per level
- Skills unlock tied to new path careers (Theoretical → Lab Assistant; Command → Flight Officer)
- Path-specific skill bonuses: Garage uses Dexterity, Academy uses Theory, Corps uses Strategic Vision, Syndicate uses Charisma

### v0.1.1 — *UI Pass*
- Intro overlay on page load freezes game until player clicks Begin
- Left status sidebar (PKR-style): Life/lifespan bar, Speed controls, Finances (balance, net, income, expense), Cosmic Insight, active Career progress, active Skill progress
- Hard Reset moved into sidebar; header simplified to title only
- GitHub repo: `BrewerIndustries/Stellar-Ascent` — dev branch for active work, main branch for GitHub Pages deploys

### v0.1 — *Scaffold*
- Initial release. Literal reskin of Progress Knight: Reborn structure.
- 25 careers, 16 skills, 25 shop items
- Rebirth loop with Cosmic Insight currency
- Tier 5 careers and The Cube gated behind first rebirth
- localStorage auto-save
