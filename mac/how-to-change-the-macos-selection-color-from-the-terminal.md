# June 23, 2023 TIL - How to Change the macOS Selection Color From the Terminal

Using `defaults`, change the macOS selection color.

```bash
# example: set green selection color
defaults write NSGlobalDomain AppleHighlightColor -string "0.615686 0.823529 0.454902"

# set blue selection color
defaults write NSGlobalDomain AppleHighlightColor -string "0.698039 0.843137 1.000000"

# get current selection color
defaults read NSGlobalDomain AppleHighlightColor
> 0.698039 0.843137 1.000000 Blue
```

## Use Cases

- Change macOS selection to your preferred color

## References

- [FelixKratz/SketchyVim: Adds all vim moves and modes to macOS text fields](https://github.com/FelixKratz/SketchyVim)

