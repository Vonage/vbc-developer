---
title: Transfer a call
---

# Transfer a call

This example demonstrates how to transfer a call.

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| id                | Unique identifier of the call |
| phoneNumber       | Phone number to transfer to |

``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/vis/v1/self/calls/:id/transfer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "phoneNumber": "$phoneNumber" 
 }'
```
