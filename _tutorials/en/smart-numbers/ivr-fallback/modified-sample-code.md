---
title: Modifiy the sample code
description: Download the sample code and modify
navigation_weight: 1
---

1. Download the application from Github in order to get started. 
    You will need to have Git installed on your machine. If you are new to git or need to install git, please visit this documentation from [Github](https://docs.github.com/en/github/getting-started-with-github/set-up-git).

    In terminal, insert the following:
    ```bash
    git clone https://github.com/nexmo-community/smart-number-smart-ivr-fallback-demo.git
    cd smart-number-smart-ivr-fallback-demo
    ``` 
2. Next, install the dependencies:
    ```bash
    npm install
    ```

2. Navigate into the cloned repository  and create a new file called `.env`.

3. In the `.env` file, add the following

    ```javascript
    CALLER_ID=''
    DEST_TYPE=''
    DEST_NUMBER=''
    DEST_EXT=''
    DEST_SIP=''
    FALLBACK_TYPE=''
    FALLBACK_NUMBER=''
    FALLBACK_EXT=''
    FALLBACK_SIP=''
    VOICE_NAME=''
    PORT=''
    ```

    Lets go over each environment variable: 

    `CALLER_ID`: The caller ID used for outbound connections.

    `DEST_TYPE`: The type of connection to connect the hotline to.

    `DEST_NUMBER`: The PSTN number to connect. This is used when `DEST_TYPE` is set to `phone`.

    `DEST_EXT`: The Vonage Business Cloud extension number to connect. This is used when `DEST_TYPE` is set to `vbc`.

    `DEST_SIP`: The SIP URI to connect. This is used when `DEST_TYPE` is set to `sip`.

    `FALLBACK_TYPE`: The type of connection to connect the hotline to.

    `FALLBACK_NUMBER`: The PSTN number to connect. This is used when `FALLBACK_TYPE` is set to `phone`

     `FALLBACK_EXT`: The Vonage Business Cloud extension number to connect. This is used when `FALLBACK_TYPE` is set to `vbc`

    `FALLBACK_SIP`: The SIP URI to connect. This is used when `FALLBACK_TYPE` is set to `sip`.

    `VOICE_NAME`: Nexmo voice to use for text-to-speech.

    `PORT`: The port the application should listen on.

5. For this example, we will have our application dial a PSTN number when there is a call on our Smart Number.

    In the `.env`, lets update the following

    ```javascript
    CALLER_ID={a valid PSTN number}
    DEST_TYPE="phone"
    DEST_NUMBER={phone number to dial}
    FALLBACK_TYPE="phone"
    FALLBACK_NUMBER={phone number to dial}
    PORT=3000
    ```