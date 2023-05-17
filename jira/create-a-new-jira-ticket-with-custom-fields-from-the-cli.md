# Create a New Jira Ticket With Custom Fields From the CLI

How to create a new Jira ticket using only the CLI with [ankitpokhrel/jira-cli](https://github.com/ankitpokhrel/jira-cli).

## Required Fields

**type**: Jira Issue Type - string - "Task"
**project**: Project Key - string - "PROJKEY"
**summary**: Ticket summary/title - string - "New Jira Ticket"
**body**: Ticket description/body - string - "New Jira Ticket Description"
**priority**: Ticket priority - string - "High"
**reporter**: Username/Email of reporter - string - "USER"
**assignee**: Username/Email of assignee - string - "USER"
**label**: 1x label is 1 array value - array-value - one-label
**label**: 1x label is 1 array value - array-value - two-label
**label**: 1x label is 1 array value - array-value - three-label
**parent**: Parent ticket ID. Useful for setting Epic ID - string - "PROJKEY-###"
**custom story-points**: Story Points - number/int - 3
**custom acceptance-criteria**: Acceptance Criteria - string - "Acceptance Criteria"
**custom team**: Team ID - string - "###"
**custom sprint**: Sprint ID - string - "#####"

## Command

```bash
$ jira issue create \
  --type="Task" \
  --project="PROJKEY" \
  --summary="New Jira Ticket" \
  --body="New Jira Ticket Description" \
  --priority="High" \
  --reporter="USER" \
  --assignee="USER" \
  --label=one-label \
  --label=two-label \
  --label=three-label \
  --parent="PROJKEY-000" \
  --custom story-points=3 \
  --custom acceptance-criteria="Acceptance Criteria" \
  --custom team="000" \
  --custom sprint="00000"
```

## Use Cases

Create new Jira tickets using 100% CLI only.
No more context switching or needing to break your deep focus/flow state.
CLI based ticket creation process means we can automate!

## References

- [How can I set custom fields on issue creation? · ankitpokhrel/jira-cli · Discussion #346](https://github.com/ankitpokhrel/jira-cli/discussions/346)

