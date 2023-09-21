# September 20, 2023 TIL - Bash Here Documents & Here Strings

## Here Documents

This type of redirection instructs the shell to read input from the current
source until a line containing only word (with no trailing blanks) is seen.
All of the lines read up to that point are then used as the standard input for
a command.

The format of here-documents is:

```bash
<<[-]word
    here-document
delimiter
```

No parameter expansion, command substitution, arithmetic expansion, or pathname
expansion is performed on word.  If any characters in word are quoted, the
delimiter is the result of quote removal on word, and the lines in the
here-document are not expanded.  If word is unquoted, all lines of the
here-document are subjected to parameter expansion, command substitution, and
arithmetic expansion.  In the latter case, the character sequence \<newline> is
ignored, and \ must be used to quote the characters \, $, and `.

If the redirection operator is <<-, then all leading tab characters are
stripped from input lines and the line containing delimiter.  This allows
here-documents within shell scripts to be indented in a natural fashion.


## Here Strings

A variant of here documents, the format is:

```bash
<<<word
```

The word is expanded and supplied to the command on its standard input.


## Examples

```bash
$ test_input='some test input'

## bash herestring - multilines with variable substitution
$ echo "This is a string
that spans multiple
lines
with test_input: $test_input."
#> This is a string
#> that spans multiple
#> lines
#> with test_input: some test input.


## bash heredoc - multilines with indention and variable substitution
$ cat << EOF
    This is line 1 of the test_input: $test_input.
        This is line 2 of the test_input: $test_input.
This is line 3 of the test_input: $test_input.
EOF
#>     This is line 1 of the test_input: some test input.
#>         This is line 2 of the test_input: some test input.
#> This is line 3 of the test_input: some test input.
```


## Use Cases

- Use herestring to pass single multiline string as input to a command/script
- Use heredoc to pass multiline string document as input to a command/script


## References

- See `man bash` then search for `Here Documents` and/or `Here Strings`

