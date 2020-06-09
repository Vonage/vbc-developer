---
title: Route to a VBC Extension
navigation_weight: 2
---

# Route to a VBC Extension

This code snippet shows you how to connect an inbound call on a Smart Number to an extension.

## Example

The following example shows how to receive the inbound call and immediately forward it to your chosen VBC extension.

You achieve this with a `connect` [action](https://developer.nexmo.com/voice/voice-api/ncco-reference#connect) in the Nexmo Call Control Object (NCCO). Create an `endpoint` with a type of `vbc` and the `extension` you want to forward the call to.


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
nexmo app:create "Connect to VBC Extension Example" http://demo.ngrok.io/webhooks/answer http://demo.ngrok.io/webhooks/events --keyfile private.key
```
## Install dependencies
```bash
npm install express
```
## Initialize your dependencies
Create a file named `connect-to-extension.js` and add the following code:

```bash
const app = require('express')()
```

## Write the code
Add the following to `connect-to-extension.js`:

```javascript
const onInboundCall = (request, response) => {
  const ncco = [{
    action: 'connect',
    endpoint: [{
      type: 'vbc',
      extension: VBC_EXTENSION
    }]
  }]

  response.json(ncco)
}

app.get('/webhooks/answer', onInboundCall)

app.listen(3000)
```

## Run your code
Save this file to your machine and run it:
```bash
node connect-to-extension.js
```

## Try it out

When you call your Smart Number it should immediately forward the call to the extension number you specified.
