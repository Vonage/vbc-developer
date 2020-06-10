---
title: Get user data by account ID and user ID
navigation_weight: 1
---

# Get user data by account ID and user ID

This example demonstrates how to get detailed information on a given user for an account.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. |
| user_id           | The Vonage Business Communications user ID. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/users/$user_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
