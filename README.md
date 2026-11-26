# Jasiri apt repository

**Website: [jasiri.benlester.me](https://jasiri.benlester.me)**

A public, signed Debian-style apt repository at **`apt.benlester.me`**. It serves the Linux packages for [Jasiri](https://github.com/lester-01/jasiri), the Android app that gives you a full Linux system and an AI assistant on your phone. Inside Jasiri you install from it with plain `apt`. The same `.deb` files are also published here as GitHub releases, so you can download any package by hand.

## At a glance

| | |
| --- | --- |
| Repository URL | `https://apt.benlester.me` |
| Suite / component | `stable` / `jasiri-main` |
| Architectures | `aarch64` (about 3,050 packages) and `x86_64` (about 3,045 packages) |
| Signing | The index and `Release` file are signed |
| Index tool | [aptly](https://www.aptly.info/) |
| Release files | [github.com/lester-01/jasiri-apt/releases](https://github.com/lester-01/jasiri-apt/releases) |

The `Release` file also declares `arm` and `i686`, but those indexes are empty today.

## Use it

Download the repository's public signing key, then add the source with that key and install:

```
curl -fsSL https://apt.benlester.me/jasiri-archive-keyring.gpg -o jasiri-archive-keyring.gpg
```

```
deb [signed-by=/path/to/jasiri-archive-keyring.gpg] https://apt.benlester.me stable jasiri-main
```

```
apt update
apt install <package>
```

Replace `/path/to/` with wherever you keep the key. The key is regenerated on every build of the repository, so fetch the current copy from [apt.benlester.me/jasiri-archive-keyring.gpg](https://apt.benlester.me/jasiri-archive-keyring.gpg) and do not keep an old one.

## Download a single package

Every package is also attached to a GitHub release. Download the `.deb` from the [releases page](https://github.com/lester-01/jasiri-apt/releases) and install it with `dpkg -i <file>.deb`.

Releases are grouped by package set and architecture, and each is tagged with a run number, for example `jasiri-main-x86_64-004`:

| Set | What it holds |
| --- | --- |
| `main` | The core package set |
| `x11` | Graphical (X11 and Wayland) packages |
| `root` | Packages that need root |
| `glibc` | glibc-based packages |
| `tur` | Community packages, split into `continuous`, `nightly`, `multilib`, `hacking` and `on-device` |

Each set is published for `aarch64` and `x86_64`.

## How the packages are made

The packages are rebuilt from the [Termux packages](https://github.com/termux/termux-packages) project. File paths inside some binaries are adjusted so they work in Jasiri's own storage location, the way Termux packages use a Termux prefix. The package index records the original upstream checksums (`X-Upstream-SHA256` and friends) next to each rebuilt file, so you can trace every package back to its source. Licenses for the programs are in the Linux system itself, under `usr/share/doc` and `usr/share/licenses`, and third-party notices are in the [Jasiri notices](https://github.com/lester-01/jasiri/blob/main/NOTICES.md).

Jasiri is an independent product and is not affiliated with or endorsed by the Termux project.

## Notes

- Because of the adjusted paths, these packages are meant for Jasiri, not for a regular desktop Linux install.
- This repository holds the published release files only. The tool that builds and signs the indexes lives in a separate private repository.

---

Built by [Ben Lester](https://benlester.me), a software and systems engineer. See more at [projects.benlester.me](https://projects.benlester.me).
