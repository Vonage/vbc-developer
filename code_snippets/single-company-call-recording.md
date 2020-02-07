# Get single company call recording
This example shows you how to get a single company call recording for an account
First, subscribe to the CallRecording API suite. See the Getting Started section for more information on how to subscribe to these API's.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| account_id | The Vonage Business Cloud account ID. You can use 'self' to refer to the authenticated user's account. |
| recording_id | The recording ID | 
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/company_call_recordings/recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```