# August 29, 2023 TIL - The `take` Command

The `take` command creates a new directory and changes to it,
thus eliminating the need to type the two commands `mkdir` and `cd`.

The `take` will also create intermediate directories as needed.

```bash
# this
$ take /path/to/new/directory

# is the same as this
$ mkdir -p /path/to/new/directory && cd /path/to/new/directory

# or this
$ mkdir -p /path/to/new/directory
$ cd /path/to/new/directory
```

## Use Cases

- Use `take /new/dir` to replace `mkdir -p /new/dir && cd /new/dir` workflow

## References

- [Zsh Tricks to Blow your Mind](https://www.twilio.com/blog/zsh-tricks-to-blow-your-mind)

