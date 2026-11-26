# Jasiri apt repository

**Website: [jasiri.benlester.me](https://jasiri.benlester.me)**

A public Linux apt repository at `apt.benlester.me`, with downloadable package releases. It serves Debian-style `.deb` packages rebuilt for [Jasiri](https://github.com/lester-01/jasiri), the Android app that has a full Linux system and an AI assistant built in. Inside Jasiri you install them with normal `apt`. The same packages can be downloaded straight from this repository's [releases](https://github.com/lester-01/jasiri-apt/releases).

## What is here

- A signed apt index for the `stable` suite, component `jasiri-main`, for `aarch64`, `arm`, `i686` and `x86_64`. The `x86_64` index lists over 3,000 packages today.
- Package releases on the [releases page](https://github.com/lester-01/jasiri-apt/releases): `.deb` files grouped in sets such as `main`, `x11`, `root`, `glibc` and `tur`, each for `aarch64` and `x86_64`. Each release is tagged with its set, architecture and a run number, for example `jasiri-main-x86_64-004`.

## Use it

Add the repository as an apt source (inside Jasiri, or on a compatible system), then update and install:

```
deb https://apt.benlester.me stable jasiri-main
```

```
apt update
apt install <package>
```

The index and `Release` file are signed, so apt needs the repository's public signing key before it trusts the source. The key is published on the website and is regenerated on every build, so always fetch the current one from there. To fetch one package by hand, download its `.deb` from the releases page and install it with `dpkg -i`.

## Notes

- This repository holds the published release files only. The tool that builds and signs the indexes is kept in a separate private repository.
- The packages are built for the Jasiri Android environment (a Termux-style prefix), so they are meant for Jasiri, not for a regular desktop Linux install.

---

Built by [Ben Lester](https://benlester.me), a software and systems engineer. See more at [projects.benlester.me](https://projects.benlester.me).
