---
title: 2024-06-10 - TIL - pip vs pipx
date: 2024-06-10 21:37:04
tags: [pip-vs-pipx, resources, til]
aliases: [today-i-learned, things-i-learned]
---


# 2024-06-10 - TIL - `pip` vs `pipx`

What is the difference between `pip` vs `pipx`? When should you use one or the other?


## `pip` Use Cases

- You need to install Python libraries to import into your project.
- You just want a general-purpose package manager for Python.
- You don't want to learn/manage multiple tools.


## `pipx` Use Cases

- You need to install and run Python command-line applications in isolated environments.
- You want to avoid conflicts between different projects' dependencies on the same system.
- You are just installing and running command-line applications and are not doing any Python development.


## Usage

```sh
$ tldr pip

pip

Python package manager.
Some subcommands such as "pip install" have their own usage documentation.
More information: <https://pip.pypa.io>.

- Install a package (see "pip install" for more install examples):
    pip install package

- Install a package to the user\'s directory instead of the system-wide default location:
    pip install --user package

- Upgrade a package:
    pip install --upgrade package

- Uninstall a package:
    pip uninstall package

- Save installed packages to file:
    pip freeze > requirements.txt

- Show installed package info:
    pip show package

- Install packages from a file:
    pip install --requirement requirements.txt


$ tldr pipx

pipx

Install and run Python applications in isolated environments.
More information: <https://github.com/pypa/pipx>.

- Run an app in a temporary virtual environment:
    pipx run pycowsay moo

- Install a package in a virtual environment and add entry points to path:
    pipx install package

- List installed packages:
    pipx list

- Run an app in a temporary virtual environment with a package name different from the executable:
    pipx run --spec httpx-cli httpx http://www.github.com

- Inject dependencies into an existing virtual environment:
    pipx inject package dependency1 dependency2 ...

- Install a package in a virtual environment with pip arguments:
    pipx install --pip-args='pip-args' package
```


## Use Cases

- Use `pip` for general-purpose package management and Python development.
- Use `pipx` for installing and running command-line applications in isolated environments.
- Use `pipx` over `pip` to avoid conflicts between different projects' dependencies on the same system.


## References

- [Explain `pip` vs `pipx`, which is better, and why](https://www.phind.com/search?cache=bthccd7i3i0w6kk04nl2i27u)


