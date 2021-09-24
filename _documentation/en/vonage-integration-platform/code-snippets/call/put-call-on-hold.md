---
title: Put call on hold
---

# Put call on hold

This example demonstrates how to put a call on hold.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| id                | Unique identifier of the call |

``` bash
curl --location --request PUT 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls/$id/hold' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```