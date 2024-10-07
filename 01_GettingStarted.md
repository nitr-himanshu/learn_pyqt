# Getting started

## Creating an application

```python
from PyQt6.QtWidgets import QApplication, QWidget
import sys

app = QApplication(sys.argv)
window = QWidget()
window.show()
app.exec()
```

<img src="img/01_firstApp.png" alt="screenshot" width="400"/>

- You need one (and only one) QApplication instance per application.
- Pass in sys.argv to allow command line arguments for your app. if not needed, QApplication([]) works too.
- Qt widget (windows) will be our window.
- Windows are hidden by default. To show call method show().
- Widgets without a parent are invisible by default. So, after creating the window object, we must always call .show() to make it visible.
- app.exec() starts the event loop.
- Untill exit, the event loop won't stop.
- In Qt all top level widgets are windows -- that is, they don't have a parent and are not nested within another widget or layout.

## What is a window?

- Holds the user-interface of your application - Every application needs at least one (...but can have more)
- Application will (by default) exit when last window is closed

## What's the event loop?

- The core of every Qt Applications is the QApplication class.
- Every application needs one — and only one — QApplication object to function.
- This object holds the event loop of your application — the core loop which governs all user interaction with the GUI.
<img src="img/02_eventLoop.png" alt="Event loop" width="400"/>
