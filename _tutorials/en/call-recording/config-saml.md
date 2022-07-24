---
title: Configure a SAML integration
description: In this step you learn how to configure a SAML integration in your Okta developer account.
---

## Configure a SAML integration

When configuring a SAML integration, you will need to enter the URLs and SP issuer values provided by Vonage Business Communications.

1. Click **Show Advanced Settings** on the **Configure SAML** tab.
2. Enter the following in the specified fields:
    a. **SP (Entity ID)**: vonage-vbc
    b. **Single Sign-On URL**: https://login.auth.vonage.com/accountrecoveryendpoint/saml-translator.jsp?id={customer_account_number}&env=prod&client=Web
    c. **Requestable SSO URL**: https://login.auth.vonage.com/commonauth
    d. **Relay State**: 0
    e. **Logout URL**: https://login.auth.vonage.com/commonauth
    ![Screenshot showing Okta SAML configuration settings on Advanced Settings dialog box](/images/tutorials/okta-config/Okta_5.png)
    ![Screenshot showing Okta SAML configuration settings on Advanced Settings dialog box](/images/tutorials/okta-config/Okta_6.png)
3. On the **Feedback** tab, select the **I'm an Okta customer adding an internal app** radio button.
    ![Screenshot showing Feedback tab in Okta SAML configuration settings](/images/tutorials/okta-config/Okta_7.png)
4. Click **Finish**.
    You will see the following propmt once you are finished creating an application. The message states **SAML 2.0 is not configured until you complete the setup instructions.**
    ![Screenshot showing Feedback tab in Okta SAML configuration settings](/images/tutorials/okta-config/Okta_8.png)
5. Click **View Setup Instructions**.
    The setup instructions window opens.
    ![Screenshot showing Feedback tab in Okta SAML configuration settings](/images/tutorials/okta-config/Okta_9.png)
6. In a separate browser window, open the Vonage Business Communications [Single Sign-on Settings](https://admin.vonage.com/management/m/ssoSettings) page.
7. Enter the values from Okta into the appropriate fields on the Vonage Business Communications Single Sign-on Settings page:
    | Okta Setting                             | VBC Setting                                                   |
    |------------------------------------------|---------------------------------------------------------------|
    | Identity Provider Sign-on URL            | Sign-in page URL                                              |
    | Identity Provider Issuer                 | Entity ID                                                     |
    | Identity Provider Single Logout URL      | Sign-out page URL                                             |
8. Upload your X509 certificate from the previous section via **Upload Certificate**.
9. Once you have entered all the necessary values in the appropriate fields, click **Save**.

> Note: To assign users to your application, follow [these instructions](https://developer.okta.com/docs/guides/saml-application-setup/assign-users-to-the-app/)

> Note: To enable a flexible username format (other than email addresses), refer to [these instructions](https://help.okta.com/en/prod/Content/Topics/Directory/eu-profile_editor_tasks.htm)
