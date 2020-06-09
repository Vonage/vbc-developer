---
title: Receive an inbound call
navigation_weight: 1
---

# Receive an inbound call

This code snippet shows you how to receive an inbound call on your Smart Number.
# Example

## Create an application

A Nexmo application contains the required configuration for your project. You can create an application using the [Nexmo CLI](https://github.com/Nexmo/nexmo-cli) or [via the dashboard](https://dashboard.nexmo.com/voice/create-application). To learn more about applications [see our Nexmo concepts guide](https://developer.nexmo.com/concepts/guides/applications).

## Install the CLI
```bash
npm install -g nexmo-cli
```

## Create an application
Once you have the CLI installed you can use it to create a Nexmo application. Run the following command and make a note of the application ID that it returns. This is the value to use in `NEXMO_APPLICATION_ID` in the example below. It will also create `private.key` in the current directory which you will need in the `Initialize your dependencies` step.

Nexmo needs to connect to your local machine to access your `answer_url`. We recommend using [ngrok](https://www.nexmo.com/blog/2017/07/04/local-development-nexmo-ngrok-tunnel-dr/) to do this. Make sure to change `demo.ngrok.io` in the examples below to your own ngrok URL.

```bash
nexmo app:create "Receive Inbound Call Example" http://demo.ngrok.io/webhooks/answer http://demo.ngrok.io/webhooks/events --keyfile private.key
```

## Install dependencies
```bash
npm install express
```
## Initialize your dependencies
Create a file named `receive-an-inbound-call.js` and add the following code:

```javascript
const app = require('express')()
```

## Write the code
Add the following to `receive-an-inbound-call.js`:

```bash javascript
const onInboundCall = (request, response) => {
  const from = request.query.from
  const fromSplitIntoCharacters = from.split('').join(' ')

  const ncco = [{
    action: 'talk',
    text: `Thank you for calling from ${fromSplitIntoCharacters}`
  }]

  response.json(ncco)
}

app.get('/webhooks/answer', onInboundCall)

app.listen(3000)
```

## Run your code
Save this file to your machine and run it:

```bash
node receive-an-inbound-call.js
```

## Try it out

When you call your Smart Number you will hear a text-to-speech message.
