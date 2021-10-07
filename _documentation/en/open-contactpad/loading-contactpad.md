---
title: Loading the SDK
description: Learn how to load the Open ContactPad SDK
navigation_weight: 3
---

#  Loading the Open ContactPad SDK

##  Using SDK bundle as external script with a pre-existing Web page

### For Vonage Unified Communications /VBC, VBE/
``` bash
<script data-provider='uc' src='https://apps.gunify.vonage.com/cti/common/vonage.dialer.sdk.js'></script>
```

[LIVE SAMPLE](https://plnkr.co/edit/Hla8wmRvHPNTxe30?preview)

### For Vonage Contact Center /VCC/
``` html
<script data-provider='cc' data-cc-domain='nam.newvoicemedia.com' src='https://apps.gunify.vonage.com/cti/common/vonage.dialer.sdk.js'></script>
```
[LIVE SAMPLE](https://plnkr.co/edit/0I3NDs1soJYNxkZU?preview)

##  Using SDK as an NPM packag added to the webpage source code

[NPM Package](https://www.npmjs.com/package/@vgip/vonage-dialer-sdk)

``` javascript
const VonageDialer = require('@vgip/vonage-dialer-sdk');
 
VonageDialer.enableClickToDial(true); // Annotate phone numbers for click-to-dial
VonageDialer.init({ provider: '[cc|uc]' /* other config options */ }, (dialer) => { 
  // see “building with Open ContactPad”
});
```

* When loaded, the SDK is searching the current HTML page for a dedicated container element having class='vonage-dialer-container' and renders the dialer interface within it. If such a container element does not exist on the page, the interface starts in “DOT” mode by providing a clickable circle icon that can be dragged around the page.

* The Vonage Contact Center  interface requires 200px by 400px container size. The Unified Communications interface is responsive and fits well any container size (recommended 280px by 420px).

[LIVE SAMPLE](https://plnkr.co/edit/CxOH2DS4RJFwGxLH?preview)

> Continue to [Building with Open ContactPad](open-contactpad/building-contactpad).