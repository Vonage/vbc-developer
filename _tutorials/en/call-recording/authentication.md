---
title: Authentication
description: In this step you learn how to generate an access token with the Accounts API 
---

# Authentication

Now that you have created an application and subscribed to the Call Recording API, you must generate an access token.

1. Log-in using your Vonage Business Cloud credentials. This example application uses the Requests library to call the `/api/accounts/` API. 

    > Refer to the [Making an API request guide](/getting-started/make-an-api-request) for more details.

2. Create a function that requests the `/api/accounts` API to generate an access token.

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

3. Run the function passing in the following values:

    | Key | Description |
    | --- | ----------- |
    | `USERNAME`      | Vonage Business cloud username. Be sure to append `@vbc.prod` to the username. `firstname.lastname@vbc.prod`. |
    | `PASSWORD`      | Vonage Business Cloud password. |
    | `CLIENT_ID`      | The client id of your Vonage Developer application. |
    | `SECRET`      | The secret to your Vonage Developer application. |

    After running this function, you should see the following response:

    ```json
    {'access_token': 'abc123-xxxxx-xxxxx',
    'expires_in': 9999,
    'refresh_token': 'def456-xxxx-xxxx',
    'scope': 'default',
    'token_type': 'Bearer'}
     ```

Next, you will make a GET request to get a list of recordings from the account.
