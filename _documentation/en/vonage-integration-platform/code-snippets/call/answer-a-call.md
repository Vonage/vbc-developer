---
title: Answer a call
---

# Answer a call

This example demonstrates how to answer a call.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| id                | Unique identifier of the call |

``` bash
curl --location --request PUT 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls/$id/answer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```