---
title: Create a new call
navigation_weight: 1
---

# Create a new call

This example shows you how to make a phone call. In order to make the call, you will need to have a physical phone or softphone.

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |
| from_type         | The type of destination. Can be one of two values `extension` , or `device` |
| from_destination  | The destination. If  `from_type` is `extension`, then the `from_destination` must be an extension. If `from_type` is `device`, then the `from_destination` must be a valid device ID. | 
| to_type           | The type of destination. Can be one of three values `extension` , `device`, or `pstn` |
| to_destination    | The destination. If  `from_type` is `extension`, then the `to_destination` must be an extension. If `from_type` is `device`, then the `to_destination` must be a valid device ID. If `from_type` is `pstn`, then the `to_destination` must be a valid phone number. |
| type           | Should be one of `click2dial`, `click2dialme`, `odr` or `default` |

``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "from": {  
      "type": "$from_type",
     "destination": "$from_destination"
   },  
   "to": {  
      "type": "$to_type",
     "destination": "$to_destination"
   },  
   "type": "$type"  
 }'
```
