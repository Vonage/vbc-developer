---
title: Get events count
---

# Get events count

This example demonstrates how to count events.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/vis/v1/self/events/count' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```
