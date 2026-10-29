# Bastion for Windows

**Documentation:** [pissmyran.github.io/bastion_windows](https://pissmyran.github.io/bastion_windows/)

Bastion is an SSH client. This repo holds the version for Windows with WinUI, built with C#, .NET, WinUI and SSH.NET. The other platforms have their own repos: [Bastion for Apple](https://github.com/pissmyran/bastion_apple), [Bastion for Linux](https://github.com/pissmyran/bastion_linux), [Bastion for Android](https://github.com/pissmyran/bastion_android). The [Bastion hub](https://github.com/pissmyran/bastion) ties them together.

## Contents

| Path | Contents |
| --- | --- |
| `WindowsApp/Bastion.Core/` | The core: sessions, host list, sync, encryption and tools |
| `WindowsApp/Bastion.Core.Tests/` | Tests for the core, with its own copy of the sync fixture |
| `WindowsApp/` (root) | The WinUI app: `App.xaml`, `MainWindow.xaml` and `WindowsApp.csproj` |

## Getting started

Test the core (works on Linux, macOS and Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Build the app (Windows only):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

The core and its tests target cross-platform .NET and can be tested anywhere. The WinUI app needs Windows.

## More

- [The documentation](https://pissmyran.github.io/bastion_windows/): getting started, architecture, operations, sync format and releases
- [SECURITY.md](SECURITY.md): report a vulnerability
- [CONTRIBUTING.md](CONTRIBUTING.md): contribute
