---
title: Concepts
description: Learn more about using an embeddable dialer
navigation_weight: 2
---

#  Concepts

##  Embeddable Dialer

The dialer interface is not itself a softphone, but it can be used to control Vonage devices such as a hard wired phone or the Vonage Business Communications Desktop or Mobile applications.  To learn more about using Vonage Business Communications, visit the [Vonage Learning Center](https://vbctraining.vonage.com/).

##  How To Embed Contact Center ContactPad
This same SDK can be used to embed the [Vonage Contact Center (CC)](https://www.vonage.com/contact-centers/) ContactPad.  Some functionality, such as customizing the dialer interface and bringing your own contacts is not available.  The interface requires a 200px by 400px container size as described in the [Loading the Open ContactPad SDK](/open-contactpad/loading-contactpad) section.

``` html
<script data-provider='cc' data-cc-domain='nam.newvoicemedia.com' src='https://apps.gunify.vonage.com/cti/common/vonage.dialer.sdk.js'></script>
```

[LIVE SAMPLE](https://plnkr.co/edit/0I3NDs1soJYNxkZU?preview)

For Vonage Contact Center APIs, visit the [Vonage Contact Center Developer Portal](https://developer.newvoicemedia.com/).

> Continue to [Loading the Open ContactPad SDK](/open-contactpad/loading-contactpad).