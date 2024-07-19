---
title: 2024-07-18 - TIL - Valid Combinations of GOOS (OS) and GOARCH (Architecture)
date: 2024-07-18 20:04:35
tags: [valid-combinations-of-goos-os-and-goarch-architecture, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2024-07-18 - TIL - Valid Combinations of GOOS (OS) and GOARCH (Architecture)

OS and Architecture standard values used in Kubernetes, Docker, etc.


## `$GOOS` & `$GOARCH` Values

The name of the target operating system and compilation architecture. These default to the values of `$GOHOSTOS` and `$GOHOSTARCH` respectively (described below).

Choices for `$GOOS` are `android`, `darwin`, `dragonfly`, `freebsd`, `illumos`, `ios`, `js`, `linux`, `netbsd`, `openbsd`, `plan9`, `solaris`, `wasip1`, and `windows`.

Choices for `$GOARCH` are `amd64` (64-bit x86, the most mature port), `386` (32-bit x86), `arm` (32-bit ARM), `arm64` (64-bit ARM), `ppc64le` (PowerPC 64-bit, little-endian), `ppc64` (PowerPC 64-bit, big-endian), `mips64le` (MIPS 64-bit, little-endian), `mips64` (MIPS 64-bit, big-endian), `mipsle` (MIPS 32-bit, little-endian), `mips` (MIPS 32-bit, big-endian), `s390x` (IBM System z 64-bit, big-endian), and `wasm` (WebAssembly 32-bit).

The valid combinations of `$GOOS` and `$GOARCH` are:

|  | `$GOOS`     | `$GOARCH`  |
|--|:------------|:-----------|
|  | `aix`       | `ppc64`    |
|  | `android`   | `386`      |
|  | `android`   | `amd64`    |
|  | `android`   | `arm`      |
|  | `android`   | `arm64`    |
|  | `darwin`    | `amd64`    |
|  | `darwin`    | `arm64`    |
|  | `dragonfly` | `amd64`    |
|  | `freebsd`   | `386`      |
|  | `freebsd`   | `amd64`    |
|  | `freebsd`   | `arm`      |
|  | `illumos`   | `amd64`    |
|  | `ios`       | `arm64`    |
|  | `js`        | `wasm`     |
|  | `linux`     | `386`      |
|  | `linux`     | `amd64`    |
|  | `linux`     | `arm`      |
|  | `linux`     | `arm64`    |
|  | `linux`     | `loong64`  |
|  | `linux`     | `mips`     |
|  | `linux`     | `mipsle`   |
|  | `linux`     | `mips64`   |
|  | `linux`     | `mips64le` |
|  | `linux`     | `ppc64`    |
|  | `linux`     | `ppc64le`  |
|  | `linux`     | `riscv64`  |
|  | `linux`     | `s390x`    |
|  | `netbsd`    | `386`      |
|  | `netbsd`    | `amd64`    |
|  | `netbsd`    | `arm`      |
|  | `openbsd`   | `386`      |
|  | `openbsd`   | `amd64`    |
|  | `openbsd`   | `arm`      |
|  | `openbsd`   | `arm64`    |
|  | `plan9`     | `386`      |
|  | `plan9`     | `amd64`    |
|  | `plan9`     | `arm`      |
|  | `solaris`   | `amd64`    |
|  | `wasip1`    | `wasm`     |
|  | `windows`   | `386`      |
|  | `windows`   | `amd64`    |
|  | `windows`   | `arm`      |
|  | `windows`   | `arm64`    |


## Use Cases

- OS and Architecture values reference when working with Kubernetes, Docker, etc.


## References

- [Optional Environment Variables - The Go Programming Language](https://go.dev/doc/install/source#environment)


