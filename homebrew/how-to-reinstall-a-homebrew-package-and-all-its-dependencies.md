# October 18, 2023 TIL - How to Reinstall a Homebrew Package and All its Dependencies

How to reinstall a Homebrew package and all its dependencies. This is useful when you have a broken package with an error message referencing a broken dependency.

For example, when attempting to run a broken installation of [commitizen-tools/commitizen](https://github.com/commitizen-tools/commitizen) you might see an error message similar to the following:

```bash
$ cz
Traceback (most recent call last):
  File "/opt/homebrew/bin/cz", line 5, in <module>
    from commitizen.cli import main
  File "/opt/homebrew/Cellar/commitizen/3.10.1/libexec/lib/python3.12/site-packages/commitizen/cli.py", line 13, in <module>
    from commitizen import commands, config, out, version_schemes
  File "/opt/homebrew/Cellar/commitizen/3.10.1/libexec/lib/python3.12/site-packages/commitizen/commands/__init__.py", line 1, in <module>
    from .bump import Bump
  File "/opt/homebrew/Cellar/commitizen/3.10.1/libexec/lib/python3.12/site-packages/commitizen/commands/bump.py", line 9, in <module>
    from commitizen import bump, cmd, factory, git, hooks, out
  File "/opt/homebrew/Cellar/commitizen/3.10.1/libexec/lib/python3.12/site-packages/commitizen/bump.py", line 11, in <module>
    from commitizen.version_schemes import DEFAULT_SCHEME, Version, VersionScheme
  File "/opt/homebrew/Cellar/commitizen/3.10.1/libexec/lib/python3.12/site-packages/commitizen/version_schemes.py", line 10, in <module>
    from packaging.version import InvalidVersion  # noqa: F401: Rexpose the common exception
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ModuleNotFoundError: No module named 'packaging'
```

To fix this, run the following command:

```bash
$ brew reinstall $(brew deps commitizen) commitizen
```

This will reinstall [commitizen-tools/commitizen](https://github.com/commitizen-tools/commitizen) from Homebrew, and all its dependencies.

## Use Cases

- Fix a broken Homebrew package
- Reinstall a Homebrew package and all its dependencies

## References

- [Release 3.10.1 (macos/homebrew): ModuleNotFoundError: No module named 'yaml' · Issue #887 · commitizen-tools/commitizen](https://github.com/commitizen-tools/commitizen/issues/887)

