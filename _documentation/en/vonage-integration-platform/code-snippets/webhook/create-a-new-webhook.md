---
title: Create a new webhook
---

# Create a new webhook

This example shows you how to create a new webhook subscription

Replace the following placeholder value in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| url               | Destination URL for events |
| events            | Array of events to subscribe to |
| signingAlgo       | Signing algorithm for the webhook |
| signingKey        | Signing key for the webhook |
| metadataPolicy    | Metadata policy for the webhook |

``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
--data-raw '{  
   "url": "$url",
   "events": "$events",
   "signingAlgo": "$signingAlgo",
   "signingKey": "$signingKey",
   "metadataPolicy": "$metadataPolicy"
 }'
```
