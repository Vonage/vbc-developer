---
title: Get account locations data by account ID
navigation_weight: 1
---

# Get account locations data by account ID

This example shows you how to get the physical location using the account id. You can use this to retrieve details of the account, including the name of the account, the status, and its address.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Cloud account ID. |


``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/locations' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
