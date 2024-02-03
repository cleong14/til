# 2024-02-02 - TIL - Use Git WIP Commits vs Git Stashes to Multitask Like a Pro

Git WIP commits help make the inevitable context switching in an Agile environment or when working on multiple projects at the same time much more manageable while ensuring you're not stuck with countless stale stashes that are bound to build up over time.


## Usage

```bash
# `gwip` - alias to stage everything and create a WIP commit in one go
alias gwip='git add -A; git rm $(git ls-files --deleted) 2> /dev/null; git commit --no-verify --no-gpg-sign --message "--wip-- [skip ci]"'

# `gunwip` to unwip (soft reset) the last WIP commit you’ve made
alias gunwip='git rev-list --max-count=1 --format="%s" HEAD | grep -q "\--wip--" && git reset HEAD~1'

# `gunwipall` - similar to `gunwip` but recursive; "Unwips" all recent `--wip--` commits not just the last one
function gunwipall() {
  local _commit=$(git log --grep='--wip--' --invert-grep --max-count=1 --format=format:%H)

  # Check if a commit without "--wip--" was found and it's not the same as HEAD
  if [[ "$_commit" != "$(git rev-parse HEAD)" ]]; then
    git reset $_commit || return 1
  fi
}
```


## Use Cases

- Relevant work is stored in the relevant branch
- WIP commits are gone when you delete the branch, so you don’t have a list of rotting old stashes.
- No copy-pasting of files like with apply
- Your work is saved on the cloud


## References

- [Multitask like a pro with the WIP commit | by Aziz Nal | Medium | ITNEXT](https://itnext.io/multitask-like-a-pro-with-the-wip-commit-2f4d40ca0192)

