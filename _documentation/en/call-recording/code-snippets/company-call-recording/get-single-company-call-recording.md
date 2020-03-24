---
title: Get single company call recording
navigation_weight: 1
---

# Get single company call recording
This example shows you how to get a single company call recording for an account

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| recording_id      | The recording ID | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/company_call_recordings/$recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
