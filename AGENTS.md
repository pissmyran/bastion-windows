# AGENTS.md – bastion_windows

Bastion for Windows: the SSH client for Windows with WinUI, built with C#, .NET, WinUI and SSH.NET.

Read the shared rules at the start of every session: [GOVERNANCE.md](https://raw.githubusercontent.com/pissmyran/.github/main/GOVERNANCE.md) and [BASTION.md](https://raw.githubusercontent.com/pissmyran/.github/main/BASTION.md).

## Read first

1. [docs/architecture.md](docs/architecture.md): components and security boundaries.
2. [docs/operations.md](docs/operations.md): verification before pushing.
3. [docs/sync-format.md](docs/sync-format.md): when the host list or sync is involved.

## Commands

Test the core (works on Linux, macOS and Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Build the app (Windows only):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

## Rules

- **The WinUI app cannot be built on Linux.** Test the core.
- **The fixture** in `Bastion.Core.Tests` is a copy of the sync format owned by `bastion_apple`.
- **Extra care:** host key verification, sync format and encryption, commands built for remote systems.
