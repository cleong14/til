# September 26, 2023 TIL - How to Use a Multiline String Command Argument Input & Preserve the String's Newlines in the Output Using "Here Strings" and/or "Here Documents"

Using "Here Strings"/"Here Documents", we can use multiline strings as command argument inputs while preserving the newlines in the multiline string command output.

## Example

Using [ankitpokhrel/jira-cli](https://github.com/ankitpokhrel/jira-cli), add a multiline string comment to a Jira Issue & preserve any newlines.

Note: [ankitpokhrel/jira-cli](https://github.com/ankitpokhrel/jira-cli) supports both [Github-flavored](https://github.github.com/gfm/) and [Jira-flavored](https://jira.atlassian.com/secure/WikiRendererHelpAction.jspa?section=all) markdown for writing comments.

```bash
# "Here String" Method
$ jira issue comment add --no-input ISSUE-1 "
# GFM Flavor H1

## GFM Flavor H2

- UL List Item 1
- UL List Item 2"

# "Here Document" Method
$ jira issue comment add --no-input ISSUE-1 --template - << EOF
# GFM Flavor H1

## GFM Flavor H2

- UL List Item 1
- UL List Item 2
EOF
```

## Use Cases

- Use "Here Strings"/"Here Documents" to add multiline strings as command argument inputs while preserving the newlines in the multiline string command output
- Add multiline string comments to Jira Issues from the CLI using [ankitpokhrel/jira-cli](https://github.com/ankitpokhrel/jira-cli) + "Here Strings"/"Here Documents"

## References

- [Here Document And Here String in Bash on Linux](https://www.tutorialspoint.com/here-document-and-here-string-in-bash-on-linux)
- [ankitpokhrel/jira-cli: 🔥 Feature-rich interactive Jira command line.](https://github.com/ankitpokhrel/jira-cli)

