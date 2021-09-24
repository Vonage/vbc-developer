---
title: Get location data by account ID and location ID
navigation_weight: 1
---

# Get location data by account ID and location ID

This example demonstrates how to get the physical location of the account using the `account_id` and `location_id`.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |
| location_id       | The location Id. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/locations/$location_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
