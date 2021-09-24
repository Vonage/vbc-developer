---
title: Get call recording export jobs
navigation_weight: 1
---

# Get call recording export jobs

This example demonstrates how to create a call recording job for an account user.

Export jobs allows users to download recordings in bulk based on search criteria. Export jobs are initiated from the corresponding company and on-demand call recording export endpoints.

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| user_id           | The Vonage Business Communications user ID. You can use 'self' to refer to the authenticated user. | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/users/$user_id/call_recordings/jobs' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
