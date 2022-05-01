---
layout: post
title: Python Selenium
author: john_doe
date: 2022-04-30 10:10:21
---
Selenium is a tool for web application testing.

Selenium tests run directly in the browser, just like a real user is doing. Supported browsers include Edge, Firefox, Safari, Chrome, Opera, etc.

Use python crawler to call selenium to simulate a normal user accessing the browser.

**Installation**

Install selenium:

```
windows: pip install selenium
linux: pip3 install selenium
```

Install [ChromeDriver](https://chromedriver.chromium.org/home), the tool for selenium to use Chrome. By comparing the versions, you can find that each driver version corresponds to Chrome version

Unzip the downloaded ChromeDriver. Place the extracted files in a suitable location.

windows: Move the extracted files to a folder with environment variables configured, such as python's folder.

linux: Move the extracted files to the /usr/local/bin directory.
    
Done.

### Selenium example

As mentioned above, we can use python to import selenium to control the browser for any site.

This means that we can use python to open a browser to automate access.

```python
#! /usr/bin/env python3
from selenium import webdriver
import time

# Create a Chrome object.
driver = webdriver.Chrome()

# Manipulate this object.
driver.get('https://www.youtube.com') # open youtube
time.sleep(2)

# After using, remember to close the browser, otherwise the chromedriver.exe process will remain in memory.
driver.quit() 
```

You can use any browser you want, as long as you have the web driver installed.

```python
# -*- coding: utf-8 -*-
from selenium import webdriver

browser=webdriver.Chrome()
browser=webdriver.Firefox()
browser=webdriver.Safari()
browser=webdriver.Edge()
browser=webdriver.PhantomJS()
```
<br />
### Selenium headless

Chrome running without interface

```python
#! /usr/bin/env python3
'''
    Based on new features released in chrome browser in 2017,
    requires unix versions of chrome above 57,
    windows version of chrome is higher than 58,
    to run without an interface.
'''

from selenium import webdriver
from selenium.webdriver.chrome.options import Options
import time

chrome_opt = Options() # Create an argument object.
chrome_opt.add_argument('--headless') # No interface.
chrome_opt.add_argument('--disable-gpu') # Combine with disable-gpu above.
chrome_opt.add_argument('--window-size=1366,768') # Set the window size, the window size will have an effect.

# Create a Chrome object and pass in the settings.
driver = webdriver.Chrome(chrome_options=chrome_opt) 
       
# Manipulate this object.
driver.get('https://www.youtube.com') # Open youtube.
time.sleep(2)
print(driver.page_source) # Print the loaded page code, proving that the (prove) program is right.
driver.quit() 
```
<br />
### Selenium Driver Operations

Driver object common operations

* get(url): Access the incoming url address in the current browser session, driver.get('https://www.youtube.com').

* close(): Close the current browser window.

* quit(): Quit the webdriver and close all windows.

* refresh(): Refresh the current page.

* title: Get the title of the current page.

* page_source: Get the source code of the current page after rendering.

* current_url: Get the url of the current page.

* window_handles: Get the handles of all windows in the current session.

## Driver finds a single element

You can interact with the elements on the web page.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
#from selenium.webdriver.chrome.service import Service

#wd=webdriver.Chrome())
wd=webdriver.Firefox()
wd.get('https://www.bing.com')

element=wd.find_element_by_id('sb_form_q')  # find input by unique id
element.send_keys('cats')
element.send_keys(u'\ue007') # enter key

#wd.quit()
```

There are many ways to select an element:

| Method                              | Function                          |
|-------------------------------------|-----------------------------------|
| find_element_by_xpath()             | Find by Xpath                     |
| find_element_by_class_name()        | find by class attribute           |
| find_element_by_css_selector()      | find element by css selector      |
| find_element_by_id()                | find by id                        |
| find_element_by_link_text()         | find using ahref link text        |
| find_element_by_name()              | find by unique name               |
| find_element_by_partial_link_text() | find element by partial link text |
| find_element_by_tag_name()          | find by tag name                  |

If an element is not found, an exception can be thrown

```python
# -*- coding: utf-8 -*-
from selenium import webdriver
from selenium.common.exceptions import TimeoutException,NoSuchElementException

browser=webdriver.Chrome()
try:
    browser.get("https://www.youtube.com")
except TimeoutException:
    print("Time out")
try:
    browser.find_element_by_id("hello")
except NoSuchElementException:
    print("No Element")
finally:
    browser.close()
```
<br />
### Selenium show page source

The program below starts a web browser, opens a url and then shows html page source.

```python
#_*_coding: utf-8_*_

from selenium import webdriver
browser=webdriver.Chrome()
browser.get("https://news.ycombinator.com")
print(browser.page_source)
browser.close()
```
<br />
### Driver cookies

You can add a cookie to the current session.

```python
add_cookie(cookie_dict) : 
```

cookie_dict: A dictionary object, must have "name" and "value" keys, optional keys are: "path", "domain", "secure", "expiry".

```python
driver.add_cookie({'name' : 'foo', 'value' : 'bar '})
driver.add_cookie({'name' : 'foo', 'value' : 'bar ', 'path' : '/'})
driver.add_cookie({'name' : 'foo', 'value' : 'bar ', 'path' : '/', 'secure':True})
```

Methods 

```python
Gets a single cookie by name, returns None if there is none.
get_cookie(name): 

Get all cookies, returns a set of dictionaries.
get_cookies(): 

Delete all cookies.
delete_all_cookies(): 

Delete the specified cookie by name.
delete_cookie(name): 
```
<br />
### Selenium wait

#### Explicit waiting

In the process of selenium operating the browser, each time a url is requested, selenium will wait for the page to be loaded before giving the operation permission to our application again.

However, due to the asynchronous loading problem of ajax and various JS codes, we often encounter an error report when using selenium before the operation element is loaded. To solve this problem, Selenium provides several methods of waiting so that we can wait for the element to be loaded and then perform the operation.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.get("http://somedomain/url_that_delays_loading")

try:
    # wait
    element = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "myDynamicElement"))
    )

finally:
    driver.quit()
```

In this example, instead of using find_element_by_* as such to find an element, we use WebDriverWait.

The meaning of the code in the try block is: wait up to 10 seconds before throwing an exception that the element does not exist. During these 10 seconds, WebDriverWait will run the content of until every 500ms by default, while EC.presence_of_element_located in until checks if the element has been loaded, and the checked element is found by By.ID in this way.

That is, within 10 seconds, the default is to check every 0.5 seconds if the element exists and assign the element to the variable element if it exists. If the element still does not exist after 10 seconds, a timeout exception is thrown.

#### Implicit Waiting.

Implicit wait means that when a find_element operation is performed in the webdriver, if the element is not found, it will be polled for a period of time by default.

This value defaults to 0 and can be set as follows.

```python
from selenium import webdriver

driver = webdriver.Chrome()
driver.implicitly_wait(10) 
driver.get("http://somedomain/url_that_delays_loading")
myDynamicElement = driver.find_element_by_id("myDynamicElement")
```

