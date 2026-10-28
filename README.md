# Bastion för Windows

**Dokumentation:** [pissmyran.github.io/bastion_windows](https://pissmyran.github.io/bastion_windows/)

Bastion är en SSH-klient. Det här repot innehåller versionen för Windows med WinUI, byggd med C#, .NET, WinUI och SSH.NET. Övriga plattformar har egna repon: [Bastion för Apple](https://github.com/pissmyran/bastion_apple), [Bastion för Linux](https://github.com/pissmyran/bastion_linux), [Bastion för Android](https://github.com/pissmyran/bastion_android).

## Innehåll

| Plats | Innehåll |
| --- | --- |
| `WindowsApp/Bastion.Core/` | Kärnan: sessioner, värdlista, synk, kryptering och verktyg |
| `WindowsApp/Bastion.Core.Tests/` | Tester för kärnan, med en egen kopia av synkfixturen |
| `WindowsApp/` (rot) | WinUI-appen: `App.xaml`, `MainWindow.xaml` och `WindowsApp.csproj` |

## Kom igång

Testa kärnan (fungerar på Linux, macOS och Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Bygg appen (bara på Windows):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

Kärnan och testerna riktar sig mot plattformsoberoende .NET och kan testas överallt. WinUI-appen kräver Windows.

## Mer

- [Dokumentationen](https://pissmyran.github.io/bastion_windows/) – kom igång, arkitektur, drift, synkformat och release
- [SECURITY.md](SECURITY.md) – rapportera en sårbarhet
- [CONTRIBUTING.md](CONTRIBUTING.md) – bidra
