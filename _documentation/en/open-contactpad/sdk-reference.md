---
title: SDK Reference Material
description: Learn how to customize the Open ContactPad User Interface
navigation_weight: 6
---

#  SDK Reference Material

- [SDK Global Methods](#sdk-global-methods)
  * [Init](#init)
  * [setProvider](#setprovider)
  * [placeCall](#placecall)
  * [setProvider](#setprovider-1)
  * [enableClickToDial](#enableclicktodial)
  * [setCountryCode](#setcountrycode)
- [SDK Dialer Instance Methods](#sdk-dialer-instance-methods)
  * [setVisibility](#setvisibility)
  * [setOnDialerEvent](#setondialerevent)
  * [registerSvgIcon](#registersvgicon)
  * [placeCall](#placecall-1)
- [SDK Data Models](#sdk-data-models)
  * [dialerEvent](#dialerevent)
  * [Event type CALL_START](#event-type-call-start)
  * [Event type CALL_ANSWER](#event-type-call-answer)
  * [Event type CALL_END | CALL_HISTORY](#event-type-call-end---call-history)
  * [dialerConfig](#dialerconfig)
  * [dialerFeatures](#dialerfeatures)
  * [contactable](#contactable)
  * [entityRef](#entityref)

##  SDK Global Methods

### Init

Acquire a dialer API instance and ensure the dialer interface is ready 
(see [SDK dialer instance methods](#sdk-dialer-instance-methods))

| Parameter | Type | Description |
| --- | ----- | ----------- |
| dialerConfig | \[object\] | Dialer configuration options. |
| callback | \[function\] | Callback function. |

### setProvider

Allows switching the provider (CC/UC) after the dialer interface is 
loaded. 

* The SDK provides other methods to set the provider during initial 
load (see [Loading Open ContactPad SDK](loading-contactpad))

| Parameters | Type | Description |
| --- | ----- | ----------- |
| provider | "cc" / "uc" | <ul><li>CC loads Vonage Call Center ContactPad as a dialer interface /VCC/.</li><li>UC loads Vonage Business Communicatons ContactPad as a dialer interface /VBC, VBE/.</li></ul> |
| ccDomain (optional) | \[string\] | Use a custom VCC region domain. Well known options are: <ul><li>nam.newvoicemedia.com (default)</li><li>emea.newvoicemedia.com</li><li>apac.newvoicemedia.com</li></ul> |
| ccAccount (optional) | \[string\] | Use a custom VCC account name.  |

### placeCall

Shortcut alias to dialer instance method placeCall (to be used when 
integration does not allow custom initialization). 

* The result is not guaranteed if called too early.

| Parameters | Type | Description |
| --- | ----- | ----------- |
| phoneNumber | \[string\] | Phone number to dial |
| contactable (optional) | \[entityRef\] | Optionally pass a preferred contact to be attached to the interaction events. |

### setProvider
Allows switching the provider (CC/UC) after the dialer interface is 
loaded. 

* The SDK provides other methods to set the provider during initial 
load (see [Loading Open ContactPad SDK](loading-contactpad))

| Parameters | Type | Description |
| --- | ----- | ----------- |
| provider | "cc" / "uc" | <ul><li>CC loads Vonage Call Center ContactPad as a dialer interface /VCC/.</li><li>UC loads Vonage Business Communicatons ContactPad as a dialer interface /VBC, VBE/.</li></ul> |
| ccDomain (optional) | \[string\] | Use a custom VCC region domain. Well known options are: <ul><li>nam.newvoicemedia.com (default)</li><li>emea.newvoicemedia.com</li><li>apac.newvoicemedia.com</li></ul> |
| ccAccount (optional) | \[string\] | Use a custom VCC account name. |

### enableClickToDial
Enable/Disable SDK build in phone number annotation 
library.  

| Parameters | Type | Description |
| --- | ----- | ----------- |
| enabled | \[boolean\] | Annotate phone numbers on the current WEB page with a ClickToDial icon. |

### setCountryCode
Set default country for national format phone numbers 
recognition. 

* In use by ClickToDial annotation library and UC 
dialer interface productivity helpers.

| Parameters | Type | Description |
| --- | ----- | ----------- |
| countryCode | \[string\] | 2 character country code ([ISO 3166-1 alpha-2 standard)](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |


##  SDK Dialer Instance Methods
``` javascript
VonageDialer.init({ debug: true }, (dialer) => {
  dialer // <- dialer instance 
});
```

### setVisibility
Programmatically show/hide the dialer frame in DOT 
mode. This method has no effect when the dialer is loaded in a container. 

* In DOT mode the user invokes the ContactPad frame by clicking
on the Vonage button and hides the frame when the user clicks anywhere on the surrounding page areas.

| Parameters | Type | Description |
| --- | ----- | ----------- |
| visible | \[boolean\] | Show/Hide the dialer frame. |

### setOnDialerEvent
Register a callback function to be executed when a dialer event occurs. 

| Parameters | Type | Description |
| --- | ----- | ----------- |
| callback | \[function\] | Event processing callback function. The parameter sent to the callback function is a polymorphic model object having a property named "type". Each event type has its own properties structure. |

### registerSvgIcon
(UC dialer only) Set custom integration icon for settings and contacts visualization. 

| Parameters | Type | Description |
| --- | ----- | ----------- |
| providerCode | \[string\] | Custom integration provider programmatic name. |
| dataUrl | \[string\] | Base64 data encoded SVG image (* You can convert any SVG image (recommended size 64x64px) to a data URL with an [online tool](https://dopiaza.org/tools/datauri/index.php)). |

### placeCall

Place a call.

| Parameters | Type | Description |
| --- | ----- | ----------- |
| phoneNumber | \[string\] | Phone number to dial. |
| contactable (optional) | \[entityRef\] | Optionally pass a preferred contact to be attached to the interaction events. |

##  SDK Data Models

### dialerEvent
Dialer events are polymorphic objects categorized by type. The SDK uses events for operations that do not require response from the integration code.

| Properties | Type | Description |
| --- | ----- | ----------- |
| type | \[string\] | Interaction or operation event type: <ul><li>CALL_START - Call first appearance</li><li>CALL_ANSWER (*UC only) - The call is connected</li><li>CALL_END - The call reached its final state</li><li>CALL_HISTORY (*UC only) - The user selected an interaction from the history dialog interface.</li><li>CHAT_START (*CC only)</li><li>CHAT_END (*CC only)</li><li>READY - The user is logged in the interface.</li><li>LOGOUT - The user logged out.</li><li>HEALTH - The telephony service status (ability to place and receive calls).</li></ul> |
| data | [object] | Event data. Each type has a different data schema. |

### Event type CALL_START

The event is generated by the SDK only once when a 
new interaction appear (in any internal state), or 
when there is an active call after the dialer is reloaded.

| Properties | Type | Description |
| --- | ----- | ----------- |
| id | \[string\] | Telephony provider interaction identifier. This identifier is not unique for the system. In order to keep association to the Vonage interaction in 3rd party storage use uid instead. |
| uid | \[string\] | A composite interaction identifier (guarantees true uniqueness for the whole system). |
| direction | "INBOUND" / "OUTBOUND" | Interaction direction |
| phoneNumber | \[string\] | Interaction remote party phone number |
| state | \[string\] | Interaction fine lifecycle state (INITIALIZING -> RINGING -> ACTIVE -> final disposition). |
| internal | [boolean / undefined] |TRUE when this is a Vonage account internal communication. |
| tag (optional) | \[string\] | *VBC only. [Call Tagging](https://businesssupport.vonage.com/articles/answer/Custom-Call-Tagging-999) |
| contact (optional) | \[contactable\] | Attached contact. A contact could be assigned with the [place call](#placecall-2) action. |
| activity (optional) | \[entityRef\] | Attached uncompleted/current 3rd party activity reference. |

### Event type CALL_ANSWER
(UC only) The event is generated by the SDK when the call is connected.

| Properties (extends [CALL_START event schema](#event-type-call_start)) | Type | Description |
| --- | ----- | ----------- |
| answerDate | \[datetime\] | Answer time. |

### Event type CALL_END | CALL_HISTORY

The END event is generated by the SDK when the interaction reaches its final state. The HISTORY event is generated when the user selects a completed call from the history.

| Properties (extends [CALL_START event schema](#event-type-call_start)) | Type | Description |
| --- | ----- | ----------- |
| answerDate (optional) | \[datetime\] | Answer time (unless it is zero duration state). |
| endDate | \[datetime\] | Release time. |


* In case the custom integration is interested in the fine call state logic, here are some help constants including all possible call STATEs and its lifecycle:

``` javascript
const ACTIVE_CALL_STATES = ['INITIALIZING', 'RINGING', 'ACTIVE', 'HELD', 'REMOTE_HELD'];
const TALKING_CALL_STATES = ['ACTIVE', 'HELD', 'REMOTE_HELD'];
const RELEASED_CALL_STATES = ['ANSWERED', 'CANCELLED', 'MISSED', 'REJECTED', 'DETACHED', 'DISCONNECTED'];
const ZERO_DURATION_STATES = ['CANCELLED', 'MISSED', 'REJECTED', 'DISCONNECTED'];
```

### dialerConfig
Configuration options for SDK init method.

| Properties | Type | Description |
| --- | ----- | ----------- |
| debug | \[boolean\] <br> default: false | Print extra debug information in the browser JS console. |
| provider "cc" / "uc" <br> default: "uc" | <ul><li>CC loads Vonage Call Center ContactPad as a dialer interface /VCC/.</li><li>UC loads Vonage Integration Platform (VGIP) as a dialer interface /VBC, VBE/.</li> |
| ccDomain (CC only) | \[string\] | Use a custom VCC region domain. Well known options are: <ul><li>nam.newvoicemedia.com (default)</li><li>emea.newvoicemedia.com</li><li>apac.newvoicemedia.com</li> |
| ccAccount (optional) | \[string\] | Use a custom VCC account name. |  
| features (UC only) | \[dialerFeatures\] | Customize UC dialer interface (show/hide extra UI controls). |

### dialerFeatures
Show/Hide extra controls in the UC dialer interface.

| Properties | Type | Description |
| --- | ----- | ----------- |
| contactsProvider | \[boolean\] <br> default: false | When enabled, the dialer will execute the configured searchContactables callback when the user types in the dialpad phone number input and show the results as contacts suggestions. |
| openContact | \[boolean\] <br> default: false | When enabled, the dialer will visualize an extra "open external link" icon near the contacts within the interface. Click on the icon executes the implemented openContact callback.|
| openActivity | \[string\] | The value must be the providerCode chosen for the custom integration. Vonage Integrations attaches activities from different integration sources to the interaction events. The value is used as a scope to filter only the activities generated by your custom integration provider. When enabled, the UC dialer will visualize an extra "new/open note" icon in the interaction history and during an active call. Click on the icon executes the implemented openActivity callback. |
| eventsHistory | \[boolean\] <br> default: true | When enabled the dialer will generate an extra event of type "CALL_HISTORY" when the user clicks on a completed call from the interaction history dialog. |

### contactable
Unified object which represent any 3rd party entity having names and phone number and can represent an interaction party.

| Properties | Type | Description |
| --- | ----- | ----------- |
| provider | \[string\] (required) | Custom integration code. When visualizing contacts UI decorates the contact with the registered SVG icon having the same provider code. |
| id | \[string\] (required) | External identifier. The custom integration contact uniqueness must be based provider+id+type. |
| type | \[string\] (required) | External entity programmatic type. <br> *Common CRM types are: Contact, Lead, Account, Candidate etc. |
| label | \[string\] (required) | A string representing the external entity as human readable text  sufficient enough for the user to recognize that the object is the desired one.<br> *Usually in CRMs it is the First and Last name + some extra info specific for the integration. |
| phoneNumber | \[string\]  (required) | Contact phone number. Recommended is E.164 format, although the system is compatible with national formats when the country code is set correctly. |
| phoneType | \[string\] (optional) | Extra label for visualization purposes. If the integration has a contact with 2 numbers (Home and Mobile), it must use 2 identical contactables having only different phoneNumber and phoneType. |
| typeLabel | \[string\] (optional) | Human label for the programmatic entity type for visualization purposes. |

### entityRef
Unified object which represents any 3rd party entity having integration 
code, unique identifier and type 

> NOTE: The object could be a contactable as well, but the purpose is not Visualization (it does not require a phone number). The reference is carried with the interaction events and could be used for custom logic.

| Properties | Type | Description |
| --- | ----- | ----------- |
| provider | \[string\] (required) | Custom integration code. |
| id | \[string\] (required) | External identifier. The custom integration contact uniqueness must be based provider+id+type |
| type | \[string\] (required) | External entity programmatic type. *CRM type like: Case, Campaign, Task, etc.. |
| label | \[string\] (optional) | A string representing the external entity as human readable text,  sufficient enough for the user to recognize that the object is the desired one. |
| typeLabel | \[string\] (optional) | Human label for the programmatic entity type for visualization purposes. |




















