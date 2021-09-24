---
title: Get device registration info
navigation_weight: 1
---

# Get device registration info

This example shows you how return the details of a device. 

Replace the following placeholder values in the sample code:

| Key | Description |
| --- | ----------- |
| bearer_token      | Your OAuth token. [Read more about OAuth tokens](/getting-started/create-a-developer-account) |
| account_id        | The Vonage Business Communications account ID. |
| device_id         | MAC address of device | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/registration/accounts/$account_id/devices/$device_id' \
--header 'Authorization: Bearer $bearer_token'
```
