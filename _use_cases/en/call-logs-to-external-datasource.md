---
title: Save call logs to external datasource
navigation_weight: 1
products: call-logs
languages:
    - Python
---

# Save call logs to external datasource

In this tutorial, we will go over how to save your call logs into an external datasource in order to gain understanding of your data. There are many places in which call logs can be saved(google sheets, excel and so on). For this example, we'll save our call logs into a JSON list, which can be used as a datasource for Tableau.

## Prerequisites

Before you can get started, you will need to have a Vonage Developer account. If you do not have a Vonage Developer account, please use this [guide](_documentation/en/concepts/guides/create-a-developer-account.md) to setup and create your account.

After you have an account, you will need to do the following using these guides:

* [Create an application](_documentation/en/concepts/guides/create-an-application.md).
* [Subscribe to the API's](_documentation/en/concepts/guides/create-an-application.md).

For this example, you will need to Subscribe to the [Reports API](_documentation/en/reports/overview.md).

## Authentication

After creating an application and subscribing to the Reports API, you will now need to log-in using your Vonage Business Cloud credentials. Check out the [Making an API Request guide](_documentation/en/concepts/guides/make-an-api-request.md) for more details.

Next, we'll create a function that requests the `/token` API to generate an access token.

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

 ## Call Logs API
 The next step is to pull the list of calls from the call logs api. We can use this function to return a list of calls by a start date and end dates. If there are more results than the number of items we have requested using the page_size parameter, this function will retrieve those other pages as well.

 ```Python
 results = []
def get_reports(token, account_id, start_date, end_date, order="asc", page_size=10, page=1):
  url = "https://api.vonage.com/t/vbc.prod/reports/v1/accounts/{}/call-logs?start:gte={}&start:lte={}&page_size={}&page={}&order={}".format(account_id, start_date, end_date, page_size, page, order)
  headers = {
    'Accept': 'application/json',
    'Authorization': 'Bearer {}'.format(token),
  }

  response = requests.request("GET", url, headers=headers).json()
  if "_embedded" in response:
    results.extend(response["_embedded"]["call_logs"])

  if page < response["total_page"]:
    page = page + 1
    get_reports(token, account_id, start_date, end_date, page_size=page_size, page=page)

  return results
```

Next, we'll need to create a start and end date to pass into the function. The start date will be the current day and the end date will be 1 day in the past.

```python
import datetime
from datetime import timedelta
today = datetime.datetime.now()
today_str = today.strftime('%Y-%m-%d 00:00:00')

yesterday = today - timedelta(days = 1)
yesterday_str = yesterday.strftime('%Y-%m-%d 23:59:59')

access_token = get_token()["access_token"]
reports = get_reports(access_token,account_id={YOUR_ACCOUNT_ID}, start_date=today_str, end_date=yesterday_str)
```
This will generate the start_date which is the current day at midnight, and the end_date which one day in the past. We will then call the `get_reports` function to return a list of calls between those 2 dates. Next, we'll then need to create a JSON file that contains a list of these logs.
```Python
import json

def write_json(data, filename='data.json'):
    with open(filename,'w') as f:
        return json.dump(data, f)

def read_json(filename='data.json'):
  try:
    with open(filename) as json_file:
      return  json.load(json_file)
  except IOError:
    return []

data = read_json()
data.extend(reports)
write_json(data)
```

Here, we create 2 functions to read and write to a JSON file. We then read our JSON file. If the file does not exist, we return a empty list(`[]`). Next, we need to add our calls logs into the JSON file using the `extend()` function. Finally, we need to load this list back into the json file. For every day that we run this function, we will append the latest call logs in the JSON file.

## CRON Job
The final step is to run our [script](https://gist.github.com/tbass134/86965b64e69b05720d932d4e708e3c01) every day using a CRON job. This way, we will not have to run these functions manually. A CRON is way to run scripts periodically at fixed times, dates, or intervals.
You can create a CRON job locally by first running `crontab -e` on a OSX/Linux based system.
For a Windows machine:
* Log on with a privileged account, e.g. Administrator
* Go to Start > Control Panel > System and Security > Administrative Tools > Task Scheduler
* In the right panel click on Create Basic Task

Our CRON job will look like this:
`* 0 * * * get_call_logs.py >/dev/null 2>&1`
This will run everyday at midnight. To create your own CRON job, check out https://crontab-generator.org/

## Import into Tableau
For this example, we will be using Tableau to generate a dashboard from our call log data. It will look something like this:
![](/images/use_cases/call-logs-to-external-datasource/tableau_dashboard.png)

First, in Tableau, click `Connect To Data` and under `To a file`, click `JSON file`
![](/images/use_cases/call-logs-to-external-datasource/tableau_connect_to_json.png)
Next, locate the JSON file that contains the calls logs. You can optionally select a few columns. Then navigate to `Sheet 1` to view your data.

Next, go to `Sheet 1` and in the `Folders` section, Right click on the `End` parameter and set `Change Data Type` to `Date`
![](/images/use_cases/call-logs-to-external-datasource/tableau_change_end_parmeter.png)

Then, drag the `End` parameter to the Columns section. Next, right click on the `End` parameter and change to `Day`.
Then, drag the `Count` parameter under the `Measured Names` section to the row. You should then see a line chart for the number of calls by day.

As our CRON job runs everyday, our Tableau dashboard will update itself with the new call logs. Just remember to save the JSON in the same location as where you originally added the datasource for Tableau

## Conclusion
In this example, we have seen how to create a function that returns a list of calls logs for a given day. Pushing this data is a dashboard like Tableu will be able to help your team Analyze your call traffic. Our dashboard just shows the number of calls every day, but you can customize it to shown number of inbound / outbound calls, average cost per day, average lenght of calls, and much more. 
