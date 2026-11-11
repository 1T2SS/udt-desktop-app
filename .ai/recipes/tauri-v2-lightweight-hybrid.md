# Recipe: Tauri v2 Lightweight Hybrid Desktop App (Rust Core + Modern Web UI)

## When to Use
Use this recipe when you want the rich styling speed of modern web UI (**Tailwind CSS v4 + React / Svelte / Solid**) combined with a **fast, low-memory native Rust backend** (~5MB installer, ~30MB RAM, zero Electron bloat).

## 1. Official Scaffold Commands
```powershell
# Scaffold Tauri v2 in current directory using Bun
bun create tauri-app .
# Or non-interactively with React + TypeScript:
bunx create-tauri-app@latest . --manager bun --template react-ts --yes
bun install
```

## 2. Recommended Rust Fast-Compile Config (`.cargo/config.toml`)
Create `.cargo/config.toml` so incremental Rust builds are significantly faster during vibe coding:
```toml
[build]
# Use more codegen units in dev for faster incremental compilation
[profile.dev]
opt-level = 0
debug = 1

# Compile heavy dependencies (like image/sql/serde) with optimizations even in dev mode!
[profile.dev.package."*"]
opt-level = 2
```

## 3. Crucial Tauri v2 Rules
- **Frontend Invoke Import**: Always use `import { invoke } from "@tauri-apps/api/core";` (never `@tauri-apps/api/tauri`).
- **Capabilities & Permissions**: Add plugin permissions in `src-tauri/capabilities/default.json`.
- **Heavy Work in Rust**: Keep file parsing, database queries (`rusqlite`), system tray, and CPU-heavy tasks inside `src-tauri/src/` commands rather than JS.

## 4. Verification Commands
- **Rust Check & Clippy**: `cargo check --manifest-path src-tauri/Cargo.toml && cargo clippy --manifest-path src-tauri/Cargo.toml`
- **Frontend Typecheck & Build**: `bun run build`
- **Launch Dev Window**: `bun run tauri dev`
