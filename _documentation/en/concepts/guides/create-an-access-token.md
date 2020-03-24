---
title: Create an Access Token
description: Authenticating to the Vonage Business Communications APIs
navigation_weight: 5
---

#  Authenticating to the Vonage Business Communications APIs

Once you have [created your application](/concepts/guides/create-application), and [subscribed to the Provisioning API](/account-api/overview) you are ready to create an access token. Vonage Business Communications APIs APIs use [OAuth](https://oauth.net/2/) for authentication.

## Creating authentication keys

1. Log into [developer.vonage.com](https://developer.vonage.com/store).

2. Select "My Applications" in the left-hand navigation menu.

3. On the "My Application" page, locate your application in the table and click the "View" link in the "Actions" column.

4. Select the "Production Keys" tab:

  ![Screenshot showing the Production Keys tab of the My Applications page](/assets/images/vbc/production-keys.png)

  > Note: The default grant type is `Code`. The [grant type](https://oauth.net/2/grant-types/) is the method OAuth uses to generate an access token. When you create a production application you will typically want to use this method to authenticate requests. The `Refresh Token` option will create a new token when the current one expires.

5. In the "Callback URL" field, enter a valid callback URL that your application will use to receive the generated token. If you haven't created your application yet, enter `http://localhost` for now and remember to enter the correct URL when you are ready to test it.

	> Note: If you are planning on using password grant type for your application you will not need to use a callback URL to retrieve the token like you would using the authorization code flow. In you are using password grant you can enter `http://localhost`.

6. Click the "Generate Keys" button. This generates the "Consumer Key" and "Consumer Secret" that your application will use to request a token.

## Supported Grant Types

Vonage Business Communications supports the following grant types for generating access tokens.

* [Authorization Code](https://oauth.net/2/grant-types/authorization-code/) - The Authorization Code grant type is used by confidential and public clients to exchange an authorization code for an access token. After the user returns to the client via the redirect URL, the application will get the authorization code from the URL and use it to request an access token.
* [Password Grant](https://oauth.net/2/grant-types/password) - The Password grant type is a way to exchange a user's credentials for an access token. 

### When to Use the Password Grant Type?

The Password grant type requires that the application collect the user's password. It is recommended that the Password grant type only be used to enable server-to-server applications where collecting user credentials is not required.

7. Look at the "Endpoint Examples" and "Generating Access Tokens" samples to learn how to request the authentication code and exchange it for an access token:

> In production, you should use the [authorization_code](https://oauth.net/2/grant-types/authorization-code/) grant type (`Code`) and this is the only option shown in the My Applications tab at [developer.vonage.com](https://developer.vonage.com/store). The `Code` grant type requires your application to implement a valid callback URL to retrieve the authorization code from the Vonage servers and exchange it for a token. See the Endpoint examples in the My Applications tab to learn how to create the authorization and token requests.

## Authenticating with Authorization Code Grant

The following example shows how to an obtain an authorization_code via the authorize end point.
				
```code_snippets
https://api.vonage.com/authorize?scope=openid&response_type=code&redirect_uri=$REDIRECT_URI&client_id=$CONSUMER_KEY
```

* `REDIRECT_URI` - The URL to redirect the user to after authentication.
* `CONSUMER_KEY` - The Consumer Key that you generated in step 5 above

The following example shows how to exchange an authorization code for a token via the token end point

```code_snippets
curl -k -d "grant_type=authorization_code&code=$AUTHORIZATION_CODE&redirect_uri=$REDIRECT_URI" \  
	-H "Authorization: Basic $AUTHORIZATION" \
	https://api.vonage.com/token`
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

```code_snippets
source: '_examples/vonage-business-cloud/vbc-apis/general/authenticate-password'
```

When you run it, you will receive a JSON response with the `access_token` embedded in it. You need this token to use the Account, Extension and User APIs:

```json
{
   "access_token":"1c31afac-175c-3e3a-9d4b-8ecee3980cfa",
   "refresh_token":"dde2a67f-d99f-3f03-810b-1fcae59245de",
   "scope":"default",
   "token_type":"Bearer",
   "expires_in":86400
}
```

## Token Expiration

* **Access Token** - Access tokens expire expire after 24 hours (86400 seconds). After an access token expires you will need to use the refresh token with the [Refresh grant type](https://oauth.net/2/grant-types/refresh-token/) to request a new access token.
* **Refresh Token** - Refresh tokens expire after 7 days (604800 seconds). After a refresh token is exchange for an access token the refresh token is no longer usable, and a new refresh token is provided. If the refresh token is not used within the expiration window you will need to reauthenticate.

## Next Steps 

Now that you have create an access token, you are ready to [make an API request](/concepts/guides/make-an-api-request).