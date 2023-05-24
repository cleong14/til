# The Difference Between Using `glob` and `noglob` When Specifying Zsh Completion Options

What effect do these options have on how the completion function behaves?

In zsh, the `glob` option causes the shell to perform filename generation (or globbing) on the arguments to the function, while the `noglob` option disables this feature.

When using `compctl`, `glob` is the default behavior, so omitting both `glob` and `noglob` will result in globbing being enabled for the arguments passed to the completion function.

However, when using the `-N` option, the `noglob` option is explicitly enabled, so filename generation is disabled for the arguments passed to the completion function.

In general, the `-N` option should be used when you want to prevent the shell from performing filename generation on the arguments to the function, while the `-g` option is used when you want to enable filename generation.

```bash
# _mycomp completion function
_mycomp() {
    # some code ...
}

# glob
compctl -g "_mycomp" mycommand  # using -g (glob)

# versus

# noglob
compctl -N "_mycomp" mycommand # using -N (noglob)
```

## Use Cases

- `-g` / `glob` should be used for filename generation completions (default behavior)
- `-N` / `noglob` should be used for non-filename generation completions (e.g. command completions)

