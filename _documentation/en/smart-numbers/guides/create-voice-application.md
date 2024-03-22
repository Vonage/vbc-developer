---
title: Create a Vonage API Platform Voice application
description: The application stores security and configuration information for your interaction with the Voice API.
navigation_weight: 2
---

# Create a Vonage API Platform Application

Every Smart Numbers application that you build must be associated with a Vonage API Platform Voice Application.

> **Note**: To avoid confusion, `Application` here refers to the Vonage API Platform Application. The application you are building will be referred to as "application".

A Vonage API Platform Application stores configuration information such as details of the Smart Numbers and webhook callback URLs that your application uses. To make your VBC Smart Number calls zero-rated in Vonage API Platform, you must create an Application with the `vbc` and `voice` capabilities, using the [Vonage API Platform Application API](https://developer.vonage.com/en/api/application.v2).

## Using the Application API

To create a Vonage API Platform Application for working with Smart Numbers, issue the `curl` command shown below, replacing `VONAGE_API_KEY` and `VONAGE_API_SECRET` with your Vonage API Platform API key and secret respectively. You can find this information in the [Vonage API Platform Developer dashboard](https://dashboard.nexmo.com/getting-started-guide).

The two URLs you provide refer to the webhook endpoints that your application will expose to Vonage API Platform's servers:

* The first is the webhook to which Vonage API Platform's APIs will make a request when a call is received on your Smart Number.
* The second is where Vonage API Platform's APIs will post details about events that your application might be interested in - such as a call being answered or terminated.


```sh
curl -X POST \
  https://api.nexmo.com/v2/applications \
  -H 'Authorization: Basic Base64($VONAGE_API_KEY:$VONAGE_API_SECRET)' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "My VAPI VBC Application",
    "capabilities": {
      "vbc": {},
      "voice": {
        "webhooks": {
          "answer_url": {
            "address": "https://example.com/webhooks/answer",
            "http_method": "POST"
          },
          "event_url": {
            "address": "https://example.com/webhooks/event",
            "http_method": "POST"
          }
        }
      }
	  }
  }'
```

The response is a JSON object containing the Vonage API Platform Application `id` that you will use to interact with the Vonage API Platform Voice API.

```json
{
  "id": "27aa0583-7246-4822-aabb-17b03c25d52e",
  "name": "My VAPI VBC Application",
  "keys": {
    "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvAIBADANBgkq...
    -----END PRIVATE KEY-----\n",
    "public_key": "-----BEGIN PUBLIC_KEY-----\nMIIBIjANBgkqh...
    -----END PUBLIC KEY-----\n"
  },
  "capabilities": {
    "voice": {
      "webhooks": {
        "event_url": {
            "address": "https://example.com/webhooks/event",
            "http_method": "POST"
        },
        "answer_url": {
            "address": "https://example.com/webhooks/answer",
            "http_method": "POST"
        }
      }
    },
    "vbc": {}
  },
  "_links": {
    "self": {
      "href": "/v2/applications/27aa0583-7246-4822-aabb-17b03c25d52e"
    }
  }
}
```

> The next step is to [provision Smart Numbers](/smart-numbers/guides/provision-smart-numbers) using the Vonage API Platform Application `id`.
