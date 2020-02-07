# Delete company call recording
This example shows you how to delete a single company call recording for an account

Replace the following placeholder values in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Cloud account ID. You can use 'self' to refer to the authenticated user's account. |
| recording_id | The recording ID. | 

``` bash
curl --location --request DELETE 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/company_call_recordings/$recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
