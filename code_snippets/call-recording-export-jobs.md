# Get call recording export jobs
This example shows you how to create a call recording job for an account user. 
Export jobs let users download recordings in bulk based on search criteria. 
Export jobs are initiated from the corresponding company and on-demand call recording export endpoints.

First, subscribe to the CallRecording API suite. See the Getting Started section for more information on how to subscribe to these API's.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| account_id | The Vonage Business Cloud account ID. You can use 'self' to refer to the authenticated user's account. |
| user_id | The Vonage Business Cloud user ID. You can use 'self' to refer to the authenticated user. | 
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/api/accounts/$account_id/users/$user_id/call_recordings/jobs' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
