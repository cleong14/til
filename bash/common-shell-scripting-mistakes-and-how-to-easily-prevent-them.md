# 2024-02-04 - TIL - Common Shell Scripting Mistakes and How to Easily Prevent Them

Common shell scripting mistakes and how to easily prevent them with stricter error handling.


## Usage

```sh
### Add these options to the top of every shell script
# stop scripts on errors - causes the script to exit immediately if any command exits with a non-zero status
set -e # or `set -o errexit`
# stop script if undefined var - causes the script to exit if it tries to use a variable that has not been set
set -u # or `set -o nounset`
# stop script if there's a pipe failure - causes the script to exit if any command in a pipeline fails, rather than continuing with the next command in the pipeline
set -o pipefail
# bonus: set all 3 as a one-liner
set -euo pipefail

### Other useful options
# prevents redirection from overwriting existing files; if a redirection would cause a file to be overwritten, the shell will not perform the redirection
set -C # or `set -o noclobber`

### Useful shell options
# causes a non-matching glob pattern to cause an error, rather than being treated as a literal string
shopt -s failglob
# causes subshells and functions to inherit the errexit option, so they will also exit immediately if any command exits with a non-zero status
shopt -s inherit_errexit

### Set all options and shell options above in a shell script
set -Ceuo pipefail # longhand: `set -o errexit -o noclobber -o nounset -o pipefail`
shopt -s failglob inherit_errexit
### Set all options and shell options above in a shell script
```


## Use Cases

- Prevent common shell scripting mistakes and avoid common pitfalls using stricter error handling


## References

- [Common shell script mistakes (2008) | Hacker News](https://news.ycombinator.com/item?id=29470863)
- [BashPitfalls - Greg's Wiki](https://mywiki.wooledge.org/BashPitfalls)

