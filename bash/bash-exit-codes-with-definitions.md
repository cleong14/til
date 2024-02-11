# 2024-02-10 - TIL - Bash Exit Codes With Definitions

A list of common Bash exit codes along with their definitions.


## Bash Exit Codes With Definitions

```sh
# Successful termination
0    # General success status

# Error codes
1    # Catchall for general errors
2    # Misuse of shell builtins (according to Bash documentation)
6    # No such device or address
124  # Command timed out
125  # Command did not complete successfully
126  # Command found but cannot be invoked (not executable)
127  # Command not found (possible issue with PATH or typo)
128  # Invalid argument to exit
130  # Terminated by Control-C
137  # Killed by SIGKILL
141  # Pipe error
143  # Killed by signal  15
255  # Exit status out of range
```


## Use Cases

- Bash exit codes cheatsheet/reference with definitions


## References

- [Can You Provide a List of Bash Exit Codes and Their Definitions?](https://www.phind.com/search?cache=xqgtckqcw5gidpy0fo7idd6z)

