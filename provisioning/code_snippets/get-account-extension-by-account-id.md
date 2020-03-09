# Get account extensions data by account ID

This example shows you how to get a list of account extensions by the account Id. For each extension, you will receive information about the user that is tied to the extension, as well as the caller_id and any headsets that are connected to the extension.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |


``` bash
curl --location --request POST 'https://api.vonage.com/t/vbc.prod/provisioning/v1/api/accounts/$account_id/extensions' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer $bearer_token' \
```
