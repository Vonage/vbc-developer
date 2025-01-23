---
title: Create a VBC integration user
description: Learn how to create a VBC integration user
navigation_weight: 5
---

#  Authenticating to the Vonage Business Communications APIs

To authenticate with VBC APIs you will need a VBC integration user. You will use this user account to create an access token.

## Create a VBC integration user

- Login to VBC with your admin user account
  - [https://admin.vonage.com](https://admin.vonage.com)
- Go to **Phone System > Users**
  - Click **Add New**
    - Enter a first name **API**
    - Enter a first name **USER**
    - Enter a username with your VBC account number, for example: **api_user_999999**
    - Enter an email address
    - Select User Type **Account Administrator**
    - Select **User does not need an extension**
    - Click **save**
- Search for the newly created user and click the **edit** button
  - Click **Update Password**
    - Enter a strong password with a minimum 20 characters, irregular capitalization, special characters, and at least one numeral.
    - Click **update**
- If using SSO on your VBC account
  - Uncheck **Enable single sign-on for this user**
  - Click **save**