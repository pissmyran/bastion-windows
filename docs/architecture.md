# Architecture

Bastion for Windows is a standalone .NET app. The core is a port of the Swift core in Bastion for Apple, with the same field names in the sync format.

```text
        +-----------------------------+
        |   WinUI app (WindowsApp/)   |
        +--------------+--------------+
                       |
        +--------------+--------------+
        |  Bastion.Core (.NET, C#)    |
        |  ssh, sync, encryption      |
        +--------------+--------------+
                       |
                    SSH.NET
```

## Parts

- **Bastion.Core** holds everything that is not user interface and can be tested without Windows.
- **The WinUI app** in `WindowsApp/` is only the interface on top of the core.
- **Sync** (`SyncEngine`, `SyncState`, `SyncCrypto`) follows the format from Bastion for Apple.

## Security boundary

Host key verification in `KnownHosts.cs` and `HostAuth.cs` rejects a changed key for the same host and port. Keys and passwords are never stored in the repo or in test data.
