---
title: Delete a call leg
navigation_weight: 1
---

# Delete a call leg

This example shows you how to delete a call leg. If the call is active, this SHOULD hang up the call. #TODO

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |
| call_id           | The call id for the call |
| leg_id            | The call leg id you want to remove |  

``` bash
curl --location --request DELETE 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$call_id/legs/$leg_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```

