# May 04, 2023 TIL

## Remove Sensitive Data from a Repository Using `git filter-repo`

If you commit sensitive data, such as a password or SSH key into a Git repository, you can remove it from the history. To entirely remove unwanted files from a repository's history you can use either the git filter-repo tool or the BFG Repo-Cleaner open source tool.

### [Purging a file from your repository's history](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository#purging-a-file-from-your-repositorys-history)

#### Using `git filter-repo`

1. Install `git filter-repo`

```bash
$ brew install git-filter-repo
```

2. Clone a _FRESH COPY_ of the repository

```bash
$ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
> Initialized empty Git repository in /Users/YOUR-FILE-PATH/YOUR-REPOSITORY/.git/
> remote: Counting objects: 1301, done.
> remote: Compressing objects: 100% (769/769), done.
> remote: Total 1301 (delta 724), reused 910 (delta 522)
> Receiving objects: 100% (1301/1301), 164.39 KiB, done.
> Resolving deltas: 100% (724/724), done.
```

3. Navigate into the repository's working directory

```bash
$ cd YOUR-REPOSITORY
```

4. Run the following command, replacing `PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA` with the _path to the file you want to remove, not just its filename_

```bash
# analyze and output repo stats
$ git filter-repo --analyze

# run command dry-run to test changes
$ git filter-repo --invert-paths --path PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA --dry-run

$ git filter-repo --invert-paths --path PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA
  Parsed 197 commits
  New history written in 0.11 seconds; now repacking/cleaning...
  Repacking your repo and cleaning out old unneeded objects
  Enumerating objects: 210, done.
  Counting objects: 100% (210/210), done.
  Delta compression using up to 12 threads
  Compressing objects: 100% (127/127), done.
  Writing objects: 100% (210/210), done.
  Building bitmaps: 100% (48/48), done.
  Total 210 (delta 98), reused 144 (delta 75), pack-reused 0
  Completely finished after 0.64 seconds.
```

5. Add your file with sensitive data to `.gitignore` to ensure that you don't accidentally commit it again

```bash
$ echo "YOUR-FILE-WITH-SENSITIVE-DATA" >> .gitignore
$ git add .gitignore
$ git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
> [main 051452f] Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore
>  1 files changed, 1 insertions(+), 0 deletions(-)
```

6. Double-check that you've removed everything you wanted to from your repository's history, and that all of your branches are checked out
7. Once you're happy with the state of your repository, force-push your local changes to overwrite your repository

```bash
$ git push origin --force --all
> Counting objects: 1074, done.
> Delta compression using 2 threads.
> Compressing objects: 100% (677/677), done.
> Writing objects: 100% (1058/1058), 148.85 KiB, done.
> Total 1058 (delta 590), reused 602 (delta 378)
> To https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
>  + 48dc599...051452f main -> main (forced update)
```

8. In order to remove the sensitive file from your tagged releases, you'll also need to force-push against your Git
   tags

```bash
$ git push origin --force --tags
> Counting objects: 321, done.
> Delta compression using up to 8 threads.
> Compressing objects: 100% (166/166), done.
> Writing objects: 100% (321/321), 331.74 KiB | 0 bytes/s, done.
> Total 321 (delta 124), reused 269 (delta 108)
> To https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
>  + 48dc599...051452f main -> main (forced update)
```

