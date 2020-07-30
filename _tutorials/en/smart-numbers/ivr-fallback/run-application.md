---
title: Run Application
description: Run your demo application
---

1. After we update our application, we'll now need to expose a port on our local machine using. A good way to create an accessible URL is to use [ngrok](https://www.nexmo.com/blog/2017/07/04/local-development-nexmo-ngrok-tunnel-dr). 

2. Next, run the application

    ```bash
    npm start
    ```

3. On a separate device, make a phone call to your Smart Number. When the call is received by the application, it will generate a NCCO that will make a phone call out to the `DEST_NUMBER`. 



