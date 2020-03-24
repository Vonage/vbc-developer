---
title: Send DTMF into existing call
navigation_weight: 1
---

# Send DTMF into existing call

This example shows you how to send a DTMF into an existing call. 

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. |
| call_id | The call id for the call you would like to update |
| leg | The leg id for the call you would like to update |

| dtmf | The DTMF code you would like to send into the call. |


``` bash
curl -X PUT 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account/calls/$call_id/legs/$leg_id'
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "dtmf": "$dtmf"
 }'
```
