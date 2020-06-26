---
title: Create a local server
description: In this step you learn how to create a local server using an ExpressJS application.
---

# Create a local server using an ExpressJS application

To use an ExpressJS application: 

1. Create a new application using `npm init`.
2. Install the ExpressJS library by using `npm install express --save`
3. Write the code:
    
   ```javascript
    const express = require('express')
    const app = express()
    const port = 3000
    app.post('/webhook', function(req, res, next) {
     console.log(req.body)
     res.send(200)
    });
    app.listen(port, () => console.log(`Example app listening at http://localhost:${port}`))
   ```
4. To start your application, run the following command:

    `node app.js`

Your application will now print the events to the console when a call is made or received. 

> Note: Make sure the port you have specified (`300`) is the same port you use when creating your ngrok URL.
