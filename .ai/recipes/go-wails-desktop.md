# Recipe: Go + Wails Desktop App

## When to Use
Use this recipe when you prefer **Go** over Rust for backend systems concurrency, networking, and simplicity, paired with a lightweight OS-native webview frontend (Svelte, React, or Solid).

## 1. Official Scaffold Commands
```powershell
# Ensure Wails CLI is installed
go install github.com/wailsapp/wails/v2/cmd/wails@latest

# Initialize Wails project in current directory (React + TS or Svelte + TS)
wails init -n app -t react-ts
```

## 2. Verification Commands
- **Check Environment**: `wails doctor`
- **Run Dev Mode (Hot Reload)**: `wails dev`
- **Production Native Binary Build**: `wails build`
