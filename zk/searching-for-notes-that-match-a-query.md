# Searching for Notes that Match a Query

## Searching for a Match in a Note Title

```bash
$ zk list -m $TITLE_QUERY # -m, --match=$TITLE_QUERY,...            Terms to search for in the notes.
```

## Searching for a Match in a Note Title or Note Contents

To include note contents in our search, we'll need to perform our search in interactive mode using
[junegunn/fzf](https://github.com/junegunn/fzf/). fzf is a general-purpose command-line fuzzy finder.

```bash
$ zk list -i # -i, --interactive                Select notes interactively with fzf.
```
