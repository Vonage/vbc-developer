---
title: Stream audio into call leg
navigation_weight: 1
---

# Stream audio into call leg

This example shows you how to play a media file into an existing call. 

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. |
| call_id           | The call id for the call you would like to update |
| leg               | The leg id for the call you would like to update |
| stream            | set stream to `true` to start playing file. Sending `false` will stop playing the file. | 
| stream_url        | The full URL of the audio file you would like to send into the call. |

``` bash
curl -X PUT 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account/calls/$call_id/legs/$leg_id'
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "stream": "$stream",
   "stream_url":"$stream_url"
 }'
```
