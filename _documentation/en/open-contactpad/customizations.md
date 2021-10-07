---
title: Customizing the User Interface
description: Learn how to customize the Open ContactPad User Interface
navigation_weight: 5
---

#  Customizing the Open ContactPad User Interface (UC only)

  * [Create an integration provider](#create-an-integration-provider)
  * [Set integration icon](#set-integration-icon)
  * [Add Custom Settings to the Dialer Interface](#add-custom-settings-to-the-dialer-interface)
  * [Contacts provider](#contacts-provider)
    + [Contacts autocomplete (dial suggestions)](#contacts-autocomplete--dial-suggestions-)
      - [Register the custom contact search method with the dialer API setOnSearchContactables:](#register-the-custom-contact-search-method-with-the-dialer-api-setonsearchcontactables-)
    + [Set interaction contact (active call screen)](#set-interaction-contact--active-call-screen-)
  * [Interactive History](#interactive-history)

##  Create an integration provider

Choose a unique name for your integration provider. It will be used to associate integration provider owned resources. The below samples are using ‘acme’ as customization provider.

Tell the UC dialer which extra features to enable in the user interface during the initialization. 

> Note: You still have to implement the corresponding handlers for the enabled features!

``` javascript
 VonageDialer.init({
   features: {
     contactsProvider: true,
     openContact: true,
     openActivity: 'acme',
     eventsHistory: true
   }
 }, (dialer) => { /* <-- dialer instance */ });
 ```

## Set integration icon

``` javascript
VonageDialer.init({}, (dialer) => {
  dialer.registerSvgIcon('acme', 'data:image/svg+xml;base64,PHN… ...zdmc+');
});
```

* You can convert any SVG image (recommended size 64x64px) to a data URL with an [online tool](https://dopiaza.org/tools/datauri/index.php).

##  Add Custom Settings to the Dialer Interface
![](/images/open-contactpad/settings.png "Custom Settings")

The SDK provides a method to extend the dialer interface default settings with extra configuration options (supported types: string, boolean, select). 

``` javascript
dialer.registerCustomSettings('acme', [
  { name: 'autoLog', label: 'Auto Log Telephony Records', type: 'boolean', subtype: 'switch', default: true },
  { name: 'skipInternal', label: 'Skip internal communications', type: 'boolean', subtype: 'checkbox', dependsOn: 'autoLog', default: true },
  { name: 'skipZeroDuration', label: 'Skip zero duration calls', type: 'boolean', subtype: 'checkbox', dependsOn: 'autoLog', default: true },
  { name: 'skipNoContact', label: 'Skip if contact not found', type: 'boolean', subtype: 'checkbox', dependsOn: 'autoLog' },
  { name: 'skipMultipleContacts', label: 'Skip if multiple contacts', type: 'boolean', subtype: 'checkbox', dependsOn: 'autoLog' }
]);
dialer.getSettings('acme', (settings) => {
  //{"autoLog":true,"skipInternal":true,"skipZeroDuration":false,"skipNoContact":true}
});
``` 

[LIVE SAMPLE](https://plnkr.co/edit/aRIIleXeQajPljil?preview)

* The extra settings values are auto-saved by the dialer in the browser storage and are available for later use by the integration code (honoring the default values).

##  Contacts provider

How to bring your own contacts within the dialer interface.

![](/images/open-contactpad/contacts-provider.png)

### Contacts autocomplete (dial suggestions)

Implement a special method for searching contacts from your own data source. The first input parameter is the text user types in the dialer input control (*it could be a phone number or any text as string). The second parameter is a callback function for returning the results when the search is complete. The callback must be called always with a parameter of type array (including zero or more contactable items). The UI shows a tiny progress bar during the search.

``` javascript
const searchContactables = (query, callback) => {
  // 'query' parameter contains the autocomplete search string
  callback([
   {
     provider: 'acme',
     id: '123',
     label: 'John Smith',
     type: 'contact',
     typeLabel: 'Contact',
     phoneNumber: '+12027621401',
     phoneType: 'Mobile'
   },
   {
     provider: 'acme',
     id: '124',
     label: 'John Smith',
     type: 'lead',
     // 'typeLabel' - optional, for visualization purposes
     phoneNumber: '+12027621401',
     // 'phoneType' - optional, for visualization purposes (home, mobile, office)
   }
  ]);
};
```

#### Register the custom contact search method with the dialer API setOnSearchContactables:

``` javascript
  dialer.setOnSearchContactables(searchContactables);
```

[LIVE SAMPLE](https://plnkr.co/edit/BPtph0rmNgrhW3x1?preview)

### Set interaction contact (active call screen)

The SDK allows attaching an external contact object to the interaction events for visualization and logging purposes.
Once the ongoing call identifier is known (see [Subscribing for interaction events](/open-contactpad/building-contactpad#subscribing-for-interaction-events)), the integration could assign an external contact to the interaction. 

The attached contactable is visualized during the active call screen (UC only) and also is carried by the system through the whole interaction lifecycle.

``` javascript
dialer.setOnDialerEvent((event) => {
   switch (event.type) {
     case 'CALL_START': {
       dialer.setInteractionContact(event.data.id, {
         provider: 'acme',
         id: '123',
         label: 'John Smith',
         type: 'contact',
       });
       break;
     }
     case 'CALL_END': {
       console.log(event.data.contact); // <- carries the assigned contact object
       break;
     }
     default: {
       console.log('Unhandled event', event);
     }
   }
 });
```

[LIVE SAMPLE](https://plnkr.co/edit/mRtUOrqEqbfm2OQn?preview)

* The contact assignment is available in both CC and UC dialers, but CC ContactPad does not visualize the given contact name within the user interface.

##  Interactive History

Coming soon!

> Continue to [SDK Reference Material](/open-contactpad/sdk-reference).

