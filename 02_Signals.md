# Signals

- [Signals](#signals)
  - [Signals \& Slots](#signals--slots)
  - [Receiving data](#receiving-data)
  - [Storing data](#storing-data)
  - [Changing the interface](#changing-the-interface)
  - [Connecting widgets together directly](#connecting-widgets-together-directly)
  - [Events](#events)
    - [QMouseEvent](#qmouseevent)
  - [Context menus](#context-menus)
  - [Python inheritance forwarding](#python-inheritance-forwarding)
  - [Layout forwarding](#layout-forwarding)

## Signals & Slots

- Signals are notifications emitted by widgets when something happens.
- Signals are a neat feature of Qt that allow you to pass messages between different components in your applications.
- signals can also send data to provide additional context about what happened.
- Slots is the name Qt uses for the receivers of signals.
- In Python any function (or method) in your application can be used as a slot. Like eventHandler

```python
import sys
from PyQt6.QtWidgets import QApplication, QMainWindow, QPushButton
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("My App")
        button = QPushButton("Press Me!")
        button.setCheckable(True)
        button.clicked.connect(self.the_button_was_clicked)
        self.setCentralWidget(button)

    def the_button_was_clicked(self):
        print("Clicked!")
app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

## Receiving data

```python
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("My App")
        button = QPushButton("Press Me!")
        button.setCheckable(True)
        button.clicked.connect(self.the_button_was_clicked)
        button.clicked.connect(self.the_button_was_toggled)
        self.setCentralWidget(button)

    def the_button_was_clicked(self):
        print("Clicked!")

    def the_button_was_toggled(self, checked):
        print("Checked?", checked)
```

## Storing data

- In the next example we store the checked value of our button in a variable called button_is_checked on self.

```python
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.button_is_checked = True
        self.setWindowTitle("My App")
        button = QPushButton("Press Me!")
        button.setCheckable(True)
        button.clicked.connect(self.the_button_was_toggled)
        button.setChecked(self.button_is_checked)
        self.setCentralWidget(button)

    def the_button_was_toggled(self, checked):
        self.button_is_checked = checked

        print(self.button_is_checked)
```

## Changing the interface

- method to modify the button, changing the text and disabling the button so it is no longer clickable. We'll also turn off the checkable state for now.

```python
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("My App")
        self.button = QPushButton("Press Me!")
        self.button.clicked.connect(self.the_button_was_clicked)
        self.setCentralWidget(self.button)

    def the_button_was_clicked(self):
        self.button.setText("You already clicked me.")
        self.button.setEnabled(False)
        self.setWindowTitle("My Oneshot App")
```

## Connecting widgets together directly

- In the following example, we add a QLineEdit widget and a QLabel to the window. In the \__init__ for the window we connect our line edit .textChanged signal to the .setText method on the QLabel. Now any time the text changes in the QLineEdit the QLabel will receive that text to it's .setText method.

```python
from PyQt6.QtWidgets import QApplication, QMainWindow, QLabel, QLineEdit, QVBoxLayout, QWidget
import sys
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("My App")
        self.label = QLabel()
        self.input = QLineEdit()
        self.input.textChanged.connect(self.label.setText)
        layout = QVBoxLayout()
        layout.addWidget(self.input)
        layout.addWidget(self.label)
        container = QWidget()
        container.setLayout(layout)
        self.setCentralWidget(container)
app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

- [qlabel public slots](https://doc.qt.io/qt-5/qlabel.html#public-slots)

## Events

- Every interaction the user has with a Qt application is an event.
- Qt represents these events using event objects which package up information about what happened.
- These events are passed to specific event handlers on the widget where the interaction occurred.

### QMouseEvent

- QMouseEvent events are created for each and every mouse movement and button click on a widget.
  - mouseMoveEvent
  - mousePressEvent
  - mouseReleaseEvent
  - mouseDoubleClickEvent

```python
import sys
from PyQt6.QtCore import Qt
from PyQt6.QtWidgets import QApplication, QLabel, QMainWindow, QTextEdit

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.label = QLabel("Click in this window")
        self.setCentralWidget(self.label)

    def mouseMoveEvent(self, e):
        self.label.setText("mouseMoveEvent")

    def mousePressEvent(self, e):
        self.label.setText("mousePressEvent")

    def mouseReleaseEvent(self, e):
        self.label.setText("mouseReleaseEvent")

    def mouseDoubleClickEvent(self, e):
        self.label.setText("mouseDoubleClickEvent")

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

- self.setMouseTracking(True) will register event if the press (click) and double-click.
- Typically to register a click from a user we should watch for both the mouse down and the release.
- **Methods**
  - .button() -> Specific button that triggered this event
  - .buttons() -> State of all mouse buttons (OR'ed flags)
  - .position() -> Widget-relative position as a QPoint integer (provide both global and local (widget-relative) position)

```python
def mousePressEvent(self, e):
        if e.button() == Qt.MouseButton.LeftButton:
            # handle the left-button press in here
            self.label.setText("mousePressEvent LEFT")

        elif e.button() == Qt.MouseButton.MiddleButton:
            # handle the middle-button press in here.
            self.label.setText("mousePressEvent MIDDLE")

        elif e.button() == Qt.MouseButton.RightButton:
            # handle the right-button press in here.
            self.label.setText("mousePressEvent RIGHT")
```

## Context menus

- This event is fired whenever a context menu is about to be shown,

```python
import sys
from PyQt6.QtCore import Qt
from PyQt6.QtGui import QAction
from PyQt6.QtWidgets import QApplication, QLabel, QMainWindow, QMenu

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

    def contextMenuEvent(self, e):
        context = QMenu(self)
        context.addAction(QAction("test 1", self))
        context.addAction(QAction("test 2", self))
        context.addAction(QAction("test 3", self))
        context.exec(e.globalPos())

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

## Python inheritance forwarding

- If your object is inherited from a standard widget, it will likely have sensible behavior implemented by default.
- You can trigger this by calling up to the parent implementation using super().

```python
def mousePressEvent(self, event):
    print("Mouse pressed!")
    super().mousePressEvent(event)
```

## Layout forwarding

- In your own event handlers you can choose to mark an event as handled calling .accept()

```python
 class CustomButton(QPushButton)
        def mousePressEvent(self, e):
            e.accept()
```

- Alternatively, you can mark it as unhandled by calling .ignore() on the event object. In this case the event will continue to bubble up the hierarchy.

```py
 class CustomButton(QPushButton)
        def event(self, e):
            e.ignore()
```
