---
title: Create an Access Token
description: Learn how to create authenticate to the Vonage Business Communications APIs
navigation_weight: 5
---

#  Authenticating to the Vonage Business Communications APIs

Once you have [created your application](/getting-started/create-an-application), and [subscribed to the Provisioning API](/getting-started/subscribe-to-apis) you are ready to create an access token. Vonage Business Communications APIs APIs use [OAuth](https://oauth.net/2/) for authentication.

## Creating authentication keys

1. Log in to the [Business Communications Developer Portal](https://apimanager.uc.vonage.com/) using your developer credentials and select **Vonage Business Communications** from the platform drop down list.
2. Select **My Applications** in the left-hand navigation menu.
3. On the **My Application** page, locate your application in the table and click the **View** link in the **Actions** column.
4. Select the **Production Keys** tab:

    ![Screenshot showing the Production Keys tab of the My Applications page](/images/vbc/getting-started/production-keys.png)

    > Note: The default grant type is `Code`. The [grant type](https://oauth.net/2/grant-types/) is the method OAuth uses to generate an access token. When you create a production application you will typically want to use this method to authenticate requests. The `Refresh Token` option will create a new token when the current one expires.

5. In the **Callback URL** field, enter a valid callback URL that your application will use to receive the generated token. If you haven't created your application yet, enter `http://localhost` for now and remember to enter the correct URL when you are ready to test it.

    > Note: If you are planning on using password grant type for your application you will not need to use a callback URL to retrieve the token like you would using the authorization code flow. In you are using password grant you can enter `http://localhost`.

6. Click the **Generate Keys** button. This generates the **Consumer Key** and **Consumer Secret** your application will use to request a token.

## Supported Grant Types

Vonage Business Communications supports the following grant types for generating access tokens.

* [Authorization Code](https://oauth.net/2/grant-types/authorization-code/) - The Authorization Code grant type is used by confidential and public clients to exchange an authorization code for an access token. After the user returns to the client via the redirect URL, the application will get the authorization code from the URL and use it to request an access token.
* [Password Grant](https://oauth.net/2/grant-types/password) - The Password grant type is a way to exchange a user's credentials for an access token. 

### When to Use the Password Grant Type?

The Password grant type requires that the application collect the user's password. It is recommended that the Password grant type only be used to enable server-to-server applications where collecting user credentials is not required.

7. Look at the **Endpoint Examples** and **Generating Access Tokens** samples to learn how to request the authentication code and exchange it for an access token:

> In production, you should use the [authorization_code](https://oauth.net/2/grant-types/authorization-code/) grant type (`Code`) and this is the only option shown in the My Applications tab at [apimanager.uc.vonage.com](https://apimanager.uc.vonage.com). The `Code` grant type requires your application to implement a valid callback URL to retrieve the authorization code from the Vonage servers and exchange it for a token. See the Endpoint examples in the My Applications tab to learn how to create the authorization and token requests.

## Authenticating with Authorization Code Grant

The following example shows how to obtain an authorization_code via the authorize end point.
				
```bash
https://api.vonage.com/authorize?scope=openid&response_type=code&redirect_uri=$REDIRECT_URI&client_id=$CONSUMER_KEY
```

* `REDIRECT_URI` - The URL to redirect the user to after authentication.
* `CONSUMER_KEY` - The Consumer Key that you generated in step 5 above

The following example shows how to exchange an authorization code for a token via the token end point

```bash
curl -k -d "grant_type=authorization_code&code=$AUTHORIZATION_CODE&redirect_uri=$REDIRECT_URI" \  
-H "Authorization: Basic $AUTHORIZATION" \
https://api.vonage.com/token
```

* `AUTHORIZATION_CODE` - The code received by the `redirect_uri` after successful login.
* `REDIRECT_URI` - The URL to redirect the user to after the authorization code is exchanged.
* `AUTHORIZATION` - A Base64 encoded token of the application credentials in the format `$CONSUMER_KEY:$CONSUMER_SECRET`.

After exchanging the token you will receive a JSON response with the `access_token` embedded in it. You need this token to use the Account, Extension and User APIs:

```json
{
   "access_token":"1c31afac-175c-3e3a-9d4b-8ecee3980cfa",
   "refresh_token":"dde2a67f-d99f-3f03-810b-1fcae59245de",
   "scope":"default",
   "token_type":"Bearer",
   "expires_in":86400
}
```

## Authenticating with Password Grant

All the code snippets in the VBC API documentation use the [password grant type](https://oauth.net/2/grant-types/password) instead of the recommended `authorization_code` to make them easy to run. This grant type does not require you to implement a callback URL. Instead, you provide your VBC user name and password to request a token.

Replace the following placeholders in the example with your own values:

* `VBC_USERNAME` - Your Vonage Business Communications user name
* `VBC_PASSWORD` - Your Vonage Business Communications password
* `CONSUMER_KEY` - The Consumer Key that you generated in step 5 above
* `CONSUMER_SECRET` - The Consumer Secret that you generated in step 5 above

> Note: When using password grant, you will need to append `@vbc.prod` to your username. 

```bash
curl -k -d "grant_type=password&username=$VBC_USERNAME@vbc.prod&password=$VBC_PASSWORD" \
-d "&client_id=$VBC_CLIENT_ID&client_secret=$VBC_CLIENT_SECRET&scope=openid" \
https://api.vonage.com/token
```

When you run it, you will receive a JSON response with the `access_token` embedded in it. You need this token to use the Account, Extension and User APIs:

```json
{
    "access_token": "abc123-580f-3ace-9a55-9584aaa60842",
    "refresh_token": "abc123-5903-3513-8d27-333daf581837",
    "scope": "openid",
    "id_token": "abc123eyJ4NQiOiJNemcxTnpZeU5UTXhPR1kxTlRNMU1HUTBPR1ZsTVRnM05XRXlZamRpWVdRNE1XSTFemhrWmciLCJraWQiOiJNemcxTnpZeU5UTXhPR1kxTlRNMU1HUTBPR1ZsTVRnM05XRXlZamRpWVdRNE1XSTFNemhrWmciLCJhbGciOiJSUzI1NiJ9..gs7JO2RLPFIld7NXM9gnOy9CYaLs_EYXJJilxX76MFBiidoiG9sIW4RkeHLvDVLyFP1eVd_Pt7000wAr13mcXn-6x6D9oJeAH_Iz8nbzd3vmWDZ8VMHf1SueiAaChfvH0yLvwu02sp-QU-tljGYBTJ8Pr1jWQIG-o39XRrBSMis",
    "token_type": "Bearer",
    "expires_in": 82566
}
```



## Token Expiration

* **Access Token** - Access tokens expire after 24 hours (86400 seconds). After an access token expires you will need to use the refresh token with the refresh grant type to request a new access token.
* **Refresh Token** - Refresh tokens expire after 7 days (604800 seconds). After a refresh token is exchange for an access token the refresh token is no longer usable, and a new refresh token is provided. If the refresh token is not used within the expiration window you will need to reauthenticate.

## Using the Refresh Token
When the access token expires, you will need to regenerate a new access token, using the refresh token. The refresh token will be sent when you first make a request to the `/token` endpoint.

To regenerate the access token:

```bash
curl --location --request POST 'https://api.vonage.com/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'client_id=$VBC_CLIENT_ID' \
--data-urlencode 'client_secret=$VBC_CLIENT_SECRET' \
--data-urlencode 'refresh_token=$REFRESH_TOKEN'
```

Replace the following placeholders in the example with your own values:

* `VBC_CLIENT_ID` - The Client ID from your developer application
* `VBC_CLIENT_SECRET` - The Secret from your developer application
* `REFRESH_TOKEN` - The refresh token from your initial request to retrieve an access token. 

This will return a new access token and refresh token

```json
{
   "access_token": "abc123-580f-3ace-9a55-9584aaa60842",
    "refresh_token": "abc123-5903-3513-8d27-333daf581837",
    "scope": "openid",
    "id_token": "abc123eyJ4NXQiOiJNemcxTnpZeU5UTXhPR1kxTlRNMU1HUTBPR1ZsTVRnM05XRXlZamRpWVdRNE1XSTFNemhrWmciLCJraWQiOiJNemcxTnpZeU5UTXhPR1kxTlRNMU1HUTBPR1ZsTVRnM05XRXlZamRpWVdRNE1XSTFNemhrWmciLCJhbGciOiJSUzI1NiJ9..kpFXRg4qSW9sntliysg-3EGO8KwZ8Vk5jGvOwqq0gJEyPQHL5BQKKrF799VL6Z9OJfCne564N42UWnrQqUmNyU0q8l0td1E3zPA0L5iQQEbaVsbxRf5NCZUwYY9Pb7bXjINCiGF4Xy7wCw2SRpv9iQvg3G68qI5Z8f_25QmxSTY",
    "token_type": "Bearer",
    "expires_in": 86400
}
```

For all API requests going further, you will need to use this access token. When this access token expires, you will need to regenerate a new access token using the latest refresh token.


## Next Steps

Now that you have create an access token, you are ready to [make an API request](/getting-started/make-an-api-request).