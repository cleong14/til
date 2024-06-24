---
title: 2024-06-24 - TIL - Open Files from Finder in Nvim
date: 2024-06-24 12:34:50
tags: [open-files-from-finder-in-nvim, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2024-06-24 - TIL - Open Files from Finder in Nvim

Open files from `Finder.app` directly in `nvim` running in your preferred terminal emulator (e.g. `Alacritty.app`) using `Automator.app`.


## Setup - Create New `Neovim.app` Automator Application

1.  Open `Automator.app`
2.  Select `Application`
3.  Click `Choose`
4.  Search for `Run Shell Script`
5.  Double-click `Run Shell Script`
6.  For `Shell:`, select a shell to run your shell script (e.g. `/bin/zsh`)
7.  For `Pass input:`, select `as arguments`
8.  For example, if you want to use `/bin/zsh` in `Alacritty.app`:

```sh
#!/usr/bin/env zsh

/opt/homebrew/bin/alacritty --command /opt/homebrew/bin/nvim "$1"
```

Note: The full path to each executable must be specified.

9.  Save your Automator Application with an easy to remember name to an easy to find location (e.g. `/Applications/Neovim.app`)


## Usage - Open With `Neovim.app`


### Just Once

1.  Open `Finder.app`
2.  Right-click a `<file>` > Hover over `Open With` > Click `Other...`
3.  Locate/Select your Automator Application (e.g. `/Applications/Neovim.app`) > Click `Open`


### Always and for All Documents Similar to the Selected File

1.  Open `Finder.app`
2.  Right-click a `<file>` > Click `Get Info`
3.  Under `Open with:`, locate/select your Automator Application (e.g. `/Applications/Neovim.app`) > Click `Add`
4.  Click `Change All...`


## Use Cases

- Open files from `Finder.app` directly in `nvim` running in your preferred terminal emulator (e.g. `Alacritty.app`) using `Automator.app`
- In `Finder.app`, set files to "Always Open With" `Neovim.app` instead of `Xcode.app`
- Configure all similar files to "Always Open With" `Neovim.app`


## References

- [Answer - Open files in Neovim from Mac Finder (double-clicking)? : r/neovim](https://www.reddit.com/r/neovim/comments/11jowku/comment/jb4ekjd/)
- [Screenshot - Open files in Neovim from Mac Finder (double-clicking)? : Imgur: The magic of the Internet](https://imgur.com/gKU08Y9)
- [Use a shell script action in an Automator workflow on Mac - Apple Support](https://support.apple.com/guide/automator/use-a-shell-script-action-in-a-workflow-autbbd4cc11c/mac)
- [Automator - MacOS Automation](https://www.reddit.com/r/Automator/)


