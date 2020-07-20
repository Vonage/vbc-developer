---
title: Send call to voicemail
---

# Send call to voicemail

This example demonstrates how to send a call to voicemail.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| id                | Unique identifier of the call |

``` bash
curl --location --request PUT 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls/$id/vmtransfer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```