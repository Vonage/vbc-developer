# Download
This example shows you how to download a call recording audio file

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| recording_id | TThe recording ID |


``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/v1/api/audio/recording/$recording_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
