# Arkitektur

Bastion för Windows är en fristående .NET-app. Kärnan är en port av Swift-kärnan i Bastion för Apple, med samma fältnamn i synkformatet.

```text
        +-----------------------------+
        |   WinUI-app (WindowsApp/)   |
        +--------------+--------------+
                       |
        +--------------+--------------+
        |  Bastion.Core (.NET, C#)    |
        |  ssh, synk, kryptering      |
        +--------------+--------------+
                       |
                    SSH.NET
```

## Delar

- **Bastion.Core** innehåller allt som inte är gränssnitt och kan testas utan Windows.
- **WinUI-appen** i `WindowsApp/` är bara gränssnittet ovanpå kärnan.
- **Synk** (`SyncEngine`, `SyncState`, `SyncCrypto`) följer formatet från Bastion för Apple.

## Säkerhetsgräns

Värdnyckelkontrollen i `KnownHosts.cs` och `HostAuth.cs` avvisar en ändrad nyckel för samma värd och port. Nycklar och lösenord lagras aldrig i repot eller i testdata.
