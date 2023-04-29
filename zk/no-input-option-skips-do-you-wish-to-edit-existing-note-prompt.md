# `--no-input` Option Skips 'Do You Wish to Edit Existing Note' Prompt

## [zk/daily-journal.md](https://github.com/mickael-menu/zk/blob/main/docs/daily-journal.md) Documentation Example

Assume we created an alias for daily journal type notes:

```toml
# ~/.config/zk/config.toml

# ...

[alias]
daily = 'zk new --no-input "$ZK_NOTEBOOK_DIR/journal/daily"'

# ...

```

Let's unpack this alias:

-   `zk new` will refuse to overwrite notes. If you already created today's note, it will instead ask you if you wish to edit it. Using `--no-input` skips the prompt and edit the existing note right away.
-   `$ZK_NOTEBOOK_DIR` is set to the absolute path of the current [notebook](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/mickael-menu/zk/blob/main/docs/notebook.md) when running an alias. Using it allows you to run `zk daily` no matter where you are in the notebook folder hierarchy.
-   We need to use double quotes around `$ZK_NOTEBOOK_DIR`, otherwise it will not be expanded.

