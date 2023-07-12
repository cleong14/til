# July 11, 2023 TIL - How to Build Neovim From Source

Building Neovim from source is useful when you want to use neovim-nightly
but your package manager does not support it.

```bash
## when in doubt/to uninstall neovim built from source
$ make distclean

## build/install neovim from source for termux
# PREFIX=/data/data/com.termux/files/usr # termux

# 1. git clone neovim source repo
$ git clone https://github.com/neovim/neovim

# 2. build neovim && install to termux custom prefix location
$ cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo CMAKE_INSTALL_PREFIX=$PREFIX/bin/nvim install

# 3. anytime you update neovim source, before rebuilding be sure to run `make distclean`
$ cd neovim && make distclean

# 4. verify your installation is working
$ type nvim && nvim --version # or nvim -V1 -v
```

## Use Cases

- Build neovim from source on any platform
- Install neovim-nightly regardless of package manager support

## References

- [Building Neovim · neovim/neovim Wiki](https://github.com/neovim/neovim/wiki/Building-Neovim#quick-start)

