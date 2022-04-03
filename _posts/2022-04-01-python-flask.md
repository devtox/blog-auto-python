---
layout: post
title: Flask
meta_description: Python Flask introduction, make web apps with Python
author: john_doe
date: 2021-03-01 22:52:00
intro_paragraph: Python Flask is a Python package for developing web
  applications with. It features a built-in development server and a unit test
  integration. Python Flask is used in many large projects.
categories: Web
---
The Python Flask framework allows you to focus mainly on your business logic, with the user interface being automatically generated from templates.

Python is a high-level, general-purpose programming language. Flask is an open source web application framework written in Python. It’s used to create web application prototypes quickly without the need to hook into a specific database or to write raw SQL queries, but you have the option to do so.

The goal of the project is to empower developers with a simple but flexible structure for application development. Features include, but are not limited to:

* Routing
* View Templates
* Configurations
* OAuth 1.0a
* Form Validation
* Extensions  


<br />

### Flask web app

We will use Python Flask to create a very simple web application.

This application will have a single page with a small form that will allow us to track visitors to this page.

We will perform the following tasks:

1. Install a recent version of Python and pip.
2. Create a new project folder (directory).
3. Install Flask in the project
4. Create a new Python file inside our project directory.
5. Write the first lines of code in our Python file to create a web server.
6. Test if our web server works correctly by visiting it through our browser. 

<br />

**Install Python and pip**

You can install Python and pip using these commands:

```bash
$ sudo apt-get install python3 python-env  # linux
% brew install python3  # apple mac os
```

<br />

**Create new project**

The next step is to create a new project environment. 

```bash
% mkdir flask-hello-world   # create project folder
% cd flask-hello-world      # enter project folder
% python3 -m venv venv      # create virtual environment(venv)
```

Then you need to activate your project environment

```bash
% source venv/bin/activate     # For Apple/Linux users
> venv\Scripts\activate        # For Windows users
```

<br />

**Install Flask**

You can install Flask using the pip package manager.

```bash
pip install -U Flask
```

<br />

**Create a Python file inside the src directory**

Create a new directory for your code, 

```bash
cd venv
mkdir src
cd src
touch hello.py
```

<br />

**Create the program for the web server**

The file hello.py can contain the code below

```bash
# save this as app.py
from flask import Flask

# create new app
app = Flask(__name__)

# if the / route is opened in the browser, return text
@app.route("/")
def hello():
    return "Hello, World!"

# the start of the application
if __name__ == "__main__":
    app.run()
```

<br />

### Test if our web server works 

Now run the program with the command

```bash
python3 hello.py
```

<br />

It should output that it started the web server

```bash
$ python3 hello.py 
 * Serving Flask app 'hello' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
```

You can then open *http://127.0.0.1:5000* and you should see the output. Besides text output, you can return html output in the function.