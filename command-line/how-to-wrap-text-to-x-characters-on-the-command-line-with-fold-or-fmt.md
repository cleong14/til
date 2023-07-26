# July 25, 2023 TIL - How to Wrap Text to X Characters on the Command Line with fold or fmt

`fold` and `fmt` are core GNU tools that you likely already have available.
Both help to make output to the commandline more readable.

```bash
$ tldr fmt

fmt

Reformat a text file by joining its paragraphs and limiting the line width to given number of characters (75 by default).
More information: <https://www.gnu.org/software/coreutils/fmt>.

- Reformat a file:
    fmt path/to/file

- Reformat a file producing output lines of (at most) `n` characters:
    fmt -w n path/to/file

- Reformat a file without joining lines shorter than the given width together:
    fmt -s path/to/file

- Reformat a file with uniform spacing (1 space between words and 2 spaces between paragraphs):
    fmt -u path/to/file

# ------------------------------------------------------------------------

$ tldr fold

fold

Wraps each line in an input file to fit a specified width and prints it to the standard output.
More information: <https://manned.org/fold.1p>.

- Wrap each line to default width (80 characters):
    fold path/to/file

- Wrap each line to width "30":
    fold -w30 path/to/file

- Wrap each line to width "5" and break the line at spaces (puts each space separated word in a new line, words with length > 5 are wrapped):
    fold -w5 -s path/to/file

```

## Use Cases

- For maximum compatibility, use `fold` (POSIX compliant)
- For extra features such as "squishing" or joining lines if there is extra whitespace between words, use `fmt`

## References

- [Wrap Text to X Characters on the Command Line with fold or fmt — Nick Janetakis](https://nickjanetakis.com/blog/wrap-text-to-x-characters-on-the-command-line-with-fold-or-fmt)

