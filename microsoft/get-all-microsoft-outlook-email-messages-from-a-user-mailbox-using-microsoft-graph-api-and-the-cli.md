# 2024-01-11 TIL - Get All Microsoft Outlook Email Messages From a User Mailbox Using Microsoft Graph API and the CLI

How to get all Microsoft Outlook email messages from a user's mailbox using Microsoft Graph API and the CLI.


## Usage

```http
# Microsoft Graph API: List Messages in Folder
#
# https://learn.microsoft.com/en-us/graph/api/mailfolder-list-messages
#
# Get all messages in a target user's mailbox
#
# Request Headers:
#
# Authorization: Bearer <ACCESS_TOKEN>
#
# Request Body:
#
# None
#
# Response:
#
# If successful, this method returns a `200` OK response code and collection of `Message` objects in the response body.
#
# Example:
#
# Request:
#
GET https://graph.microsoft.com/v1.0/me/mailFolders/<parentFolderId>/messages
Authorization: Bearer <ACCESS_TOKEN>
#
# Response:
#
HTTP/1.1 200 OK
Content-type: application/json

{
  "value": [
    {
      "receivedDateTime": "2018-02-13T03:53:55Z",
      "sentDateTime": "2018-02-13T03:53:55Z",
      "hasAttachments": true,
      "subject": "MyAnalytics | Your past week",
      "body": {
        "contentType": "html",
        "content": "<html lang=\"en\">\r\n<head></head>\r\n<body> </body>\r\n</html>\r\n"
      },
      "bodyPreview": "February 4-10, 2018\r\n\r\n\r\nHi Megan Bowen,\r\n\r\nWe've got your highlights from last week\r\n\r\n\r\n\r\nYour time\r\n\r\n\r\nEmail hours\r\n\r\n\r\n\r\n\r\n0 hrs\r\n\r\n\r\n\r\nMeeting hours\r\n\r\n\r\n\r\n\r\n12 hrs\r\n\r\n\r\n\r\n\r\nFocus hours\r\n\r\n\r\n\r\n\r\n30 hrs\r\n\r\n\r\n\r\n\r\n\r\nGoals keep you motivated. Set them"
    },
    {
      "id": "<id>",
      "createdDateTime": "1970-01-01T00:00:00Z",
      "lastModifiedDateTime": "1970-01-01T00:00:00Z",
      "changeKey": "<changeKey>",
      "categories": [],
      "receivedDateTime": "1970-01-01T00:00:00Z",
      "sentDateTime": "1970-01-01T00:00:00Z",
      "hasAttachments": false,
      "internetMessageId": "<internetMessageId>",
      "subject": "<subject>",
      "bodyPreview": "<bodyPreview>",
      "importance": "<importance>",
      "parentFolderId": "<parentFolderId>",
      "conversationId": "<conversationId>",
      "conversationIndex": "<conversationIndex>",
      "isDeliveryReceiptRequested": null,
      "isReadReceiptRequested": false,
      "isRead": false,
      "isDraft": false,
      "webLink": "<webLink>",
      "inferenceClassification": "<inferenceClassification>",
      "body": {
        "contentType": "<contentType>",
        "content": "<content>"
      },
      "sender": {
        "emailAddress": {
          "name": "<name>",
          "address": "<address>"
        }
      },
      "from": {
        "emailAddress": {
          "name": "<name>",
          "address": "<address>"
        }
      },
      "toRecipients": [
        {
          "emailAddress": {
            "name": "<name>",
            "address": "<address>"
          }
        }
      ],
      "ccRecipients": [
        {
          "emailAddress": {
            "name": "<name>",
            "address": "<address>"
          }
        }
      ],
      "bccRecipients": [],
      "replyTo": [],
      "flag": {
        "flagStatus": "<flagStatus>"
      }
    },
  ]
}
```


## Use Cases

- Get all Microsoft Outlook email messages from a user's mailbox using Microsoft Graph API and the CLI
- Avoid the need for context switching just to check your email


## References

- [List messages - Microsoft Graph v1.0 | Microsoft Learn](https://learn.microsoft.com/en-us/graph/api/mailfolder-list-messages)

