# Jasiri apt repository

**Website: [jasiri.benlester.me](https://jasiri.benlester.me)**

The package repository for the Jasiri Linux system: a public, signed Debian-style apt repository at **`apt.benlester.me`**. [Jasiri](https://github.com/lester-01/jasiri) is an Android app that gives you a full Linux system and an AI assistant on your phone, and this is where its software comes from. Inside Jasiri you install from it with plain `apt`. The same `.deb` files are also published here as GitHub releases, so you can download any package by hand.

## At a glance

| | |
|---|---|
| Repository URL | `https://apt.benlester.me` |
| Suite / component | `stable` / `jasiri-main` |
| Architectures | `aarch64` and `x86_64` are published. 32-bit ARM and `i686` are declared in the index but not built yet |
| Runs on | Android phones, and x86_64 devices and emulators |
| Signing | The index and `Release` file are signed |
| Index tool | [aptly](https://www.aptly.info/) |
| Release files | [github.com/lester-01/jasiri-apt/releases](https://github.com/lester-01/jasiri-apt/releases) |

## How it is maintained

I maintain this as a small Linux distribution. A pipeline written in Go takes upstream packages, patches them to install under Jasiri's own directory, builds and signs the apt index, and publishes the result to the repository and to the release files here. Each build is resumable and tested.

Keeping up with upstream is moving to a scheduled GitHub Actions workflow (CI/CD): check for new and updated upstream packages every day, then rebuild, sign and publish only what changed, so the repository stays current without manual runs. The pipeline's code lives in a separate private repository.

## Use it

The index and `Release` file are signed. Jasiri ships with the repository's public signing key, so inside Jasiri apt already trusts this source and you can just run `apt update` and `apt install <package>`.

To use the repository from another compatible system, download the public key and point the source at it:

```
curl -fsSL https://apt.benlester.me/jasiri-archive-keyring.gpg -o /etc/apt/keyrings/jasiri-archive-keyring.gpg
```

```
deb [signed-by=/etc/apt/keyrings/jasiri-archive-keyring.gpg] https://apt.benlester.me stable jasiri-main
```

```
apt update
apt install <package>
```

The key only changes if the signing key is replaced, which would come with a Jasiri update that ships the new key.

## Download a single package

Every package is also attached to a GitHub release. Download the `.deb` from the [releases page](https://github.com/lester-01/jasiri-apt/releases) and install it with `dpkg -i <file>.deb`.

Releases are grouped by package set and architecture, and each is tagged with a run number, for example `jasiri-main-x86_64-004`:

| Set | What it holds |
|---|---|
| `main` | The core package set |
| `x11` | Graphical (X11 and Wayland) packages |
| `root` | Packages that need root |
| `glibc` | glibc-based packages |
| `tur` | Community packages, split into `continuous`, `nightly`, `multilib`, `hacking` and `on-device` |

Each set is published for `aarch64` and `x86_64`.

## Where the packages come from

The packages are derived from open-source projects, with file paths inside some binaries adjusted so they work in Jasiri's own storage location. The index records the original upstream checksums (`X-Upstream-SHA256` and friends) next to each rebuilt file, so every package can be traced back to its source. Licenses for the programs are in the Linux system itself, under `usr/share/doc` and `usr/share/licenses`. The upstream projects and their licenses are listed in the [Jasiri notices](https://github.com/lester-01/jasiri/blob/main/NOTICES.md).

## Notes

- Because of the adjusted paths, these packages are meant for Jasiri, not for a regular desktop Linux install.
- This repository holds the published release files only.

---

Built by [Ben Lester](https://benlester.me), a software and systems engineer. See more at [projects.benlester.me](https://projects.benlester.me).
