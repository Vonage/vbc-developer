---
title: Create a company call recording export job
navigation_weight: 1
---

# Create a company call recording export job

This example shows you how to create a company call recording export job for an account.

Replace the following placeholder value in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |

``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/company_call_recordings/export' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
