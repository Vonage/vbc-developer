---
title: Place a call
---

# Place a call

This example demonstrates how to place a call.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-an-access-token) |
| phoneNumber       | Phone number to call |

``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "phoneNumber": "$phoneNumber" 
 }'
```
