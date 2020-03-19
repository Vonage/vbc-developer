---
title: Get location data by account ID and location ID
navigation_weight: 1
---

# Get location data by account ID and location ID

This example shows you how to get the physical location of the account, using the account id and location id.

Replace the following placeholder value in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |
| location_id | The location Id. |


``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/locations/$location_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
