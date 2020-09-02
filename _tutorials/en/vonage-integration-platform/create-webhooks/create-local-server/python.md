---
title: Create a local server
description: In this step you learn how to create a local server using a Python application.
---

# Create a local server using Python application

To use a Flask app

1. Create a virtual environment. Python 3 comes with [`venv`](https://docs.python.org/3/library/venv.html#module-venv) to create virtual environments. In your project directory, create a new virtual environment and activate it.
        
    ```bash
     python3 -m venv venv
     . venv/bin/activate
    ```

2. Install Flask:

    ```bash
     pip install Flask
    ```

3. Create a new file called `app.py` and create the application:
    
    ```python
     from flask import Flask, request, Response
     app = Flask(__name__)
     @app.route('/webhook', methods=['POST'])
     def webhook():
      print(request.get_json())
      return Response(status=200)
    ```

4. Run the application:
    ```bash
     export FLASK_APP=app.py
     flask run -h localhost -p 3000
    ```

This application will run on port 3000, which is the same port you should have configured for ngrok. Now, when you make a call to or receive a call from your Vonage Business Communications number, the application will print the events to the console.
