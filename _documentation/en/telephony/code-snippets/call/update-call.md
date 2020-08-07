---
title: Update an existing call
navigation_weight: 1
---

# Update an existing call

This example shows you how to update an existing call on a account. This will return the call legs, direction (inbound or outbound) and status for every call.

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id        | The Vonage Business Communications account ID. |
| call_id           | The call id for the call you would like to update. |
| from_type         | The type of destination. Can be one of three values `extension` , `device`, or `pstn`. |
| from_destination  | The from destination. If `from_type` is `extension`, then the `from_destination` must be an extension. If `from_type` is `device`, then the `from_destination` must be a valid device ID. If `from_type` is `pstn`, then the `from_destination` must be a valid phone number. | 
| to_type           | The type of destination. Can be one of three values `extension` , `device`, or `pstn`. |
| to_destination    | The to destination. If `from_type` is `extension`, then the `to_destination` must be an extension. If `from_type` is `device`, then the `to_destination` must be a valid device ID. If `from_type` is `pstn`, then the `to_destination` must be a valid phone number. |
| to_type           | Should be one of `click2dial`, `click2dialme`, `odr` or `default`. |
| state             | This will change the state of the call. Set to `active` to answer a  call. To transfer a call, `state` should not be specified. Set to `parked` to park a call. |

``` bash
curl -X PUT 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$call_id'
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "from": {
    "type": "$from_type",
     "destination": "$from_destination"
   },
   "state": "$state",
   "to": {
    "type": "$to_type",
     "destination": "$to_destination"
   } 
 } 
```
