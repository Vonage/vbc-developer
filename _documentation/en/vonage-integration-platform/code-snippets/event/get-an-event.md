---
title: Get an event
---

# Get an event

This example demonstrates how to get details on an event.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| id                | Unique identifier of the event |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/vis/v1/self/events/:id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```
