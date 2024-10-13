# Toolbars & Menus

## Toolbars

- Toolbars are bars of icons and/or text used to perform common tasks within an application, for which accessing via a menu would be cumbersome.
- Qt uses your operating system default settings to determine whether to show an icon, text or an icon and text in the toolbar. But you can override this by using .setToolButtonStyle.

## QAction

- QAction is a class that provides a way to describe abstract user interfaces.
- with QAction can define a triggered action, and then add this action to both the menu and the toolbar.
- Each QAction has names, status messages, icons and signals that you can connect to (and much more).

## QIcon

- To set icon. We can create a QIcon object by passing the name of the file to the class.

```python
import sys
from PyQt6.QtWidgets import (
    QMainWindow, QApplication,
    QLabel, QToolBar, QStatusBar
)
from PyQt6.QtGui import QAction, QIcon
from PyQt6.QtCore import Qt
class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setWindowTitle("My Awesome App")
        label = QLabel("Hello!")
        label.setAlignment(Qt.AlignmentFlag.AlignCenter)
        self.setCentralWidget(label)
        toolbar = QToolBar("My main toolbar")
        self.addToolBar(toolbar)
        button_action = QAction("Your button", self)
        button_action.setStatusTip("This is your button")
        button_action.triggered.connect(self.onMyToolBarButtonClick)
        toolbar.addAction(button_action)

    def onMyToolBarButtonClick(self, s):
        print("click", s)

app = QApplication(sys.argv)
w = MainWindow()
w.show()
app.exec()
```

## Menus

- To create a menu, we create a menubar we call .menuBar() on the QMainWindow.
- Add a menu on our menu bar by calling .addMenu(), passing in the name of the menu.

```python
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("My App")

        label = QLabel("Hello!")
        label.setAlignment(Qt.AlignmentFlag.AlignCenter)

        self.setCentralWidget(label)

        toolbar = QToolBar("My main toolbar")
        toolbar.setIconSize(QSize(16, 16))
        self.addToolBar(toolbar)

        button_action = QAction(QIcon("bug.png"), "&Your button", self)
        button_action.setStatusTip("This is your button")
        button_action.triggered.connect(self.onMyToolBarButtonClick)
        button_action.setCheckable(True)
        toolbar.addAction(button_action)

        toolbar.addSeparator()

        button_action2 = QAction(QIcon("bug.png"), "Your &button2", self)
        button_action2.setStatusTip("This is your button2")
        button_action2.triggered.connect(self.onMyToolBarButtonClick)
        button_action2.setCheckable(True)
        toolbar.addAction(button_action2)

        toolbar.addWidget(QLabel("Hello"))
        toolbar.addWidget(QCheckBox())

        self.setStatusBar(QStatusBar(self))

        menu = self.menuBar()

        file_menu = menu.addMenu("&File")
        file_menu.addAction(button_action)

    def onMyToolBarButtonClick(self, s):
        print("click", s)
```

- Define a keyboard shortcut by passing setKeySequence() and passing in the key sequence.

```python
button_action.setShortcut(QKeySequence("Ctrl+p"))
```
