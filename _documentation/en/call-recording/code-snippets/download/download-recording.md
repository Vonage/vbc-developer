---
title: Download recording
navigation_weight: 1
---

# Download recording

This example demonstrates how to download a call recording audio file.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| recording_id      | The recording ID |


``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/v1/api/audio/recording/$recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
