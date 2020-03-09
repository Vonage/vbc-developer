# Get user data by account ID and user ID

This example shows you how to get detailed information on a given user for an account.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |
| user_id | The User Id. |


``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/users/$user_id' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
