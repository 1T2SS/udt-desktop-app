# Universal High-Performance Desktop App Template (`udt-desktop-app`)

> **AI-First Vibe Coding Preset** for ultra-fast, low-memory native and hybrid desktop applications on Windows, macOS, and Linux.
> **Zero Electron Bloat**: Electron is explicitly banned by default in favor of **Tauri v2**, **Rust Native GUIs (Slint / Iced / Dioxus)**, **.NET 9 Avalonia / WinUI 3**, and **Go Wails**.

---

## Quick Start (30 Seconds)

### Option A: From GitHub
1. Click **"Use this template" → "Create a new repository"** on GitHub.
2. Clone your new repo and open it in any AI coding agent (Antigravity, Claude Code, Cursor, Windsurf, Copilot, Cline).
3. Describe the desktop program or utility you want to build!

### Option B: From Local UDT Hub
```powershell
.\scripts\new-project.ps1 -Preset desktop-app -Target "E:\Projects\MyFastDesktopApp" -InitGit
```

---

## Why This Preset Exists
Most AI agents default to **Electron** when asked for a desktop app, leaving you with a 200MB+ installer and 400MB+ idle RAM usage. This preset overrides that habit immediately via [`.ai/LIBRARY_RADAR.md`](./.ai/LIBRARY_RADAR.md) and checks your local Rust/.NET/Go compilers via [`.ai/MCP_AND_TOOLS.md`](./.ai/MCP_AND_TOOLS.md) so you get a tiny, instant-startup native desktop binary.
