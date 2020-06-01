---
title: Delete Company Call Recordings / On Demand Call Recordings by date
navigation_weight: 1
products: call-recording
languages:
    - Python
---

# Delete Company Call Recordings / On Demand Call Recordings by date

In this tutorial, you will learn how to delete call recordings by a certain date. This will help minimize storage costs for call recordings that you may not need. This could also be useful if you want to remove recordings for security purposes.
The Call Recording API lets you retrieve all call recordings and allows for filtering by call duration, extension, caller_id, direction(inbound or outbound) and more. Please have a look at the api reference to view all the possible filters.

In this example, we will query for the last 7 days of recordings. We'll be using a python script to query for the call recordings and for each recording, we'll delete the recording.

Python is the language used to build the following example; however, you can use any language with which you are most comfortable. The following Python library is used in this example:

* [requests](https://requests.readthedocs.io/en/master/)

## Prerequisites

Before you can get started, you will need to have a Vonage Developer account. If you do not have a Vonage Developer account, please use this [guide](_documentation/en/concepts/guides/create-a-developer-account.md) to setup and create your account.

After you have an account, you will need to do the following using these guides:

* [Create an application](_documentation/en/concepts/guides/create-an-application.md).
* [Subscribe to the API's](_documentation/en/concepts/guides/create-an-application.md).

For this example, you will need to Subscribe to the [Call Recording API](_documentation/en/call-recording/overview.md).

## Authentication

After creating an application and subscribing to the Call Recording API, you will now need to log-in using your Vonage Business Cloud credentials. This example application uses the Requests library to call the `/api/accounts/` API. Check out the [Making an API Request guide](_documentation/en/concepts/guides/make-an-api-request.md) for more details.

Next, we'll create a function that requests the `/api/accounts` API to generate an access token.

```python
def get_token():
  url = "https://api.vonage.com/token"
  payload = 'grant_type=password&username={}&password={}&client_id={}&client_secret={}'.format(USERNAME, PASSWORD, CLIENT_ID, SECRET)
  headers = {
    'Content-Type': 'application/x-www-form-urlencoded'
  }

  response = requests.request("POST", url, headers=headers, data = payload)
  return response.json()
  ```

To run this function, you will need to pass in the following:

* `USERNAME` - Vonage Business cloud username. Be sure to append `@vbc.prod` to the username. `firstname.lastname@vbc.prod`.
* `PASSWORD` - Vonage Business Cloud password.
* `CLIENT_ID` - The client id of your Vonage Developer application.
* `SECRET` - The secret to your Vonage Developer application.

After running this function, you should see the following response:

```json
{'access_token': 'abc123-xxxxx-xxxxx',
'expires_in': 9999,
'refresh_token': 'def456-xxxx-xxxx',
'scope': 'default',
'token_type': 'Bearer'}
 ```

## Get Call Recordings

Before we call the company_call_recordings API, we'll need to pass in a date string that is in the past. For this example, we will create a date that is 7 days in the past
```Python
import datetime
import urllib.parse
today = datetime.datetime.now()
last_week = datetime.timedelta(days = 7)
date_diff = today - last_week
encoded_date = urllib.parse.quote_plus(date_diff.strftime('%Y-%m-%dT00:00:00+0000'))
```
Here, we get the current date using `datetime.datetime.now()`, then use `datetime.timedelta()` function to create a date that is `days` in the past. Here we use `7`. Next, we'll subtract the current date from the date 7 days in the past, to get our date. Finally, we use `strftime()` to convert the date object into a string. We've set the time to `00:00:00+0000`, which means we are getting the date at midnight UTC.
Before we can pass the date into the Call Recordings API, we need to urlencode the date using `urllib.parse.quote_plus()`.

Next, we'll request the Call Recording API and use the `access_token` that was returned from the `get_token()` function. This will return a JSON response of the call recordings. We'll then pass in the date `encoded_date` into this function

```python
import requests
def company_call_recordings(token, account_id="self", order="start%3ADESC",page=1, page_size=10, start_date=None, end_date=None):
  url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/company_call_recordings?order={}&page={}&page_size={}".format(account_id, order, page, page_size)
  if start_date:
    url = url + "&start:gte="+start_date

  if end_date:
    url = url + "&start:lte="+end_date

  headers = {
    'Accept': 'application/json',
    'Authorization': 'Bearer {}'.format(token),
  }

  response = requests.request("GET", url, headers=headers)
  return response.json()
```

Here, we are calling the `company_call_recordings/v1/api/` and passing the following parameter:

* `account_id` - The Vonage Business Communications account ID. You can use `self` to refer to the authenticated user's account.
* `page` - The number of pages to request.
* `page_size` - The requested page size.
* `order` - The order of the returned call recordings
* `start:gte` - Filter records by start date (greater than or equal to)

We could also pass in `start:lte` which would return records less than the given date.

Once we get a list of call recordings, we will loop though each recording delete it. Before doing this, make sure you have a backup of the recordings. Take a look at the [delete_recordings_by_date](/use-cases/call-recording-to-s3) use case to save recordings to Amazon S3.

## Delete Call Recordings

The `get_company_call_recordings()` function returns a list of recordings from the account. Next, we'll create a function to delete the recording by its recording id.

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

This function takes the recording from the `call_id` parameter and will delete the call recording. For this example, we are setting `account_id` to `self`.

Next, lets loop though the call recordings from the `get_company_call_recordings()` function we wrote and get the recordings `call_id`. We will pass in `call_id` into our `delete_call_recording()` function to delete the recording.

```python
for recording in recordings["_embedded"]["recordings"]:
  call_id = recording["id"]
  response = delete_call_recording(access_token, call_id)
  print(response)
```
Here, we get the recording `id` from the `recordings` list, then pass that call_id to the `delete_call_recording` function. If successful, the response will be a empty 204 response.

## Delete On Demand Call Recordings

Deleting on-demand call recordings will be almost the same as deleting call recordings, however, we will be using the `call_recordings` API.

As before, we need to list all the on-demand recordings after a given date. First, we need get a list of on-demand call recordings using this function.

```python
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

  response = requests.request("GET", url, headers=headers)
  return response.json()
```

Here, we are calling the `call_recording` API and passing the following parameter:

* `account_id` - The Vonage Business Communications account ID. You can use `self` to refer to the authenticated user's account.
* `user_id` - The user ID. You can use `self` to refer to the authenticated user.
* `page` - The number of pages to request.
* `page_size` - The requested page size.
* `order` - The order of the returned call recordings
* `start:gte` - Filter records by start date (greater than or equal to)

Next, we'll generate a date 7 days in the past and use that for the `start_date` parameter.
```Python
import datetime
import urllib.parse
today = datetime.datetime.now()
last_week = datetime.timedelta(days = 7)
date_diff = today - last_week
encoded_date = urllib.parse.quote_plus(date_diff.strftime('%Y-%m-%dT00:00:00+0000'))
encoded_date
```
Next, we'll write a function that calls the `company_call_recordings` API to delete the recording by call_d

```Python
def delete_on_demand_recording(token, call_id, account_id="self", user_id="self"):
  url = "https://api.vonage.com/t/vbc.prod/call_recording/v1/api/accounts/{}/users/{}/call_recordings/{}".format(account_id, call_id)

  headers = {
    'Accept': 'application/json',
    'Authorization': 'Bearer {}'.format(token)
  }

  response = requests.request("DELETE", url, headers=headers)
  return response
```

We'll then loop though the recordings and write a function to delete the on demand call recording using the `call_id`
```Python
access_token = get_token()["access_token"]
recordings = on_demand_call_recordings(access_token, start_date=encoded_date)

for recording in recordings["_embedded"]["recordings"]:
  call_id = recording["id"]
  response = delete_on_demand_recording(access_token, call_id)
  print(response)
```

## CRON Job
The final step is to delete the call recordings every week using a CRON job. This way, we will not have to run these functions manually. A CRON is way to run scripts periodically at fixed times, dates, or intervals.
You can create a CRON job locally by first running `crontab -e` on a OSX/Linux based system.
For a Windows machine:
* Log on with a privileged account, e.g. Administrator
* Go to Start > Control Panel > System and Security > Administrative Tools > Task Scheduler
* In the right panel click on Create Basic Task

Our CRON job will run every 7 days. An here is what the CRON job will look like
```bash
* * 7 * * delete_recordings.py >/dev/null 2>&1
```
The [`delete_vbc_recordings.py`](https://gist.github.com/tbass134/03342bf8bd0c047ca54cc50906e3b828) is a script that will delete both the call recordings and on demand call recordings that are older than 7 days.
Take a look at https://crontab-generator.org/ to create your own CRON job.


## Conclusion

Here, we've shown how to create a simple CRON job script to delete VBC call recordings and on demand call recordings every 7 days. You can have a look at this [gist](https://gist.github.com/tbass134/03342bf8bd0c047ca54cc50906e3b828)  to see the full code example.
