---
title: Get list of legs for a given call
navigation_weight: 1
---

# Get list of legs for a given call

This example shows you how to make retrieve details on a call leg. This will return the call direction (inbound or outbound) status, and more.

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. |
| leg_id | The leg id for the leg you would like to get | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$leg_id/legs' \
--header 'Authorization: Bearer $bearer_token'
```
