---
title: Create an on-demand call recording export job
navigation_weight: 1
---

# Create an on-demand call recording export job

Create an on-demand call recording export job for an account user

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| user_id           | The Vonage Business Communications user ID. You can use 'self' to refer to the authenticated user. |

``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/users/$user_id/call_recordings/export' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
