---
title: Get Call Recordings
description: In this step you learn how to get call recordings from the Call Recording API
---

# Get call recordings

In this step you will make a GET request to the Call Recording API to get a JSON response with your call recordings.

1. Make a GET request to the Call Recording API and use the `access_token` that was returned from the `get_token` function. 

    ```python
    def get_company_call_recordings(token, account_id="self"):
      url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/company_call_recordings".format(account_id)

      headers = {
        'Accept': 'application/json',
        'Authorization': 'Bearer {}'.format(token),
      }

      response = requests.request("GET", url, headers=headers)
      return response.json()
    ```

    In this example, the `call_recording/v1/api/` is called and the following parameter is passed:

    | Key | Description |
    | --- | ----------- |
    | `account_id`      | The Vonage Business Communications account ID. You can use `self` to refer to the authenticated user's account. |

    > Note: A JSON response with a list of the account's call recordings is returned.

3. The Call Recording API supports many more parameters that can be used to filter your recordings. For example, you can filter recordings by length of recording using `duration:gte` and `duration:lte`. Refer to the [API documentation](/api/call-recording) for all available parameters.

Next, you will create a function to download the recording.
