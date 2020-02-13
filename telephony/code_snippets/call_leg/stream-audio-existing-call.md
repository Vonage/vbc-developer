# Stream audio into call leg

This example shows you how to play a media file into an existing call. 

Replace the following placeholder values in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Cloud account ID. |
| call_id | The call id for the call you would like to update |
| leg | The leg id for the call you would like to update |
| stream | set stream to `true` to start playing file. Sending `false` will stop playing the file. | 
| stream_url | The full URL of the audio file you would like to send into the call. |


``` bash
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' -d {
   "stream": "$stream",
   "stream_url":"$stream_url"
 } 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account/calls/$call_id/legs/$leg_id'
```
