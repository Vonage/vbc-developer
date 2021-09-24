---
title: List active calls
---

# List active calls

This example demonstrates how to list currently active calls.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```
