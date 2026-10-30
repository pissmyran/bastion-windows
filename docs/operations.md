# Operations and verification

## Before every push

There are no build or test checks in CI. The tests below are the only test gate, so they run locally before every push:

Test the core (works on Linux, macOS and Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Build the app (Windows only):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

## In CI

- **CodeQL** (GitHub's default setup) analyzes the code on every pull request and on `main`. Errors and serious security alerts block merging.
- **The documentation** is built strictly with Zensical when `docs/` or `zensical.toml` changes in a pull request.
- **The release** waits for the checks in `.github/release-required-checks`; see [Releases](release.md).


## CodeRabbit configuration

The central source is [pissmyran/coderabbit/.coderabbit.yaml](https://github.com/pissmyran/coderabbit/blob/main/.coderabbit.yaml). The repository's [.coderabbit.yaml](https://github.com/pissmyran/bastion_windows/blob/main/.coderabbit.yaml) uses `inheritance: true` and adds Windows-specific path instructions, explicit governance sources and linked Bastion repositories.

Before delivery, validate the complete YAML against the [current CodeRabbit schema](https://coderabbit.ai/integrations/schema.v2.json), rejecting duplicate keys. Check schema types and instruction length limits, and confirm every local path pattern matches the intended repository files. Arrays merge by key: local entries replace matching parent entries (for example, the same `path`); unique parent entries remain. Check that the merged configuration retains the shared scanners, advisory checks and disabled paid write features without changing approval settings.

After delivery, comment on the pull request:

```text
@coderabbitai configuration
```

Inspect CodeRabbit's resolved configuration to confirm the central source, shared scanners, advisory checks and disabled paid write features remain present. Verify unique parent array entries remain and only matching keyed entries are replaced. Confirm CodeRabbit can access the explicit governance files and linked repositories; a configured link alone does not prove access. Record unavailable sources and any verification that could not run. Local schema validation does not establish the service's resolved configuration or repository access.

## Security rules

- Private keys, tokens and passwords never go into the repo, logs or test data.
- Values that reach a shell are quoted and preferably passed through `env:`.
- A dependency is updated in the manifest that actually owns it.
