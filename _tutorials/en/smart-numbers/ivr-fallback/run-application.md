---
title: Run Application
description: Run your demo application
---

# Run the application

Now that the application is updated, you now need to expose a port your local machine is using. A good way to create an accessible URL is to use ngrok.

1. Refer to this tutorial to learn how to [connect your local development server to the Nexmo API using an ngrok tunnel](https://www.nexmo.com/blog/2017/07/04/local-development-nexmo-ngrok-tunnel-dr). 

2. Next, run the application:

    ```bash
    npm start
    ```

3. On a separate device, make a phone call to your Smart Number. When the call is received by the application, it will generate a NCCO that will make a phone call out to the `DEST_NUMBER`. 
