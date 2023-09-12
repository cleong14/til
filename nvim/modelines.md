# September 11, 2023 TIL - Modelines

```vimdoc
There are two forms of modelines.  The first form:
	[text{white}]{vi:|vim:|ex:}[white]{options}

[text{white}]		empty or any text followed by at least one blank
			character (<Space> or <Tab>); "ex:" always requires at
			least one blank character
{vi:|vim:|ex:}		the string "vi:", "vim:" or "ex:"
[white]			optional white space
{options}		a list of option settings, separated with white space
			or ':', where each part between ':' is the argument
			for a ":set" command (can be empty)

Examples:
   vi:noai:sw=3 ts=6  
   vim: tw=77  

The second form (this is compatible with some versions of Vi):

	[text{white}]{vi:|vim:|Vim:|ex:}[white]se[t] {options}:[text]

[text{white}]		empty or any text followed by at least one blank
			character (<Space> or <Tab>); "ex:" always requires at
			least one blank character
{vi:|vim:|Vim:|ex:}	the string "vi:", "vim:", "Vim:" or "ex:"
[white]			optional white space
se[t]			the string "set " or "se " (note the space); When
			"Vim" is used it must be "set".
{options}		a list of options, separated with white space, which
			is the argument for a ":set" command
:			a colon
[text]			any text or empty

Examples:  
   /* vim: set ai tw=75: */
   /* Vim: set ai tw=75: */

The white space before {vi:|vim:|Vim:|ex:} is required.  This minimizes the
chance that a normal word like "lex:" is caught.  There is one exception:
"vi:" and "vim:" can also be at the start of the line (for compatibility with
version 3.0).  Using "ex:" at the start of the line will be ignored (this
could be short for "example:").

If the modeline is disabled within a modeline, subsequent modelines will be
ignored.  This is to allow turning off modeline on a per-file basis.  This is
useful when a line looks like a modeline but isn't.  For example, it would be
good to start a YAML file containing strings like "vim:" with
    # vim: nomodeline  
so as to avoid modeline misdetection.  Following options on the same line
after modeline deactivation, if any, are still evaluated (but you would
normally not have any).
```

```bash
## `set foldmethod=marker expandtab`

# vim: fdm=marker et
```

```lua
-- `set foldmethod=marker expandtab`

-- vim: fdm=marker et
```

## Use Cases

- Configure file specific settings

## References

- See `:help modeline`

