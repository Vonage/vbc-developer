---
title: Get details for a specific call leg
navigation_weight: 1
---

# Get details for a specific call leg

This example shows you how to make retrieve details on a call leg.

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. |
| call_id | The call id for the call  | 
| leg_id | The leg id for the call you would like to retrieve | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$call_id/legs/$leg_id' \
--header 'Authorization: Bearer $bearer_token'
```
