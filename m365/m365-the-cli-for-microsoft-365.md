# January 03, 2024 TIL - `m365` - The CLI for Microsoft 365!

Using the CLI for Microsoft 365, you can manage your Microsoft 365 tenant and
SharePoint Framework projects on any platform. No matter if you are on Windows,
macOS or Linux, using Bash, Cmder or PowerShell, using the CLI for Microsoft 365
you can configure Microsoft 365, manage SharePoint Framework projects and build
automation scripts.


## Features

-   Run on any OS
    -   Linux
    -   MacOS
    -   Windows
-   Run on any shell
    -   Azure Cloud Shell
    -   bash
    -   cmder
    -   PowerShell
    -   zsh
-   Unified login
    -   Access all your Microsoft 365 workloads
-   Supported workloads
    -   Azure Active Directory
    -   Bookings
    -   Microsoft Teams
    -   Microsoft To Do
    -   OneDrive
    -   OneNote
    -   Outlook
    -   Planner
    -   Power Automate
    -   Power Apps
    -   Power Platform
    -   Purview
    -   Skype for Business
    -   SharePoint Online
    -   To Do
    -   Yammer
-   Supported authentication methods
    -   Azure Managed Identity
    -   Certificate
    -   Client Secret
    -   Device Code
    -   Username and Password
-   Manage your SharePoint Framework projects
    -   Upgrade your projects
    -   Check your environment compatibility


## Usage

```bash
### install/upgrade/login
#
# install
npm install -g @pnp/cli-microsoft365
#
# upgrade
npm upgrade -g @pnp/cli-microsoft365
#
# login - Use the `login` command to start the Device Code login flow to authenticate with your Microsoft 365 tenant.
m365 login


### outlook message list - https://pnp.github.io/cli-microsoft365/cmd/outlook/message/message-list
#
# List all messages in the folder with the specified name.
m365 outlook message list --folderName Archive
#
# List all messages in the folder with the specified ID.
m365 outlook message list --folderId AAMkAGVmMDEzMTM4LTZmYWUtNDdkNC1hMDZiLTU1OGY5OTZhYmY4OAAuAAAAAAAiQ8W967B7TKBjgx9rVEURAQAiIsqMbYjsT5e-T7KzowPTAAAAAAFNAAA=
#
# List all messages in the folder with the specified well-known name.
m365 outlook message list --folderName inbox


### outlook mail send - https://pnp.github.io/cli-microsoft365/cmd/outlook/mail/mail-send
#
# Send a text email to the specified email address
m365 outlook mail send --to chris@contoso.com --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the team site"
#
# Send an HTML email to the specified email addresses
m365 outlook mail send --to "chris@contoso.com,brian@contoso.com" --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the <a href='https://contoso.sharepoint.com/sites/marketing'>team site</a>" --bodyContentType HTML
#
# Send an HTML email to the specified email address loading email contents from a file on disk
m365 outlook mail send --to chris@contoso.com --subject "DG2000 Data Sheets" --bodyContents @email.html --bodyContentType HTML
#
# Send a text email to the specified email address. Don't store the email in sent items
m365 outlook mail send --to chris@contoso.com --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the team site" --saveToSentItems false
#
# Send an email on behalf of a shared mailbox using the signed in user
m365 outlook mail send --to chris@contoso.com --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the team site" --mailbox sales@contoso.com
#
# Send an email as another user
m365 outlook mail send --to chris@contoso.com --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the team site" --sender svc_project@contoso.com
#
# Send an email as another user, on behalf of a shared mailbox
m365 outlook mail send --to chris@contoso.com --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the team site" --sender svc_project@contoso.com --mailbox sales@contoso.com
#
# Send an email with cc and bcc recipients marked as important
m365 outlook mail send --to chris@contoso.com --cc claire@contoso.com --bcc randy@contoso.com --subject "DG2000 Data Sheets" --bodyContents "The latest data sheets are in the team site" --importance high
#
# Send an email with multiple attachments
m365 outlook mail send --to chris@contoso.com --subject "Monthly reports" --bodyContents "Here are the reports of this month." --attachment "C:/Reports/File1.jpg" --attachment "C:/Reports/File2.docx" --attachment "C:/Reports/File3.xlsx"
```


## Use Cases

- Reduce the amount of context switching when working with Microsoft products
- Manage your Microsoft 365 workloads from the terminal


## References

- [CLI for Microsoft 365 - CLI for Microsoft 365](https://pnp.github.io/cli-microsoft365/)
- [pnp/cli-microsoft365: Manage Microsoft 365 and SharePoint Framework projects on any platform](https://github.com/pnp/cli-microsoft365)

