# Retrieve download
This example shows you how to download audio files for company and on-demand call recordings.

Replace the following placeholder value in the sample code:
| Key        | Description                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| bearer_token | Your OAuth token. [Read more about OAuth tokens](https://developer.nexmo.com/vonage-business-cloud/vbc-apis/getting-started/authentication) |
| job_id | The job ID |
| login_name | 	
The login_name of the user |

``` bash
curl --location --request GET 'https://api.vonage.com/t/vbc.prod/call_recording/v1/api/bulkDownload/retrieve?job_id=$job_id&login_name=$login_name' \
--header 'Content-Type: application/zip' \
--header 'Authorization: Bearer $bearer_token' \
```
