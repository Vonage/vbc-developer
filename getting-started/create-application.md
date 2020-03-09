---
title: Creating an API Application
description: Learn how to create an API application to use with Vonage Business Communications APIs
navigation_weight: 3
---

# Creating an Application

To work with the Vonage Business Communications APIs, you must create a API application.

> Note: To avoid confusion, "application" in this context refers to a logical grouping of APIs. The application you are building to consume these APIs will be referred to as "application".

## Create a new Application

1. Sign into [Developer Portal](https://developer.vonage.com/store/) using your Vonage Business Communications credentials and select "Vonage Business Communications" from the platform drop down list.

2. Select "My Applications" from the left-hand navigation menu.

3. Click "Add Application" at the top of the page.

4. In the Add Application dialog, enter a name and optionally a description for your Application, so that you can locate it easily later. You can limit the maximum number of requests that each access token allows (see [authentication](/getting-started/authentication)) in the "Per Token Quota" dropdown. By default it is "Unlimited". Then click the "Add" button.

![Screenshot showing the Add Application dialog](/assets/images/vbc/create-application.png)

> Now that you have created your application, you need to [subscribe to APIs](/getting-started/authentication) to enable it to use the VBC APIs.