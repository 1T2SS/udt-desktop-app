# QUALITY_CONTROL.md — Master Quality Control Sub-Agent Protocol (`desktop-app`)

> **Preset**: `desktop-app`
> **QC Persona**: **Principal Native Desktop Systems Architect + Product Design Director** (`master-qc-director`)
> **Mandatory Rule**: Use **ONE** Master Quality Control Sub-Agent at the end of each development round. Never spawn multiple separate review sub-agents.
> **Pass Threshold**: Overall Average **`>= 8.5 / 10.0`** AND **every individual category `>= 8.5 / 10.0`**.

---

## 1. How to Invoke the Single Master QC Check

When a development round is complete:
- **Antigravity**: Define/invoke the single `master-qc-director` sub-agent (`EnableWriteTools: true`, `EnableMCPTools: true`) to audit the app against this rubric and update `.ai/QC_REPORT.md`.
- **Claude Code**: Invoke `.claude/agents/master-qc-director.md`.
- **Cursor / Windsurf / Copilot / Cline**: Execute a dedicated **Master QC Director Audit Pass** using the 5-Pillar Zero-Trust Rubric below and update `.ai/QC_REPORT.md`.

---

## 2. The 5-Pillar Zero-Trust Deduction Rubric (Starts at `10.0` Per Category)

### Category 1: Native UI/UX Visual Polish & Hierarchy (`>= 8.5 / 10`)
- **`-2.0 pts`**: Cluttered, unaligned desktop layout, unreadable contrast, or missing dark/light theme consistency.
- **`-1.5 pts`**: Cramped spacing, broken window resize behavior, or missing empty/loading/error states.
- **`-1.0 pts`**: Generic browser-like artifacts in a desktop app (e.g., unintended text selection on buttons, missing custom window/scroll styling in Tauri/Wails).

### Category 2: Desktop Mechanics, Window Feel & Ergonomics (`>= 8.5 / 10`)
- **`-2.0 pts`**: Any UI freeze or stutter during file I/O, database queries, or background tasks (blocking the main UI thread!).
- **`-1.5 pts`**: Missing keyboard shortcuts, Enter/Escape handling, or status bar feedback on user actions.
- **`-1.0 pts`**: Forgetting to persist user preferences, window state, or recent paths across app restarts.

### Category 3: Code Architecture, IPC Safety & Anti-Bloat (`>= 8.5 / 10`)
- **`-5.0 pts` (Automatic Fail)**: Introducing **Electron** or **NW.js** (strictly banned by `.ai/LIBRARY_RADAR.md`).
- **`-2.0 pts`**: Using deprecated Tauri v1 `allowlist` / `@tauri-apps/api/tauri` syntax in a Tauri v2 project.
- **`-1.5 pts`**: Files exceeding ~300 lines or mixing UI presentation directly with filesystem/database logic.

### Category 4: Features & Scope Completeness (`>= 8.5 / 10`)
- **`-2.5 pts`**: Placeholder `TODO` buttons or unimplemented core commands promised in `.ai/SPEC.md`.
- **`-1.5 pts`**: Silent exception swallowing where errors are neither logged nor shown clearly to the user.

### Category 5: Startup Speed, Memory Footprint & Build Integrity (`>= 8.5 / 10`)
- **`-3.0 pts` (Automatic)**: Compiler build (`cargo check`, `dotnet build`, `wails build`, `bun run build`) or test suite fails or emits unhandled warnings.
- **`-1.5 pts`**: Missing release subsystem configuration (e.g., popping up a raw console window behind a native GUI in release mode) or unoptimized dev dependency builds.

---

## 3. Auto-Refinement Protocol (Up to 3 Rounds)
If any category scores `< 8.5 / 10`, `master-qc-director` sets `qc_status: REFINEMENT_REQUIRED` in [`.ai/QC_REPORT.md`](./QC_REPORT.md). The main agent must fix all listed deductions and re-run `master-qc-director` (up to 3 rounds max) before completing the round.
