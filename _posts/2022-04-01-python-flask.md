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

<br />

You can then open *http://127.0.0.1:5000* and you should see the output. Besides text output, you can return html output in the function.

### Routing

 A route is a url, and we will use the url to run the correct function to handle it.

It is one of the key concepts in Flask. In layman’s terms, a route is just a URL pattern that gets handled by a view function. Pretty simple stuff.

You can use Flask to create simple HTTP routes to your application. By defining routes, you can use the same URLs for different actions. 

You have user a route before, namely the index route. When you open the index page in your web browser, it calls the hello function and returns the function data.

Every page in your website will pass through the Request-Response model. If you are confused, don’t worry, there is a simple way to do so.

```python
@app.route("/")
def hello():
    return "Hello, World!"
```

That's all it takes to create the index route. If you open the webpage in your web browser, you will see the text returned. 

This can be useful to keep things consistent and is a common pattern in several web frameworks.

If you have want a page to show photos, you could have a route

```python
@app.route("/photos")
```

<br />
This lets you call /photos in your web browser. But you need to map it to a function that returns data. Something like this:

```python
@app.route("/photos")
def photos():
    return "My photos!"
```

So in order to know how to handle each request, Flask needs a way to identify what the user wants. In programming terms, this is called identification. (Identification is the process of determining characteristics of something.) 

In Flask, this identification process comes in two ways: URL Routing and View Templates. The combination of these two features creates an interaction between user and server that leads to something called Flask-HTML-Response. 
<br />



![routing in the real world](/assets/img/uploads/flask-route.png "Flask routing")

<br />

### Dynamic routes

So, we have covered the basics of how to define and name routes, which is great for applications with a small, fixed set of routes. But what about applications that are more dynamic and may have many different routes?

Flask can handle this too. By using the code below, you create a dynamic route where the last parameter can hold any value.

```python
@app.route('/company/<employee>')
def show_employee(name):
    return f'Hello {name} !'
```

<br />
You can also do dynamic numbers in routing.

```python
@app.route('/product/<int:id>')
def show_product(id):
    return f'Product id {id}'
```

<br />

### Templates

A template is a web page with variables and expressions. The web page itself can be defined in html but with Flask, it uses an additional template language called Jinja2.

A function can return a template. The variables passed by the function are then automatically shown in the web page.

A simple example is show below

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/hello/')
def hello(user):
   return render_template('hello.html', name = 'alice')

if __name__ == '__main__':
   app.run(debug = True)
```

Then the template can simply output the variable name

{% raw %}

```html
<!doctype html>
<html>
   <body>
         <h1>Hello {{ name }}!</h1>
   </body>
</html>
```

{% endraw %}

The function hello() return the *template* `hello.html`. It uses the variable marks inside the template. The url to be used is a dynamic url, `/hello/<score>`.

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/hello/<int:score>')
def hello(score):
   return render_template('hello.html', mark = score)

if __name__ == '__main__':
   app.run(debug = True)
```

The template can then look like this:

{% raw %}

```python
<!doctype html>
<html>
   <body>
      {% if mark>60 %}
         <h1> You passed the exam!</h1>
      {% else %}
         <h1>You fail the exam</h1>
      {% endif %}
   </body>
</html>
```

{% endraw %}

The template contains an if statement, the output depends on the variable passed in the url. The variable gets passed from the url, to the function and then to the template.

Besides showing variables directly and if statements, you can also use for loops. So that sums up the template language.

There's a lot more to Python Flask, but these are the absolute basics.
<br />