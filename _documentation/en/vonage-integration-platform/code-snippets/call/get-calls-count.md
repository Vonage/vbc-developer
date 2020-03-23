---
title: Get calls count
---

# Get calls count

This example shows you how to count active calls

Replace the following placeholder value in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |


``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls/count' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token'
```
