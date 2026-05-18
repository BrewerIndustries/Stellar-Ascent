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
- First contact event triggering the rebirth mechanic narratively
- Endgame revelation: many species, structured galaxy
- Final career arc: decode the Cube, find a younger species to pass it to
- Story event popups at career/skill milestones

### Mechanics
- **Lifespan extension / Time Dilation system** — FTL and relativistic travel slow your aging tick. Sources: Endurance (baseline), Tier 4 jobs (passive dilation), Cryostasis shop item, Cosmic Insight upgrades, Cube Attunement (endgame).
- Cosmic Insight upgrade tree (spend Insight on permanent buffs)
- Achievements
- Statistics tab (total lives, total SC earned, longest career, etc.)

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
