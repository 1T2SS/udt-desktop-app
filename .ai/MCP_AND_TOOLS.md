# MCP_AND_TOOLS.md — Proactive Environment & MCP Setup (`desktop-app`)

> **AI Agent Instruction**: Before scaffolding a desktop app, verify that the required native compiler toolchain (Rust + MSVC Build Tools, .NET SDK, or Go) and helpful MCP/static-analysis tools are installed. **If anything is missing, tell the user what is needed and ask if you can install/configure it for them!** Record all findings in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md).

---

## 1. Recommended MCP Servers & Skills to Check

| MCP Server / Skill | Purpose in `desktop-app` | How to Check & Offer Setup |
| :--- | :--- | :--- |
| **`cargo-fallow` & `fallow` Skills** | Audits Rust workspaces (`cargo fallow`) and TypeScript UIs (`fallow`) for unused dependencies, dead code, large functions, and crate boundary violations. | If using Rust or Tauri, check `cargo fallow --version`. If missing, ask the user if you can install it or use standard `cargo clippy`. |
| **Chrome DevTools MCP** *(for Tauri / Wails hybrid apps)* | Inspects WebView UI rendering, CSS layout, and frontend performance metrics. | Check if `chrome-devtools` MCP is available when debugging complex Tauri/Wails webview layouts. |

---

## 2. Native Desktop Toolchain Doctor Checklist

Run the checks matching the user's chosen stack and record exact versions in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md):

```powershell
# A. For Tauri v2 or Pure Rust GUI (Slint / Iced / egui):
rustc --version
cargo --version
bun --version

# Check if MSVC C++ linker (link.exe) is available on Windows (required by Rust/Tauri):
where.exe cl link 2>$null

# B. For .NET 9 / Avalonia / WinUI 3:
dotnet --version
dotnet --list-sdks

# C. For Go / Wails:
go version
wails version 2>$null
```

### Auto-Setup Commands (Offer to Run with User Permission if Missing)
- **Install Rust (`rustup`) on Windows**: `winget install Rustlang.Rustup`
- **Install Visual Studio C++ Build Tools (if Rust complains about missing `link.exe`)**:
  `winget install Microsoft.VisualStudio.2022.BuildTools --override "--wait --passive --add Microsoft.VisualStudio.Workload.VCTools --includeRecommended"`
- **Install Fast Rust Linker / Cargo Tools**: `cargo install cargo-binstall`
- **Install .NET 9 SDK**: `winget install Microsoft.DotNet.SDK.9` and Avalonia templates: `dotnet new install Avalonia.Templates`
- **Install Go & Wails**: `winget install GoLang.Go && go install github.com/wailsapp/wails/v2/cmd/wails@latest`

---

## 3. Save Verified Setup Info for Future Creations
After checking or installing the toolchain:
1. Mark `Environment Check Status: VERIFIED` in [`.ai/ENVIRONMENT.md`](./ENVIRONMENT.md) with compiler versions and whether MSVC Build Tools / WebView2 are ready.
2. Add any helpful setup findings (e.g., fast-compile `.cargo/config.toml` flags or SDK paths) to Section 5 of [`.ai/MEMORY.md`](./MEMORY.md).
