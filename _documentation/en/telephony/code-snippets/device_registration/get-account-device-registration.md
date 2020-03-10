---
title: Get account device's registration info
navigation_weight: 1
---

# Get account device's registration info

This example shows you how return a list of devices associated with the account id. 

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/registration/accounts/$account_id/devices' \
--header 'Authorization: Bearer $bearer_token'
```
