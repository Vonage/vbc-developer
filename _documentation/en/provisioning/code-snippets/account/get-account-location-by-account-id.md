---
title: Get account locations data by account ID
navigation_weight: 1
---

# Get account locations data by account ID

This example shows you how to get the physical location using the account id. You can use this to retrieve details of the account, including the name of the account, the status, and its address.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. |


``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/locations' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
