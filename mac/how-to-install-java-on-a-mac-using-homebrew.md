# June 30, 2023 TIL - How to Install Java on a Mac Using Homebrew

To install Java on a Mac using Homebrew:

```bash
## install java using homebrew
$ brew install java

## you also need to create a symlink for the system Java wrappers to find this JDK:
# on apple silicon macs
$ sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk

## verify java installed successfully on your mac
$ java --version
```

## Use Cases

- Install Homebrew managed version of Java on your mac
- Resolve Java related `:checkhealth` issues

## References

- [macos - How to brew install java? - Stack Overflow](https://stackoverflow.com/questions/65601196/how-to-brew-install-java/65601197#65601197)

