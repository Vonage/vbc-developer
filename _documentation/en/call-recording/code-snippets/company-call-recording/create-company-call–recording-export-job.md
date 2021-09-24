---
title: Create a company call recording export job
navigation_weight: 1
---

# Create a company call recording export job

This example shows you how to create a company call recording export job for an account.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| call_direction           | Filter recordings by call direction. Must be one of: `INBOUND` `OUTBOUND` or `INTRA_PBX` |

There are many more filters that can be applied when generating an company call recording job. Please take a look at the [Create a company call recording export job](/api/call-recording#createCCRExportJob) spec.


``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/company_call_recordings/export' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{
    "call_direction":$call_direction
}'
```
