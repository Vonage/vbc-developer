---
title: Unhold a call
---

# Unhold a call

This example shows you how to unhold a call

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| id                | Unique identifier of the call |

``` bash
curl --location --request DELETE 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls/$id/hold' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```