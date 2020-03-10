---
title: Retrieve call logs for an account
navigation_weight: 1
---

# Retrieve call logs for an account
This example shows you how to return a list of all calls by account

Replace the following placeholder value in the sample code:

| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| account_id | The Vonage Business Communications account ID. |
| start_gte | Filter records by start date (greater equal or equal to). Must be in the following format YYYY-MM-DD HH:mm:ss | 
| start_lte | Filter records by start date (less equal or equal to).  Must be in the following format YYYY-MM-DD HH:mm:ss | 
| page_size | Number of records per page |
| page | Current page number |

``` bash
 curl --location --request GET 'https://api.vonage.com/t/vbc.prod/reports/v1/accounts/$account_id/call-logs?start:gte=$start_gte&start:lte=$start_lte&page_size=$page_size&page=$page' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer $bearer'
```
