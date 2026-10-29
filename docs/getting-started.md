# Getting started

## Prerequisites

.NET SDK (latest version) for the core. Windows with the Windows App SDK for the app.

## Build and test

Test the core (works on Linux, macOS and Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Build the app (Windows only):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

The core and its tests target cross-platform .NET and can be tested anywhere. The WinUI app needs Windows.

## Contents

| Path | Contents |
| --- | --- |
| `WindowsApp/Bastion.Core/` | The core: sessions, host list, sync, encryption and tools |
| `WindowsApp/Bastion.Core.Tests/` | Tests for the core, with its own copy of the sync fixture |
| `WindowsApp/` (root) | The WinUI app: `App.xaml`, `MainWindow.xaml` and `WindowsApp.csproj` |
