---
title: Delete Call Recordings
description: In this step you learn how to delete call recordings and/or on-demand call recordings
---

# Delete call recordings and on-demand call recordings

You can [delete call recordings](#delete-call-recordings) and [delete on-demand call recordings](#delete-on-demand-call-recordings) by duration. 

## Delete Call Recordings

The `get_company_call_recordings()` function returns a list of recordings from the account. 

1. Create a function to delete the recording by its recording id:

    ```python
    def delete_call_recording(token, call_id, account_id="self"):
      url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/company_call_recordings/{}".format(account_id, call_id)
    
      headers = {
        'Accept': 'application/json',
        'Authorization': 'Bearer {}'.format(token)
      }
    
      response = requests.request("DELETE", url, headers=headers)
      return response
    ```

    This function takes the recording from the `call_id` parameter and deletes the call recording. In this example, you are setting `account_id` to `self`.

2. Loop though the call recordings from the `get_company_call_recordings()` function you wrote and get the recording's `call_id`. You will pass in `call_id` into your `delete_call_recording()` function to delete the recording.

    ```python
    for recording in recordings["_embedded"]["recordings"]:
      call_id = recording["id"]
      response = delete_call_recording(access_token, call_id)
      print(response)
    ```

    You get the recording `id` from the `recordings` list, then pass that `call_id` to the `delete_call_recording` function. If successful, the response will be an empty 204 response.

## Delete On Demand Call Recordings

Deleting on-demand call recordings is almost the same as deleting call recordings; however, you will use the `call_recordings` API.

As before, you must list all the on-demand recordings after a given date.

1. Get a list of on-demand call recordings using this function:

    ```python
    on_demand_recordings = []
    def on_demand_call_recordings(token, account_id="self", user_id="self", order="start%3ADESC",page=1, page_size=10, start_date=None, end_date=None):
      url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/users/{}/call_recordings?order={}&page={}&page_size={}".format(account_id, user_id, order, page, page_size)
      if start_date:
        url = url + "&start:gte="+start_date

      if end_date:
        url = url + "&start:lte="+end_date

      headers = {
        'Accept': 'application/json',
        'Authorization': 'Bearer {}'.format(token),
      }

      response = requests.request("GET", url, headers=headers).json()
      if "_embedded" in response:
        on_demand_recordings.extend(response["_embedded"]["recordings"])

      if "total_pages" in response:
        if page < response["total_pages"]:
          page = page + 1
          on_demand_call_recordings(token, account_id, user_id, order,page, page_size, start_date, end_date)

      return on_demand_recordings
    ```

    Here, you are calling the `call_recording` API and passing the following parameter:

    | Key | Description |
    | --- | ----------- |
    | `account_id`      | The Vonage Business Communications account ID. You can use `self` to refer to the authenticated user's account. |
    | `user_id`      | The user ID. You can use `self` to refer to the authenticated user. |
    | `page`      | The number of pages to request. |
    | `page_size`      | The requested page size. |
    | `order`      | The order of the returned call recordings. |
    | `start:gte`      | Filter records by start date (greater than or equal to). |

2. For the purposes of this exercise, generate a date 7 days in the past and use that for the `start_date` parameter:

    ```python
    import datetime
    import urllib.parse
    today = datetime.datetime.now()
    last_week = datetime.timedelta(days = 7)
    date_diff = today - last_week
    encoded_date = urllib.parse.quote_plus(date_diff.strftime('%Y-%m-%dT00:00:00+0000'))
    ```

3. Write a function that calls the `company_call_recordings` API to delete the recording by `call_id`:

    ```python
    def delete_on_demand_recording(token, call_id, account_id="self", user_id="self"):
      url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/users/{}/call_recordings/{}".format(account_id, call_id)

      headers = {
        'Accept': 'application/json',
        'Authorization': 'Bearer {}'.format(token)
      }

      response = requests.request("DELETE", url, headers=headers)
      return response
    ```

4. Loop through the recordings and write a function to delete the on demand call recording using the `call_id`:

    ```python
    access_token = get_token()["access_token"]
    recordings = on_demand_call_recordings(access_token, start_date=encoded_date)

    for recording in recordings["_embedded"]["recordings"]:
      call_id = recording["id"]
      duration = int(recording["duration"])
        response = delete_on_demand_recording(access_token, call_id)
        print(response)
    ```

In the next step, you will create a CRON job to automatically delete the call recordings every week so you will not have to do it manually.
