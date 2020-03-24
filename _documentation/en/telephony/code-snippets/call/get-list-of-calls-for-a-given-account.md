---
title: Get list of calls for a given account
navigation_weight: 1
---

# Get list of calls for a given account

This example shows you how to make retrieve all calls on a account. This will return the call legs, direction (inbound or outbound) and status for every call.

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls' \
--header 'Authorization: Bearer $bearer_token'
```
