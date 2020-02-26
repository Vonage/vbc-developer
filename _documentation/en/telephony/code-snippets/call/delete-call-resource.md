---
title: Delete a call resource
navigation_weight: 1
---

# Delete a call resource

This example shows you how to delete a call. If the call is active, this SHOULD hang up the call. #TODO

Replace the following placeholder values in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Cloud account ID. |
| call_id | The call id for the call you would like to delete| 

``` bash
curl --location --request DELETE 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$call_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```

