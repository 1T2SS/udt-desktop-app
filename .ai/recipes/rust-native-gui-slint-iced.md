# Recipe: Pure Rust Native GPU-Accelerated GUI (Slint / Iced / egui)

## When to Use
Use this recipe when you want **100% pure native speed**, zero WebView dependency, <50ms instant startup, and ~10–25MB RAM usage.
- Choose **Slint** for polished, declarative desktop UIs with `.slint` markup.
- Choose **Iced** for clean Elm-architecture reactive native apps.
- Choose **egui (`eframe`)** for high-frequency tools, overlays, monitors, and node editors.

## 1. Official Scaffold Commands

### Option A: Iced (Reactive Native GPU GUI)
```powershell
cargo init --bin
cargo add iced --features tokio,advanced
cargo add tokio --features full
cargo add serde --features derive
cargo add serde_json anyhow tracing tracing-subscriber
```

### Option B: Slint (Declarative Native GUI)
```powershell
cargo init --bin
cargo add slint
cargo add --build slint-build
```

### Option C: egui / eframe (Immediate-Mode Native GUI)
```powershell
cargo init --bin
cargo add eframe serde --features serde/derive
```

## 2. Windows Subsystem Tip (Hide Console Window in Release Builds)
At the top of `src/main.rs`, include:
```rust
#![cfg_attr(not(debug_assertions), windows_subsystem = "windows")]
```
This keeps the console visible for logs during `cargo run` (debug) while launching as a clean native GUI window without a command prompt box in `cargo build --release`.

## 3. Verification Commands
- **Check & Lint**: `cargo check && cargo clippy -- -D warnings`
- **Test**: `cargo test`
- **Run Native GUI**: `cargo run`
