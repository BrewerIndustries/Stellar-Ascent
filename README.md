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
- **Pre-contact rebirth framing** — first rebirth should be explained without referencing aliens or The Cube (player hasn't seen them yet); needs an in-world reason (unexplained déjà vu, a dream, a compulsion) that only retroactively makes sense after first contact
- First contact event triggering the rebirth mechanic narratively
- Endgame revelation: many species, structured galaxy
- Final career arc: decode the Cube, find a younger species to pass it to
- **The Cube Codex entry** — intentionally vague. Grows more detailed with each rebirth. By loop 5 it contradicts itself

### Mechanics
- **Age-gated UI reveals** — progressively reveal sections of the UI as the player ages (automation at age 20, rebirth tab at 25, etc.). Keeps the interface from being overwhelming on day 1.
- **Second prestige path (Alignment)** — after a threshold of rebirths, choose to *align with the aliens* (gains power multipliers) or *resist* (harder path, unlocks hidden careers and lore). Each path has its own persistent currency and skill tree.
- **Cosmic Insight upgrade tree** — spend Insight on permanent buffs between runs.
- **Lifespan extension via Cosmic Insight** — post-rebirth upgrades that further extend effective death age beyond Cryostasis.

### Polish
- **Settings menu** — dedicated Settings tab or modal with: hard reset, save export/import, speed defaults, and any future toggles. Currently these live scattered across the sidebar.
- **First-time tutorial** — overlay-based walkthrough that fires on a fresh save (no prior play). Covers: what SC is, how to pick a career, what skills do, and what the rebirth loop is for. Should be re-triggerable at any time from the Settings menu.
- Audio (Web Audio API, ambient + click feedback)
- Mobile-friendly layout
- Visual polish: animations on level-up, rebirth cinematic, particle effects

### Platform
- GitHub Pages live deploy
- itch.io mirror release once beta-stable

## Changelog

### v0.1.6 — *Depth Update*
- **Codex tab** — Mechanics reference, Signal Log (5 anomaly events), 7 Lore Fragments, Career & Skill flavour entries for all 25 careers and 17 skills
- **Build tab** — 3 Installations (Research Station 500M, Orbital Platform 5B, Dyson Array Segment 50B SC) that persist through every rebirth and generate passive SC/day
- **Time Dilation** — Cryostasis Pod (35,000 SC/day) multiplies effective lifespan ×1.5; Cryonics skill (Fundamentals) amplifies the multiplier by +2%/lv. Life bar reflects actual effective death age.
- **Four backlog fixes** — Frugality skill (all-cost reducer), maxLevel spread bug, base-pay display in Careers tab, achievement system (21 achievements)

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
