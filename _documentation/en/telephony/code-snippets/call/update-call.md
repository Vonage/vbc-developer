---
title: Update an existing call
navigation_weight: 1
---

# Update an existing call

This example shows you how to update an existing call on a account. This will return the call legs, direction (inbound or outbound) and status for every call.

Replace the following placeholder values in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |
| call_id | The call id for the call you would like to update |
| from_destination | NEED DOCS |
| from_device | NEED DOCS |
| state | This will change the state of the call. Set to `active` to answer a  call. To transfer a call, `state` should not be specified. Set to `parked` to park a call. |
| to_destination | NEED DOCS |
| to_device | NEED DOCS |

``` bash
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' -d {
   "from": {
     "destination": "$from_destination",
     "type": "$from_device"
   },
   "state": "$state",
   "to": {
     "destination": "$to_destination",
     "type": "$to_device"
   } 
 } 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls/$call_id'
```
