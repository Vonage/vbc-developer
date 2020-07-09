---
title: Overview
---
# Smart Numbers Overview

> **Note** Smart Numbers is for [Vonage Business Communications Customers](https://www.vonage.com/business/) only.

Vonage Business Communications Smart Numbers enable you to:

* Forward a Vonage Business Communications call to a Nexmo [Voice API](https://developer.nexmo.com/voice/voice-api/api-reference) application
* Connect calls to a Vonage Business Communications extension from a Voice API [NCCO](https://developer.nexmo.com/voice/voice-api/guides/ncco)

## What can you do with it?

You can use all the power and flexibility of the Nexmo Voice API together with the supporting Vonage Business Communications [Provisioning API](/api/provisioning) to create fully customized call experiences for your customers, including:

* Interactive voice response (IVR) systems that link to your CRM system to personalize the menu options to your customers' needs
* Voicebots that use natural language processing and/or AI to answer simple questions spoken by your customers
* Automatic proxying of local numbers based on the area code dialed
* Voice broadcasts to alert customers to important news or events
* Real-time sentiment analysis to gauge the "mood" of a call
* Calendar integration to check the free/busy status of a call recipient and react accordingly

## Getting Started

To use Smart Numbers, you need:

* A Vonage Business Communications account
* A Nexmo account

Next, you must:

1. [Enable the Smart Number add-on](guides/enable-addon) - To add the capability to your Vonage Business Communications account
2. [Create a Nexmo Voice API Application](guides/create-voice-application) - To store security and configuration information
3. [Provision Smart Numbers](guides/provision-smart-numbers) - Configure one or more Vonage Business Communications numbers as Smart Numbers and link those numbers to your Nexmo Voice API Application

## Using Smart Numbers

You will use the [Nexmo Voice API](https://developer.nexmo.com/voice/voice-api/api-reference) to build interactive and customized call experiences for your users. Vonage provides [client libraries](https://github.com/Nexmo/) in various languages that make it easier to work with the Voice API.

To forward an inbound call on one of your linked Vonage Business Communications numbers to your Nexmo Voice API Application, you create a [webhook](https://developer.nexmo.com/concepts/guides/webhooks) endpoint in your code and configure the URL in your Nexmo account. This is so that Nexmo's APIs can alert your application when a call is received and ask for instructions on how to process the call.

You provide these instructions in the form of a [Nexmo Call Control Object (NCCO)](https://developer.nexmo.com/voice/voice-api/guides/ncco) that defines the list of actions that the call must perform, such as reading a message to your caller using text-to-speech, or collecting input as part of an interactive voice response (IVR) system. You can also use a `connect` action in the NCCO to route the call to a Vonage Business Communications extension.

You can use the [Vonage Business Communications APIs](_documentation/index) in your application to retrieve information about your Vonage Business Communications accounts, extensions and users.

> **Getting help**: For a comprehensive list of resources to help you build your application, see [here](guides/vbc-resources).
