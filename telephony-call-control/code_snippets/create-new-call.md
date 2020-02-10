# Create a new call

This example shows you how to make a phone call. In order to make the call, you will need to have a physical phone or softhone  

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Cloud account ID. |
| extension | A user's extension number | 

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/telephony/v3/cc/accounts/$account_id/calls?extension=$extension' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer $bearer_token'
```
