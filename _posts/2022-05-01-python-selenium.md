---
layout: post
title: Python Selenium
author: john_doe
date: 2022-05-01 10:10:21
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

## Selenium example

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

## Selenium headless

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