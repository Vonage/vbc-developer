---
title: Create a webhook
description: In this step you learn how to create a webhook.
---

# Webhook errors

If the webhooks you created using the `vis/v1/self/webhooks/` endpoint cannot be reached or returns a 404 or 500, that webhook is considered inactivate and you will not see any incoming payload to it. You can query the status of all the webhooks by making a GET call to the following endpoint:

`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`

This will return a list of all the webhooks that are associated with your application:

```json
[
 {
 "id": "{}",
 "userId": "{}",
 "accountId": "{}",
 "url": "{}",
 "status": "ACTIVE",
 "events": [
 "CALL"
 ],
 "signingAlgo": "HMAC_SHA256",
 "signingKey": "string",
 "metadataPolicy": "NONE",
 "expireAt": "2030-06-21T11:06:21.038Z",
 "createdAt": "2020-06-23T11:06:21.038Z",
 "purgeAt": "2040-09-16T11:06:21.038Z",
 "statistics": {
 "totalAttempts": 8,
 "totalSuccesses": 5,
 "totalFailures": 3,
 "failed": true,
 "lastSuccess": "2020-06-23T11:28:12.434Z",
 "lastFailure": "2020-06-23T17:21:48.207Z",
 "lastHttpErrorCode": "500 INTERNAL_SERVER_ERROR",
 "lastErrorMessage": "500 INTERNAL SERVER ERROR: [<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 4.01 Transitional//EN\"\n \"http://www.w3.org/TR/html4/loose.dtd\">\n<html>\n <head>\n <title>NameError: name 'flask' is not defined // Werkzeug Debugger</title>\n... (19777 bytes)]"
 }
 }
]
```

In the example above, the `lastErrorMessage` shows an error when the webhook was called. 

To receive events to the same webhook, you will need to make another POST request to create the webhook:

```bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
 "url": "https://{NGROK_URL}/webhook",
 "events": [
 "CALL"
 ],
 "signingAlgo": "HMAC_SHA256",
 "signingKey": "string",
 "metadataPolicy": "NONE"
```

You will then see the incoming events after the webhook has been updated.
