---
title: Get Call Recordings
description: In this step you learn how to get call recordings from the Call Recording API
---

# Get call recordings

In this step you will make a GET request to the Call Recording API to get a JSON response with your call recordings.

1. Before you call the company_call_recordings API, you must pass in a date string that is in the past. For the purposes of this demonstration, you will use a date 7 days in the past:

    ```python
    import datetime
    import urllib.parse
    today = datetime.datetime.now()
    last_week = datetime.timedelta(days = 7)
    date_diff = today - last_week
    encoded_date = urllib.parse.quote_plus(date_diff.strftime('%Y-%m-%dT00:00:00+0000'))
    ```

    1. In this example, you get the current date using `datetime.datetime.now()`. 
    2. Use the `datetime.timedelta()` function to create a date that is `days` in the past. In this example, `7` is the value set. 
    3. Subtract the current date from the date 7 days in the past, to get your date. 
    4. Use `strftime()` to convert the date object into a string. In this example, the time is set to `00:00:00+0000`, which means you will get the date at midnight UTC.
    5. Before you can pass the date into the Call Recordings API, you must urlencode the date using `urllib.parse.quote_plus()`.

2. Request the `company_call_recordings/v1/api/` and use the `access_token` that was returned from the `get_token()` function. This will return a JSON response of the call recordings. Next, pass in the `encoded_date` into this function:

    ```python
    import requests
    comany_recordings = []
    def company_call_recordings(token, start_date, account_id="self",order="asc", page_size=10, page=1):
      url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/company_call_recordings?order={}&page_size={}&page={}&start:gte={}".format(account_id, order, page_size, page, start_date)
      headers = {
        'Accept': 'application/json',
        'Authorization': 'Bearer {}'.format(token),
      }

      response = requests.request("GET", url, headers=headers).json()
      if "_embedded" in response:
        comany_recordings.extend(response["_embedded"]["recordings"])

      if "total_pages" in response:
        if page < response["total_pages"]:
          page = page + 1
          company_call_recordings(token, start_date, account_id, order, page_size, page)

      return comany_recordings
    ```

    In this example, you are calling the `company_call_recordings/v1/api/` and passing the following parameters:

    | Key | Description |
    | --- | ----------- |
    | `account_id`      | The Vonage Business Communications account ID. You can use `self` to refer to the authenticated user's account. |
    | `page`      | The number of pages to request. |
    | `page_size`      | The requested page size. |
    | `order`      | The order of the returned call recordings. |
    | `start:gte`      | Filter records by start date (greater than or equal to). |

    You may also pass in `start:lte` which would return records less than the given date.

3. Once you get a list of call recordings, you will loop though each recording and delete them. 
    
    > Before doing this, make sure you have a backup of the recordings. Refer to the [Saving call recordings to Amazon S3](/tutorials/save-call-recording-s3) tutorial to save recordings to an Amazon S3 bucket.

For the purposes of this tutorial, you will create a function to delete the call recordings by their recording IDs in the next step.
