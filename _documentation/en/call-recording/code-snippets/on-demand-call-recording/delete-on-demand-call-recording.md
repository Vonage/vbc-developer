---
title: Delete on-demand call recording
navigation_weight: 1
---

# Delete on-demand call recording

Delete a single on-demand call recording for an account user

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| user_id | The Vonage Business Communications user ID. You can use 'self' to refer to the authenticated user. |
| recording_id | The recording ID |

``` bash
curl --location --request DELETE 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/users/$user_id/call_recordings/$recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
