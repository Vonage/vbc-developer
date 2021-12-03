---
title: Building with the SDK
description: Learn what you can build with the Open ContactPad SDK
navigation_weight: 4
---

#  Building with the Open ContactPad SDK

- [Place a call programmatically](#place-a-call-programmatically)
- [Subscribing for interaction events](#subscribing-for-interaction-events)
- [Click To Dial](#click-to-dial)
  - [Set country code](#set-country-code)

##  Place a call programmatically

``` html
<script type="text/javascript">
  VonageDialer.placeCall('+17328586962' /* optionally pass a preferred contact */
  // , { 
  //   provider: 'acme',
  //   id: '123',
  //   label: 'John Smith',
  //   type: 'contact'
  // }
  ); 
</script>
```

[LIVE SAMPLE](https://plnkr.co/edit/ycIKCdhOYaPMynZH?preview)

* For the feature to work, the user must be logged in to the dialer and have an up and running software or hardware phone.
* The function should be called only after the dialer interface is fully loaded (after the VonageDialer.init(..callback function...) javascript is loaded). You can ensure that by executing it after the initialization callback.

##  Subscribing for interaction events

``` javascript
VonageDialer.init({ /* dialer config options */ }, (dialer) => {
  dialer.setOnDialerEvent((event) => {
    switch (event.type) {
      case 'CALL_START': {
        break;
      }
      case 'CALL_ANSWER': { // available only for UC
        break;
      }
      case 'CALL_END': {
        // do something based on event.data (screen pop, store interaction, etc.)
        break;
      }
      default: {
        console.log('Unhandled event', event);
      }
   }
  });
});
```

[LIVE SAMPLE](https://plnkr.co/edit/CCke8DxuWX6v0OnD?preview)

* The SDK architecture uses events for interaction events and other operations that do not require response from the custom integration code and callbacks for controlled request-response operations.
* For more information about Vonage events, look at the [SDK Data Model](sdk-reference#dialerevent).

##  Click To Dial 

The SDK includes a built-in phone annotation library which can parse the current page HTML content for valid phone number strings and will place a phone icon near the discovered numbers for easy ClickToDial.

![](/images/open-contactpad/click-to-connect.png "Click to Dial")

``` html
<script type="text/javascript">
  VonageDialer.enableClickToDial(true);
</script>
```

### Set country code

By default the parser is annotating all international formatted numbers (having country code prefix) and all valid national format US numbers. In order to work with a different country's local phone numbers, change the dialer country code based on ISO 3166-1 alpha-2 standard.

``` html
<script type="text/javascript">
  VonageDialer.setCountryCode('GB'); // work with UK local numbers
  VonageDialer.enableClickToDial(true);
</script>
```

[LIVE SAMPLE](https://plnkr.co/edit/1WGqaqmvtRM15HBI?preview)

> Continue to [Customizations](customizations).