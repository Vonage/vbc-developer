---
title: Download Call Recordings
description: In this step you learn how to create a function to download call recordings
---

## Download Call Recordings

The `get_company_call_recordings` function returns a list of recordings from the account.

Create a function to download the recording:

```python
def download_recording(token, recording_url):
  headers = {
    'Accept': 'application/json',
    'Authorization': 'Bearer {}'.format(token),
  }

  response = requests.request("GET", recording_url, headers=headers)
  return response.content
```

This function takes the recording from the `download_url` parameter and returns the raw data of the recording.

Next, you will configure Boto3 so you can upload the recording to an Amazon S3 bucket.
