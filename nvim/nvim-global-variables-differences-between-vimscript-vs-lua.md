# September 27, 2023 TIL - Nvim Global Variables - Differences Between Vimscript vs Lua

The Lua syntax when working with global variables in nvim differs from vimscript.

In Lua, the dot notation (`.`) is used to access nested tables, and the
underscore (`_`) is used instead of the hash symbol (`#`) for variable names.

## Example

In [haya14busa/vim-asterisk](https://github.com/haya14busa/vim-asterisk), to enable keepCursor feature in `vimscript`:

```vim
let g:asterisk#keeppos = 1
```

To enable keepCursor feature in `lua`:

```lua
vim.g.asterisk_keeppos = 1
```

## Use Cases

- Convert nvim global variables from `vimscript` to `lua`

