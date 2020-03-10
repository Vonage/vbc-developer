---
title: Get account users data by account ID
navigation_weight: 1
---

# Get account users data by account ID

This example shows you how to list all users on a given account. It will include the user's name, email, contact information and more.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |


``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/users' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
