# Sync format

Bastion for Windows reads and writes the same sync format as the other platforms. The **source** of the format is the Swift models in [Bastion for Apple](https://github.com/pissmyran/bastion_apple).

## The fixture

`WindowsApp/Bastion.Core.Tests/csharp-hosts-fixture.json` is a copy of the host format from [Bastion for Apple](https://github.com/pissmyran/bastion_apple/tree/main/Tests/fixtures). `HostStoreTests` reads it and shows that the C# side can decode Swift's format.

## When the format changes in Bastion for Apple

1. Update the fixture from `Tests/fixtures/` in Bastion for Apple.
2. Update `Host`, `HostStore`, `Snippet`, `SyncState`, `SyncEngine` and `SyncCrypto`.
3. Run the tests. Never change a fixture to make a test pass.
