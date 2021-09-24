---
title: Get webhook details
---

# Get webhook details

This example demonstrates how to get details on a webhook.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| id                | Unique identifier of the webhook |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/$id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```
