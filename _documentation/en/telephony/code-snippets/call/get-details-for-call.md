---
title: Get details for a specific call
navigation_weight: 1
---

# Get details for a specific call

This example shows you how to make retrieve details on a call. This will return the call legs, direction (inbound or outbound) and status.

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |
| call_id.          | The call ID for the call you would like to delete | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$call_id' \
--header 'Authorization: Bearer $bearer_token'
```
