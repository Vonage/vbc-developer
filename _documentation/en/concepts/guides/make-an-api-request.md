---
title: Making an API Request
description: Learn how to make an API request
navigation_weight: 6
---

# Making an API Request

Now that you've [created an access token](/concepts/guides/create-an-access-token) you are ready to make an API request.

## Sample Request

The following sample uses [curl](https://curl.haxx.se/). You can run this sample on the Linux command line.

Replace the following placeholder values in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](/concepts/guides/create-an-access-token) |
| account_id | The Vonage Business Communications account ID. You can use 'self' to refer to the authenticated user's account. |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/provisioning/api/accounts/$account_id/account' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```

