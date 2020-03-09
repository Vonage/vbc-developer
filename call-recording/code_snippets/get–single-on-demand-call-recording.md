# Get single on-demand call recording
Get a single on-demand call recording for an account user

Replace the following placeholder values in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |
| user_id | The Vonage Business Communications user ID. You can use 'self' to refer to the authenticated user. |
| recording_id | The recording ID |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/:account_id/users/:user_id/call_recordings/:recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
