---
title: Create a webhook
description: In this step you learn how to create a webhook.
---

# Create a webhook

1. To create a webhook, make a `POST` request to:

    `https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`

2. In the body of the request, you will need to enter the following JSON:

    ```json
     {
      "url": "{YOUR_URL}",
      "events": [
      "CALL"
      ],
      "signingAlgo": "HMAC_SHA256",
      "signingKey": "string",
      "metadataPolicy": "NONE"
    }
    ```

3. The full curl request will look like the following:

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

4. In the `url` parameter, you will need to add your accessible URL. This URL will be called by the Vonage Integration Platform API when a call has been updated. A good way to create an accessible URL is to use [ngrok](https://www.nexmo.com/blog/2017/07/04/local-development-nexmo-ngrok-tunnel-dr) to expose a port on your local machine.

> Next, you will create your local server. To create your local server, you can use [ExpressJS](https://expressjs.com) for NodeJS or [Flask](https://flask.palletsprojects.com/en/1.1.x/) for Python.
