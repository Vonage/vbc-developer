---
title: Cleanup
description: In this step you learn how to remove webhooks associated with your application that have failed.
---

# Cleanup

In some cases, you may encounter webhooks that fail. These webhooks will still exist in your application and it's recommended you remove them.

To view all webhooks, make a GET request to:

`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`

This will return a list of all the webhooks. If the `failed` parameter is `True`, that webhook should be removed. 

Get the webhook id from the `id` parameter and make a DELETE request, with that id:

`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/{WEBHOOK_ID}`

This will return a 204 when the webhook was deleted. 

If you make another GET request to:

`https://api.vonage.com/t/vbc.prod/vis/v1/self/webhooks/`

You will see the webhook with that id no longer exists.
