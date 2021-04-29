---
title: Get extension data by account ID and extension ID
navigation_weight: 1
---

# Get extension data by account ID and extension ID

This example demonstrates how to get details of the extension. This will include the extension's number, the `caller_id` and the headsets associated with this extension. 

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. |
| external_id      | The extension ID. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/extensions/$external_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
