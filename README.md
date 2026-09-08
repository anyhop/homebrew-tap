# homebrew-tap

Homebrew formulae for [anyhop](https://github.com/anyhop)'s projects, for macOS
and Linux. One tap for all packages: `brew tap anyhop/tap`, then
`brew install <formula>`.

## Formulae

### anyhop

[anyhop](https://github.com/anyhop/anyhop) — a universal VPN client that manages
multiple VPN connections with rule-based routing.

```bash
brew install anyhop/tap/anyhop
```

Run the background daemon at login, supervised by Homebrew:

```bash
brew services start anyhop
```

Then open the Web UI with `anyhop ui`, or see the
[getting started guide](https://github.com/anyhop/anyhop/blob/main/docs/getting-started.md).

This is the deliberately **headless** anyhop channel: the `anyhop` CLI, the
background daemon and its loopback control API, and the bundled, version-locked
Web UI. It never installs any GUI component — the formula strips that surface at
install time and its `brew test` proves the absence.

On this channel, let `brew services` own the daemon rather than
`anyhop daemon install` (they would register competing launchd/`systemd --user`
units for the same user). `anyhop upgrade` recognizes a brew-owned install and
delegates to `brew upgrade anyhop`.

## Maintenance

Each formula's canonical source lives in its project repo — for anyhop, at
[`packaging/homebrew/anyhop.rb`](https://github.com/anyhop/anyhop/blob/main/packaging/homebrew/anyhop.rb).
Each stable release, the project's publish workflow verifies the release on
PyPI, pins the new sdist by its PyPI-recorded SHA-256, and pushes the updated
formula here. Manual edits to `Formula/` in this repo will be overwritten by the
next release.

> This tap's formula was renamed from `alle` to `anyhop` when the project was
> renamed (2026-09); the old `Formula/alle.rb` was removed in the first
> `anyhop` release.
