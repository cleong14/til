# May 09, 2023 TIL - How to Access Shell Environment Variables in Nvim

To access shell environment variables in Nvim, you can use `vim.env`. For
example, if we want to print the value of `$EDITOR` in Nvim:

```lua
--- in your ~/.zshrc
-- export EDITOR=nvim

print(vim.env.EDITOR)
-- > prints 'nvim' in messages
```

## Use Cases

Rather than setting a secret or token value directly in your nvim config, you
could set it as an environment variable and access its value using `vim.env`
inside nvim.

## References

- [`vim.env` Lua Variables - Lua - Neovim docs](https://neovim.io/doc/user/lua.html#vim.env)

