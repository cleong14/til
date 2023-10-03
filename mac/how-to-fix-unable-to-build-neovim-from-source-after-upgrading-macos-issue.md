# October 02, 2023 TIL - How to Fix "Unable to Build Neovim From Source After Upgrading Macos" Issue

If you've just upgrading your MacOS, you may encounter errors when trying to
build Neovim from source due to an incompatible XCode CommandLineTools (CLT)
version. You may also encounter warnings/errors when running `brew` commands.

> The quickest fix for these issues is to downgrade XCode CLT to the previous
> version until a fix is released for the latest version of XCode CLT.

## How to Downgrade XCode CLT

1. Remove all existing XCode CLT versions from your system

```bash
$ sudo rm -rf /Library/Developer/CommandLineTools
```

2. Download/Install previous XCode CLT versions from [Downloads - Apple Developer](https://developer.apple.com/download/all/?q=command%20line%20tools)
3. Once a previous version of XCode CLT is installed, rerunning the previously failing command(s) (e.g. build neovim from source, any `brew` command, etc.) should now pass with no warnings/errors

## Use Cases

1. Fix fatal errors when trying to build neovim from source
2. Fix warnings when running `brew` commands

## References

- [xcode - How to downgrade command line tools MacOS - Stack Overflow](https://stackoverflow.com/questions/41327298/how-to-downgrade-command-line-tools-macos)
- [Downloads - Apple Developer](https://developer.apple.com/download/all/?q=command%20line%20tools)

