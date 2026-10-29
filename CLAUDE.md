# CLAUDE.md – bastion_windows

@AGENTS.md

Guidance for Claude Code in `pissmyran/bastion_windows`: Bastion for Windows, the SSH client for Windows with WinUI, built with C#, .NET, WinUI and SSH.NET. The other platforms have their own repos: [Bastion for Apple](https://github.com/pissmyran/bastion_apple), [Bastion for Linux](https://github.com/pissmyran/bastion_linux), [Bastion for Android](https://github.com/pissmyran/bastion_android).

The shared rules for all repos live in [STYRNING.md](https://github.com/pissmyran/.github/blob/main/STYRNING.md) in `pissmyran/.github`. The core rules below are a verbatim copy and stay in Swedish, because the copy is compared character by character with the source. Compare the version in the marker with the source at the start of every session (`curl -sS https://raw.githubusercontent.com/pissmyran/.github/main/STYRNING.md`); if the copy is older, update it first in a separate PR (`docs: sync core rules from .github`).

## Core rules

<!-- kärnregler:start version=2026-10-28 källa=https://github.com/pissmyran/.github/blob/main/STYRNING.md -->
1. **Inga personliga värden.** Repot är publikt. Skriv aldrig in riktiga id:n, domäner, e-postadresser, namn, nycklar, betallänkar eller kontouppgifter i kod, konfiguration, tester, dokumentation eller commit-meddelanden. Använd platshållare och `example.com`-värden.
2. **Inga hemligheter.** Tokens, lösenord, sessioner och nycklar hamnar aldrig i Git, loggar, issues eller publik dokumentation. Hemligheter läggs in utanför repot (Cloudflare, GitHub-miljöer, `wrangler secret put`).
3. **Gren och pull request.** Varje session börjar från senaste `main` (`git fetch origin main`) på en egen gren. `main` ändras bara genom en PR som squash-mergas. Ingen pushar direkt till `main`. En sessions arbete hålls i en PR.
4. **Testa lokalt före varje push.** Det finns inga testkontroller i CI. Repots egna tester och kontroller (avsnittet Kommandon i repots `CLAUDE.md`) är den enda testgrinden. Pusha aldrig med fallerande tester, och skriv tester för det du ändrar.
5. **Rör aldrig workflows.** `.github/workflows/`, `.github/actions/` och `CODEOWNERS` ändras inte av Claude, inte ens för att laga ett fel. Ingen kontroll stoppar det längre, men regeln gäller fullt ut. Behövs en ändring: beskriv den i ett issue och låt ägaren göra den. Bara Renovate och Dependabot får uppdatera dem.
6. **Granskning.** CodeRabbit, Sourcery och Codex granskar, och CodeQL (GitHubs standardinställning) skannar. Varje granskningstråd måste lösas innan merge. Svara i tråden med vad du ändrade, eller med skälet om fyndet är brus.
7. **Auto-merge sist.** Slå på auto-merge först när granskningsbotarna har granskat den senaste commiten (CodeRabbit hoppar över `docs/` och `*.md`; för sådana ändringar räcker Sourcery och Codex), alla trådar är lösta och alla kontroller som körs på PR:en är gröna, även de som reglerna inte kräver (till exempel `Dokumentation`).
8. **Laga orsaken, inte symptomet.** När något fallerar eller en granskning kräver ändring: läs allt, hitta orsaken och gör om den delen rätt. Små uppenbara fel får rättas direkt. Försvaga aldrig ett test, hoppa aldrig över en kontroll och tysta aldrig en varning.
9. **Säkerhet först.** Säkerhetslarm (CodeQL, Dependabot, Renovate) går före annat arbete. Länka issuet med `Closes #n`.
10. **Senaste versionerna.** Lägg aldrig till nya låsningar till ett versionsnummer; använd `@latest`, `node`, `latest` och versionsintervall. Befintliga låsningar som Renovate håller aktuella (till exempel `packageManager`, `requirements-docs.txt`, `.node-version`, lockfiler och actions låsta med commit-SHA) behålls och ändras bara av Renovate.
11. **Commits och titlar.** Sessionen signerar commits själv. Ändra aldrig gits användare, e-post eller signering, och använd aldrig `--no-verify`. PR-titeln blir commiten på `main` och skrivs på engelska enligt Conventional Commits: `typ: beskrivning` eller `typ(område): beskrivning`, med typ feat, fix, docs, refactor, perf, test, build, ci, chore, style eller revert.
12. **Dokumentation i samma PR.** Ändras beteende, inställningar eller kommandon uppdateras `README.md`, `docs/` och repots `CLAUDE.md` i samma PR.
13. **Inga lösa grenar.** Radera grenen när PR:en är mergad eller stängd. PR:er från forkar är förslag: gör ändringen själv på en egen gren om den är önskad, och stäng originalet med tack och länk.
14. **Noll kronor.** Slå aldrig på något som kan kosta pengar.
15. **GitHub bara via REST.** `gh pr` och `gh issue` fungerar inte i molnsessioner (GraphQL är avstängt). Använd `gh api` och de särskilda `ccr`-vägarna; se avsnittet GitHub från sessionen.
<!-- kärnregler:slut -->

## Commands

Test the core (works on Linux, macOS and Windows):

```bash
dotnet test WindowsApp/Bastion.Core.Tests
```

Build the app (Windows only):

```bash
dotnet build WindowsApp/WindowsApp.csproj
```

The core and its tests target cross-platform .NET and can be tested anywhere. The WinUI app needs Windows.

## Rules for this repo

- **Language:** everything in this repo is English: code, comments, docstrings, documentation, PR titles and bodies, commit messages, review replies and labels. Only the core rules block above stays in Swedish. Older code still has Swedish comments and UI text; write every new or changed comment and string in English.
- **The sync format is owned by Bastion for Apple.** The fixture in `Bastion.Core.Tests` is a copy; follow `docs/sync-format.md` when the format changes.
- **The WinUI app cannot be built on Linux.** Test the core locally and say in the PR that the app could not be built.
- **NuGet:** the cloud session's proxy may refuse `api.nuget.org`. If `dotnet test` cannot run, say so in the PR instead of silently skipping the tests.
- **The documentation** is a Zensical site: `docs/`, `zensical.toml` and the home page template in `overrides/home.html`. Build it locally with `pip install --upgrade zensical` and `zensical build --strict`. New pages go into `nav` in `zensical.toml`.
- **The release** is driven by the PR titles and the checks in `.github/release-required-checks`; see `docs/release.md`.

## Review in this repo

- **Gate:** `main` requires a PR, signed commits, linear history, resolved review threads and CodeQL without errors or serious alerts. No other checks are required, but the ones that run must be green. The local tests under Commands are the test gate.
- **CodeRabbit:** inherits the central configuration in `pissmyran/coderabbit`. The repo's `.coderabbit.yaml` points out risk areas with their own review instructions; read the part for the files you change before you start.
- **Sourcery and Codex:** also review, as GitHub apps without their own configuration here, and they review documentation too. Treat their threads like CodeRabbit's.
- **Extra care:** host key verification, sync format and encryption, commands built for remote systems.

## Token optimizer

- **What it is:** the platform-skills token optimizer runs in audit mode. `.token-optimizer.yaml` holds the settings, `.token-optimizer/optimize.sh` is the hook script and `.claude/agents/platform-bulk-reader.md` is the cheap reader agent.
- **What it does:** a `PreToolUse` hook in `.claude/settings.json` logs oversized reads to `.token-optimizer/decisions.log` (git-ignored). It never blocks a read.
- **Changing it:** switch `mode` to `redirect` only after `.token-optimizer/probe/run-probe.sh` has verified delegation. Set `enabled: false` to turn it off.

## GitHub from a session

GraphQL is disabled, so `gh pr` and `gh issue` do not work. Use REST:

- Open a PR: `gh api repos/pissmyran/bastion_windows/pulls -f base=main -f head=<branch> -f title='…' -f body='…'`
- PR from a branch: `gh api 'repos/pissmyran/bastion_windows/pulls?head=pissmyran:<branch>&state=open'`
- Issue: `gh api repos/pissmyran/bastion_windows/issues/<n>` and `…/issues/<n>/comments`
- Review threads: `gh api repos/pissmyran/bastion_windows/pulls/<n>/ccr/review_threads`
- Reply in a thread: `gh api repos/pissmyran/bastion_windows/pulls/<n>/comments/<id>/replies -f body='…'`
- Resolve a thread: `gh api -X POST repos/pissmyran/bastion_windows/pulls/<n>/ccr/comments/<id>/resolve`
- Checks: `gh api repos/pissmyran/bastion_windows/commits/<sha>/check-runs`
- Enable auto-merge: `gh api -X PUT repos/pissmyran/bastion_windows/pulls/<n>/ccr/auto_merge -f merge_method=squash`
- If the PR is already mergeable (auto-merge is then refused), squash-merge directly: `gh api -X PUT repos/pissmyran/bastion_windows/pulls/<n>/merge -f merge_method=squash`
- Close a PR: `gh api -X PATCH repos/pissmyran/bastion_windows/pulls/<n> -f state=closed`
- Delete a branch: GitHub deletes the branch on merge. A closed PR's branch is deleted with `git push origin --delete <branch>` (the API route is blocked).
