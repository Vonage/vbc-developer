---
title: Get account data by ID
navigation_weight: 1
---

# Get account data by ID

This example demonstrates how to get the account information by `account_id`. You can use this to retrieve details on the account, including the name of the account, the status, and its address.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
