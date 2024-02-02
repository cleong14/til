# 2024-02-01 - TIL - How to Configure Zsh Line Editor (ZLE) Highlighting Behavior when Pasting Text Into the Terminal

When pasting text into the terminal, the initial pasted text will often times have style applied to it. These styles will likely differ depending on the terminal emulator used. Some terminal emulators may render the pasted text with a background color, while others may render the pasted text italicized.

Some may be fine with this behavior, while others may find it annoying. Especially when the pasted text styles conflict with the configured colorscheme.

If you are in the latter and annoyed by the pasted text style, here is how you can configure Zsh Line Editor (ZLE) highlighting behavior when pasting text into the terminal.


## Usage

```sh
# Configure Zsh Line Editor (ZLE) highlighting behavior
#
# Configure highlighting when pasting text into the terminal
# https://news.ycombinator.com/item?id=26757438
#
# in your `~/.zshrc`, add the following:
#
zle_highlight+=(paste:none)
```


## Use Cases

- Configure Zsh Line Editor (ZLE) highlighting behavior when pasting text into the terminal


## References

- [Remove background highlighting when pasting text into the terminal | Hacker News](https://news.ycombinator.com/item?id=26757438)

