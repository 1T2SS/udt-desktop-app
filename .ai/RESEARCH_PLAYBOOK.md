# RESEARCH_PLAYBOOK.md — Desktop App Pre-Coding Research Protocol

> **Preset**: `desktop-app`
> **Rule**: Verify OS build prerequisites and v2/modern framework schemas before scaffolding or writing native bindings.

---

## 1. Critical Version & Schema Checks

1. **Tauri v2 vs Tauri v1 (Major Breaking Differences)**:
   - Tauri v2 uses `@tauri-apps/api/core` (`invoke` comes from `@tauri-apps/api/core`, **NOT** `@tauri-apps/api/tauri`).
   - Tauri v2 replaces `allowlist` in `tauri.conf.json` with fine-grained ACL files under `src-tauri/capabilities/default.json`.
   - Official Tauri v2 plugins use the `tauri-plugin-<name>` crate + `@tauri-apps/plugin-<name>` npm package.
   - Always check `cargo search tauri-plugin-` or live docs before guessing plugin names.

2. **Rust Native GUI Crate Versions (`slint`, `iced`, `egui`)**:
   - GUI crates in Rust evolve rapidly across minor versions (e.g., `iced` 0.12 vs 0.13+ replaces the `Application`/`Sandbox` trait with `iced::application(title, update, view)` builder functions!).
   - **Mandatory Check**: Run `cargo info <crate>` or check docs.rs / official examples for the exact version installed in `Cargo.toml` before writing UI code.

3. **Avalonia UI v11+ (.NET 9)**:
   - Use compiled bindings (`x:DataType="vm:MainWindowViewModel"`) by default for NativeAOT compatibility and zero reflection overhead.

## 2. Performance & Threading Architecture Research
- Never block the main UI/window thread with disk I/O, SQLite queries, or network calls.
- In Tauri/Rust: run heavy tasks on `tokio::spawn` or `tokio::task::spawn_blocking` and stream progress events via `tauri::ipc::Channel` or `AppHandle::emit`.
