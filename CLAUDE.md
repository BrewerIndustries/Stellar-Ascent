# Stellar Ascent

Browser-based incremental idle RPG — a space reimagining of *Progress Knight: Reborn*. You're a garage scientist who lives many lifetimes toward the stars, dying of old age (~70y) each run and rebirthing with persistent **Cosmic Insight**. Tone: grounded near-future hard sci-fi that drifts into cosmic strangeness. Aliens hand you a black cube; you touch it; you wake up in the garage. You've done this before.

## Tech

- **Single-file app**: everything lives in `index.html` (~2360 lines). No build step, no package.json, no dependencies to install.
- React 18 + Babel standalone, both loaded from CDN inside `index.html`. JSX is transpiled in-browser (`<script type="text/babel">`).
- Vanilla CSS in a `<style>` block at the top of the file (~line 10).
- Save/load via `localStorage`.

## Code layout inside `index.html`

Read top-to-bottom; it's organized in clear sections separated by `// ====` banners:

- **CSS** — `<style>` block near line 10.
- **Constants** — `TICK_MS = 200`, `DAYS_PER_YEAR`, `START_AGE_DAYS`, `DEATH_AGE_DAYS` (~line 563).
- **Balance/config data (top-level `const` arrays)** — this is where you change game content:
  - `CAREERS` (~572) — 25 careers, 5 paths (`garage`/`academy`/`corps`/`syndicate`/`ascended`). Fields: `basePay`, `baseXp`, `prevReq`, `levelReq`, `postRebirth`. `PATH_META` (~609) holds path labels/colors.
  - `SKILLS` (~618) — 17 skills; each has an `effectFn(lvl)` returning a multiplier and a `category`.
  - `SHOP` (~648) — 25 items, categories `Living`/`Equipment`/`Misc`; bonuses + daily SC cost.
  - `STORY_EVENTS` (~694), `ACHIEVEMENTS` (~726), `SIGNAL_EVENTS` (~760), `LORE_FRAGMENTS` (~781), `BUILDINGS` (~808, persist across rebirths).
  - `calcInsightGain(state)` (~833) — Cosmic Insight formula on death.
- **State factory** — `freshState(insight, hasReborn)` (~856) defines the entire save shape (`ageDays`, `sc`, `cosmicInsight`, `careers`, `skills`, `shop`, `buildings`, `codexSignals`, `codexLore`, `achievements`, etc.). `initialCareers()`/`initialSkills()`/`freshBuildings()` build the sub-objects.
- **`App()` component** (~884) — holds all game state via `useState`. Key logic:
  - **Load/migration**: on init reads `localStorage['stellar_ascent_save']`, then merges saved data onto a fresh state so new career/skill/building IDs don't crash old saves (~893). Preserve this merge pattern when adding IDs.
  - **`calcMults(s)`** (~936) — derives all XP/pay/cost multipliers from skills + shop bonuses. Central balance chokepoint.
  - **Game loop**: `setInterval(..., TICK_MS)` (~1065) advances days, awards XP/SC, handles auto-promote/auto-learn, level-ups, death→rebirth, and fires achievements/signals/lore/story events.
  - **Auto-save**: separate `setInterval` writes to localStorage every 30s (~1057).
  - Actions: `buyShop`, `buyBuilding`, `doRebirth`, `hardReset`, `exportSave`, `importSave`.
- **Components** (each a `function` after `App`): `StatusBar` (~1544, left sidebar: life bar, speed, finances, Insight), `CareersTab`, `SkillsTab`, `ShopTab`/`ShopRow`, `RebirthTab`, `StoryTab`, `StatsTab`, `AchievementsTab`, `BuildTab`/`BuildRow`, `CodexTab`, `PatchNotesTab`.
- **Mount** — `ReactDOM.createRoot(...).render(<App />)` at the very bottom (~2361).

## Where to change what

- **Game balance / content** → the top-level data arrays (`CAREERS`, `SKILLS`, `SHOP`, `BUILDINGS`, `ACHIEVEMENTS`, `calcInsightGain`) and multiplier math in `calcMults`. Pacing → `TICK_MS` and `baseXp`/`levelReq` values.
- **UI / layout** → the `<style>` block and the `*Tab` / `StatusBar` components.
- Adding a new career/skill/building ID: add to the array AND rely on the load-merge in `App` — don't hand-edit `freshState`'s sub-objects (the `initial*` helpers derive from the arrays).

## Run locally

Just open `index.html` in a browser (double-click / `file://`). Optionally serve statically: `python3 -m http.server` in the repo root, then browse to it. No build, no install.

## Deploy

GitHub Pages via `.github/workflows/pages.yml` (repo `BrewerIndustries/Stellar-Ascent`). One Pages site, two versions:

- `main` → `/` (prod) → https://stellar-ascent.dabrewer.dev/
- `dev` → `/dev/` → https://stellar-ascent.dabrewer.dev/dev/

**Gotcha**: the workflow lives on `dev` only and triggers on push to `dev` (or manual "Run workflow"). It checks out *both* branches itself. **Pushing to `main` does NOT auto-redeploy** — a push to `dev`, or a manual dispatch, is what rebuilds the whole site (including prod from `main`).

## Git workflow

- Do active work on `dev`. Push to `dev` freely.
- Promote to `main` ONLY via a PR the user approves. Never fast-forward, reset-push, or force-push `main`.
- After any meaningful change, update `README.md` (keep the Changelog and feature list current).
