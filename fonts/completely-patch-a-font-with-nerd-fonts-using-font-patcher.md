---
title: 2024-06-08 - TIL - Completely Patch a Font With Nerd Fonts Using Font-Patcher
date: 2024-06-08 01:34:54
tags: [completely-patch-a-font-with-nerd-fonts-using-font-patcher, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2024-06-08 - TIL - Completely Patch a Font With Nerd Fonts Using Font-Patcher

Completely patch fonts with Nerd Fonts using Font-Patcher.


## Usage

```sh
# Completely patch "FiraCode Nerd Font" with double-width glyphs using Font-Patcher
$ fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFont-Bold.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFont-Light.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFont-Medium.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFont-Regular.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFont-Retina.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFont-SemiBold.ttf

# Completely patch "FiraCode Nerd Font Mono" with single-width glyphs using Font-Patcher
$ fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontMono-Bold.ttf --mono
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontMono-Light.ttf --mono
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontMono-Medium.ttf --mono
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontMono-Regular.ttf --mono
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontMono-Retina.ttf --mono
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontMono-SemiBold.ttf --mono

# Completely patch "FiraCode Nerd Font Propo" with double-width glyphs using Font-Patcher
$ fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontPropo-Bold.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontPropo-Light.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontPropo-Medium.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontPropo-Regular.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontPropo-Retina.ttf
; fontforge -script ~/code/FontPatcher/font-patcher --complete FiraCodeNerdFontPropo-SemiBold.ttf
```


## Use Cases

- Fix unpatched fonts with Nerd Fonts using Font-Patcher after installing a new font or updating an existing font.


## References

- [Nerd Fonts - Font Patcher](https://github.com/ryanoasis/nerd-fonts#font-patcher)


