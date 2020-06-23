---
title: How to receive call events via webhooks
---

# How to receive call events using webhooks

This guide will demonstrate how to create a webhook to receive events from calls. When a call is made or received, the webhooks API allows you to monitor active calls. The webhook will return the following information 
```json
{
 "event": {
 "accountId": "{YOUR_ACCOUNT_ID}",
 "callerId": "{CALLER_NAME}",
 "direction": "{DIRECTION}",
 "duration": {LENGTH OF CALL},
 "externalId": "{ID}",
 "id": "{ID}",
 "internal": {INTERNAL_FLAG},
 "phoneNumber": "{PHONE_NUMBER",
 "startTime": "IOS8601 TIME ",
 "state": "{CALL STATE}",
 "type": "{CALL_TYPE}",
 "ucpType": "",
 "userId": "{USER_ID"
 }
}
```
When the status of the call changes, a new payload will be sent to the webhook. 
* When the call begins, you will receive a payload with the `state` as `RINGING`. 
* When the call is answered, you will receive a payload with the `state` as `ACTIVE`. 
* When the call ends, you will receive a payload with the `state` as `ANSWERED`. 
* If the call is not picked up, you will receive a payload with the `state` as `MISSED`. 
For more information about the payload in a webhook, please see this [documentation](/guides/webhooks).


# Create Webhook

## Prerequisites
Before creating a new webhook, you will need to have a Developer account. Please look at the documentation on [how to login to the developer portal](/getting-started/create-a-developer-account).

After creating an account, you will need to subscribe to the Vonage Integration Platform APIs. Please look at [how to Subscribe to the VGIS API's](/getting-started/subscribe-to-apis) as a reference.

## Create a webhook
To create a webhook, make a `POST` request to:
`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`

In the body of the request, you will need to enter the following JSON:
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

The full curl request will look like the following:
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

In the `url` parameter, you will need to add your accessible URL. This URL will be called by the Vonage Integration Platform API when a call has been updated. A good way to create an accessible URL is to use [ngrok](https://www.nexmo.com/blog/2017/07/04/local-development-nexmo-ngrok-tunnel-dr) to expose a port on your local machine. 

To create your local server, you can use [ExpressJS](https://expressjs.com) for NodeJS or [Flask](https://flask.palletsprojects.com/en/1.1.x/) for Python.

## ExpressJS
To use an ExpressJS application, create a new application using `npm init`.
Next, install the ExpressJS library by using `npm install express --save`
Finally, we'll write the code:
```javascript
const express = require('express')
const app = express()
const port = 3000

app.post('/webhook', function(req, res, next) {
 console.log(req.body)
 res.send(200)
});

app.listen(port, () => console.log(`Example app listening at http://localhost:${port}`))
```
To start your application, run the following command:
`node app.js`

Your application will now print the events to the console when a call is made or received. 

Note: make sure the port you have specified(`300`) is the same port that you use when creating your ngrok URL.

## Flask
To create a Flask app, you will first need to create a virtual environment. Python 3 comes with [`venv`](https://docs.python.org/3/library/venv.html#module-venv) to create virtual environments.
In your project directory, create a new virtual environment and activate it.
```bash
python3 -m venv venv
. venv/bin/activate
```
Next, install Flask:
```bash
pip install Flask
```

Next, create a new file called `app.py` and create our application:
```python
from flask import Flask, request, Response
app = Flask(__name__)

@app.route('/webhook', methods=['POST'])
def webhook():
 print(request.get_json())
 return Response(status=200)
```
Finally run your application:

```bash
export FLASK_APP=app.py
flask run -h localhost -p 3000
```
This will run on port 3000, which is the same port as we have configured for ngrok.

Now when you make a call to your Vonage Business Cloud number or receive a call from your Vonage Business Cloud number, the application will print the events to the console.

# Webhook Errors

When creating a new webhook using the `vis/v1/self/webhooks/` endpoint, there is one thing to be aware of. 

If the webhook cannot be reached, or returns a 404 pr 500, that webhook is considered inactivate, and you will not see any incoming payload to that webhook. You can query the status of the all the webhook using this endpoint via GET
`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`

This will return a list of all the webhooks that are associated with your application.
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
For this example, the `lastErrorMessage` shows an error when the webhook was called. 
To receive events to the same webhook, you will need to make another POST request to create the webhook.

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

# Cleanup
Webhooks that were created that failed will still exist in your application, and it's a good idea to remove them.

To view all webhooks, make a GET request to 
`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`
This will return a list of all the webhooks. If the `failed` parameter is `True`, that webhook should be removed. 

Get the webhook id from the `id` parameter and make a DELETE request, with that id.

`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/{WEBHOOK_ID}`
This will return a 204 when the webhook was deleted. 

If you make another GET request to 
`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`
You will see that the webhook with that id no longer exists.

# Conclusion

In this guide, we have shown how to create and update call event webhooks using the Vonage Integration Platform API. Using webhooks will allow you to create a unique realtime call applications to build products your users will love.