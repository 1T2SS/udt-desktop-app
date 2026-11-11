# Recipe: C# .NET 9 + Avalonia UI Cross-Platform Desktop App

## When to Use
Use this recipe when building a fast, strongly typed C#/.NET 9 desktop program with rich data grids, multi-window support, and NativeAOT compilation across Windows, macOS, and Linux.

## 1. Official Scaffold Commands
```powershell
# Ensure Avalonia templates are installed
dotnet new install Avalonia.Templates

# Create an Avalonia MVVM solution in the current folder
dotnet new avalonia.mvvm -o . --force
dotnet add package CommunityToolkit.Mvvm
dotnet add package Semi.Avalonia
```

## 2. Recommended Architecture (`MVVM`)
```text
├── Assets/               # Icons, fonts, and static resources
├── Models/               # Pure domain entities and services
├── ViewModels/           # CommunityToolkit.Mvvm ([ObservableProperty], [RelayCommand])
├── Views/                # .axaml UI files with compiled bindings (x:DataType)
├── App.axaml             # Application theme & resource dictionary
└── Program.cs            # Entrypoint
```

## 3. Verification Commands
- **Build & Compile Check**: `dotnet build -c Debug`
- **Run Tests**: `dotnet test`
- **Launch App**: `dotnet run`
