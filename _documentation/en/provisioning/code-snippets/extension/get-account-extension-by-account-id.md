---
title: Get account extensions data by account ID
navigation_weight: 1
---

# Get account extensions data by account ID

This example demonstrates how to get a list of account extensions by the `account_id`. For each extension, you will receive information about the user that is tied to the extension, as well as the `external_id` which represents the extension ID, `caller_id` and any headsets that are connected to the extension.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/extensions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
