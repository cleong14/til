---
title: 2024-04-24 - TIL - UPT — Universal Package-management Tool
date: 2024-04-24 17:21:42
tags: [upt-universal-package-management-tool, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2024-04-24 - TIL - UPT — Universal Package-management Tool

UPT provides a unified command interface to manage packages for any operating system.


## Install

```sh
## install

# Use Cargo
cargo install upt

# Use Shell (Mac, Linux)
curl -fsSL https://raw.githubusercontent.com/sigoden/upt/main/install.sh | sh -s -- --to /usr/local/bin

# Binaries for macOS, Linux, Windows, BSD
# Download from [GitHub Releases](https://github.com/sigoden/upt/releases), unzip and add `upt` to your $PATH.
```


## Usage

```sh
## usage

# `upt` allows OS specific package management commands such as
apt install $pkg          # Ubuntu, Debian, Linux Mint...
apk add $pkg              # Alpine
pacman -S $pkg            # Arch, Manjaro...
nix-env -i $pkg           # Nixos
xbps-install $pkg         # Voidlinux
emerge $pkg               # Gentoo

# to be unified under a single command 
upt install $pkg          # Works on any OS

# `upt` automatically detects OS and package manager
# alternatively, you can specify the package manager by setting `UPT_TOOL`
UPT_TOOL=brew upt install $pkg            # equal to `brew install $pkg`
UPT_TOOL=nix-env upt install $pkg         # equal to `nix-env -i $pkg`
```


## Use Cases

- Unified command interface to manage packages for any operating system
- Reduce cognitive load by only needing to remember one command across multiple systems


## References

- [sigoden/upt: Universal Package-management Tool for any OS.](https://github.com/sigoden/upt)


