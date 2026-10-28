# Kom igång

## Förutsättningar

.NET SDK (senaste versionen) för kärnan. Windows med Windows App SDK för appen.

## Bygg och testa

Testa kärnan (fungerar på Linux, macOS och Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Bygg appen (bara på Windows):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

Kärnan och testerna riktar sig mot plattformsoberoende .NET och kan testas överallt. WinUI-appen kräver Windows.

## Innehåll

| Plats | Innehåll |
| --- | --- |
| `WindowsApp/Bastion.Core/` | Kärnan: sessioner, värdlista, synk, kryptering och verktyg |
| `WindowsApp/Bastion.Core.Tests/` | Tester för kärnan, med en egen kopia av synkfixturen |
| `WindowsApp/` (rot) | WinUI-appen: `App.xaml`, `MainWindow.xaml` och `WindowsApp.csproj` |
