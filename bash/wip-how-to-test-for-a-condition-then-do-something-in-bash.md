# July 06, 2023 TIL - How to Test for a Condition Then Do Something in Bash

CONTEXT

```bash
$ tldr test

test

Check file types and compare values.
Returns 0 if the condition evaluates to true, 1 if it evaluates to false.
More information: <https://www.gnu.org/software/coreutils/test>.

- Test if a given variable is equal to a given string:
    test "$MY_VAR" == "/bin/zsh"

- Test if a given variable is empty:
    test -z "$GIT_BRANCH"

- Test if a file exists:
    test -f "path/to/file_or_directory"

- Test if a directory does not exist:
    test ! -d "path/to/directory"

- If A is true, then do B, or C in the case of an error (notice that C may run even if A fails):
    test condition && echo "true" || echo "false"

❯ test README.md
❯ test ./README.md
❯ test ./READMEeee.md
❯ test -f README.md
❯ test -f README.md && echo 'has readme'
has readme
❯ test -f READMEeee.md && echo 'has readme'
❯ test -f READMEeee.md && echo 'has readme' || echo 'no mo readmes'
no mo readmes
```

## Use Cases

USE-CASES

## References

- [REFERENCE](#)

