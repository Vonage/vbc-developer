---
title: Route to a VBC Extension
navigation_weight: 2
---

# Route to a VBC Extension

This code snippet demonstrates how to connect an inbound call on a Smart Number to an extension.

## Example

The following example shows how to receive the inbound call and immediately forward it to your chosen VBC extension.

You achieve this with a `connect` [action](/voice/voice-api/ncco-reference#connect) in the Vonage API Platform Call Control Object (NCCO). Create an `endpoint` with a type of `vbc` and the `extension` you want to forward the call to.

```code_snippets
source: '_examples/smart-numbers/vbc-route-to-extension'
application:
  type: voice
  name: 'Connect to VBC Extension Example'
```

## Try it out

When you call your Smart Number it should immediately forward the call to the extension number you specified.