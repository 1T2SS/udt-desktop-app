# LIBRARY_RADAR.md — High-Performance Desktop App Tech Stack Guide

> **Preset**: `desktop-app`
> **CRITICAL POLICY — NO ELECTRON**: Never recommend, scaffold, or install **Electron** (`electron`, `electron-builder`, `electron-forge`) or **NW.js**. Electron bundles an entire Chromium browser and Node.js runtime into every app, causing slow startup, huge binaries (150MB+), and 300MB–1GB+ RAM usage. Always use the fast, lightweight native/hybrid stacks below.

---

## 1. Architecture Decision Tree

| Project Goal | Recommended Primary Stack | Startup / Idle RAM | Matching Recipe |
| :--- | :--- | :--- | :--- |
| **Rich Modern Web UI (Tailwind/React/Svelte/Solid) + Fast Native Rust Backend** | **Tauri v2** (Rust core + OS Native WebView2/WebKit) | Instant / ~25–50MB (~5MB installer) | [`.ai/recipes/tauri-v2-lightweight-hybrid.md`](./recipes/tauri-v2-lightweight-hybrid.md) |
| **Zero-Webview Pure Native GPU-Accelerated GUI (Maximum Speed & Tiny RAM)** | **Rust + Slint**, **Iced**, **Dioxus (Native)**, or **egui** | <50ms / ~10–25MB | [`.ai/recipes/rust-native-gui-slint-iced.md`](./recipes/rust-native-gui-slint-iced.md) |
| **Enterprise / Data-Rich Windows or Cross-Platform Desktop Program in C#** | **.NET 9 + Avalonia UI** (cross-platform) or **WinUI 3** (Windows native) | Instant / ~30–60MB | [`.ai/recipes/dotnet-avalonia-crossplatform.md`](./recipes/dotnet-avalonia-crossplatform.md) |
| **Fast Go Backend + Lightweight Native Webview UI** | **Wails v2/v3** (Go + Svelte/React/Solid) | Instant / ~25–50MB | [`.ai/recipes/go-wails-desktop.md`](./recipes/go-wails-desktop.md) |

---

## 2. Approved Library Radar (By Stack)

### A. Tauri v2 Ecosystem (Rust + Web UI)
- **Core**: `@tauri-apps/api` v2, `@tauri-apps/cli` v2, `tauri` v2 crate.
- **Official Plugins**: `tauri-plugin-shell`, `tauri-plugin-fs`, `tauri-plugin-dialog`, `tauri-plugin-sql` (SQLite), `tauri-plugin-store`, `tauri-plugin-updater`, `tauri-plugin-global-shortcut`.
- **Type-Safe Rust↔TS IPC**: **`tauri-specta`** + **`specta`** (auto-generates TypeScript types directly from `#![tauri::command]` Rust functions!).
- **Frontend UI**: Vite + **SolidJS**, **Svelte 5**, or **React 19** + **Tailwind CSS v4**.

### B. Pure Rust Native GUI Ecosystem
- **Slint** (`slint` crate): Declarative `.slint` UI markup compiled to native code with GPU rendering — awesome for crisp desktop tools and utilities.
- **Iced** (`iced` crate): Elm-inspired reactive native GPU GUI in pure Rust.
- **egui / eframe**: Immediate-mode GPU GUI — unbeatable for real-time debuggers, overlays, node graphs, and data visualizers.
- **Async & System Crates**: `tokio`, `serde`, `serde_json`, `rusqlite` / `sqlx`, `tracing`, `anyhow`, `thiserror`, `directories` (OS appdata paths), `tray-icon`, `global-hotkey`.

### C. .NET 9 / C# Desktop Ecosystem
- **Framework**: **Avalonia UI v11+** (cross-platform XAML/C#, NativeAOT compatible) or **WinUI 3 / WPF (.NET 9)**.
- **MVVM**: **`CommunityToolkit.Mvvm`** (source-generated `[ObservableProperty]` and `[RelayCommand]` — zero reflection overhead).
- **UI Themes**: `Semi.Avalonia` or `FluentAvalonia`.
- **Local DB**: `Microsoft.Data.Sqlite` + `Dapper` or `EF Core`.

---

## 3. Banned / Deprecated by Default (DO NOT USE)

| Banned Tool / Library | Why It Is Banned | Use This Instead |
| :--- | :--- | :--- |
| **Electron** (`electron`, `electron-vite`, `electron-builder`) | Massive RAM usage (300MB+), 150MB+ binaries, slow cold start | **Tauri v2**, **Wails**, **Slint**, **Iced**, or **Avalonia UI** |
| **NW.js / CefSharp** *(unless embedding a full browser is the product itself)* | Bundles full Chromium engine unnecessarily | **Tauri v2** (uses OS WebView2/WebKit) or pure native GUI |
| **Tauri v1 `tauri.conf.json` `allowlist` syntax** | Deprecated/removed in Tauri v2 | Use **Tauri v2 `src-tauri/capabilities/default.json`** permissions |
| **Tkinter (Python)** | Outdated look, poor threading/DPI support | If Python is required, use **PySide6 (Qt6)** or wrap a Python sidecar in **Tauri v2** |
| **Heavy file-polling loops on UI thread** | Freezes desktop window responsiveness | Use OS-native file watchers (`notify` crate in Rust / `FileSystemWatcher` in .NET) on background threads |
