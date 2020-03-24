---
title: Get account info
---

# Get account info

This example shows you how to get detailed information about the authenticated account

Replace the following placeholder value in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |


``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/vis/v1/self/account' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
