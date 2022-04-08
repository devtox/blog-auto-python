---
layout: post
title: A Brief Introduction to PyQt
author: john_doe
date: 2022-04-08 21:06:30
intro_paragraph: PyQt is a Python binding of the Qt user interface library,
  using Qt's C++ API. It supports all major desktop platforms.
---
PyQt is a set of Python bindings for The Qt cross-platform GUI toolkit. These bindings allow Python programmers to create GUI applications that run on Windows, MacOS X and Linux.

PyQt applications look and feel like native, but with all the power of the full Qt library available at their fingertips.

**What can you do with PyQt?**

Create sophisticated *graphical user interfaces* with Python. 

Use Qt's signal/slot mechanisms or Python's own full-featured OO system to connect your functions to GUI events.

**How do I start?**

This workshop will walk you through the basics of how to create and deploy a GUI application with Python and PyQt. 

We'll cover getting an environment set up, learning about widgets, and what you need to know about events. 

### Installation

```bash
apt install python3-pyqt5
```


A basic program in PyQt5

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget
 
def show_w():
    # All PyQt5 applications must create an application (Application) object.
    # The argument is a list of arguments from the command line. (sys.argv)
     app = QApplication(sys.argv) 
    
    # The Qwidget component is the base class for all user interface classes in PyQt5. We give QWidget with a default constructor.
    w = QWidget() 
    
    # The resize() method resizes the widget component. It is now 500px wide and 500px high.
    w.resize(500, 500) 

    # The move() method moves the widget component to a location that is the x=500,y=200 coordinates on the screen.
    w.move(500, 100) 

    # Sets the title of the window. This title is displayed in the title bar.
    w.setWindowTitle('Simple') 

    # show() method displays the widget on the screen. a widget object is created in memory for the first time here and is displayed on the screen afterwards.
    w.show() 
 
    # The application enters the main loop. At this point, event handling begins to execute. The main loop is used to receive events triggered from the window
    sys.exit(app.exec_()) 
  
    sys.exit()
 
if __name__ == '__main__':
    show_w()
```

