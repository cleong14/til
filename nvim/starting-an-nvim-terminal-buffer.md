# May 05, 2023 TIL

## Starting an Nvim Terminal Buffer

There are several ways to create a terminal buffer:

- Run the `:terminal` command. (recommended)
- Call the `nvim_open_term()` or `termopen()` function.
- Edit a `term://` buffer. Examples:

```vim
:edit term://bash
:vsplit term://top
```

Note: To open a `term://` buffer from an autocmd, the `autocmd-nested`
    modifier is required.

```vim
autocmd VimEnter * ++nested split term://sh
```

(This is only mentioned for reference; use `:terminal` instead.)

When the terminal starts, the buffer contents are updated and the buffer is
named in the form of `term://{cwd}//{pid}:{cmd}`. This naming scheme is used
by `:mksession` to restore a terminal buffer (by restarting the `{cmd}`).

The terminal environment is initialized as in `jobstart-env`.
