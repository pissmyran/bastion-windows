# Synkformat

Bastion för Windows läser och skriver samma synkformat som de andra plattformarna. **Källan** till formatet är Swift-modellerna i [Bastion för Apple](https://github.com/pissmyran/bastion_apple).

## Fixturen

`WindowsApp/Bastion.Core.Tests/csharp-hosts-fixture.json` är en kopia av värdformatet från [Bastion för Apple](https://github.com/pissmyran/bastion_apple/tree/main/Tests/fixtures). `HostStoreTests` läser den och visar att C#-sidan kan avkoda Swifts format.

## När formatet ändras i Bastion för Apple

1. Uppdatera fixturen från `Tests/fixtures/` i Bastion för Apple.
2. Uppdatera `Host`, `HostStore`, `Snippet`, `SyncState`, `SyncEngine` och `SyncCrypto`.
3. Kör testerna. Ändra aldrig en fixtur för att få ett test grönt.
