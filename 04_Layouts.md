# Layouts

- There are 4 basic layouts available in Qt
  - QHBoxLayout
  - QVBoxLayout
  - QGridLayout -> In indexable grid XxY
  - QStackedLayout -> Stacked (z) in front of one another
    - can control which widget to show at any time by using .setCurrentIndex() or .setCurrentWidget()

## Examples

### QHBoxLayout or QVBoxLayout

```py
import sys
from PyQt6.QtWidgets import QApplication, QMainWindow, QWidget, QVBoxLayout, QHBoxLayout
from PyQt6.QtGui import QPalette, QColor

class Color(QWidget):
    def __init__(self, color):
        super(Color, self).__init__()
        self.setAutoFillBackground(True)

        palette = self.palette()
        palette.setColor(QPalette.ColorRole.Window, QColor(color))
        self.setPalette(palette)

class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setWindowTitle("My App")
        # layout = QVBoxLayout()
        layout = QHBoxLayout()
        layout.addWidget(Color('red'))
        layout.addWidget(Color('green'))
        layout.addWidget(Color('blue'))
        widget = QWidget()
        widget.setLayout(layout)
        self.setCentralWidget(widget)

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

### QGridLayout

```py
import sys
from PyQt6.QtWidgets import QApplication, QMainWindow, QWidget, QGridLayout
from PyQt6.QtGui import QPalette, QColor
class Color(QWidget):
    def __init__(self, color):
        super(Color, self).__init__()
        self.setAutoFillBackground(True)

        palette = self.palette()
        palette.setColor(QPalette.ColorRole.Window, QColor(color))
        self.setPalette(palette)

class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setWindowTitle("My App")
        layout = QGridLayout()
        layout.addWidget(Color('red'), 0, 0)
        layout.addWidget(Color('green'), 1, 0)
        layout.addWidget(Color('blue'), 1, 1)
        layout.addWidget(Color('purple'), 2, 1)
        widget = QWidget()
        widget.setLayout(layout)
        self.setCentralWidget(widget)

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

### QStackedLayout

```py
import sys
from PyQt6.QtWidgets import QApplication, QMainWindow, QWidget, QStackedLayout
from PyQt6.QtGui import QPalette, QColor

class Color(QWidget):
    def __init__(self, color):
        super(Color, self).__init__()
        self.setAutoFillBackground(True)
        palette = self.palette()
        palette.setColor(QPalette.ColorRole.Window, QColor(color))
        self.setPalette(palette)

class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setWindowTitle("My App")
        layout = QStackedLayout()
        layout.addWidget(Color("red"))
        layout.addWidget(Color("green"))
        layout.addWidget(Color("blue"))
        layout.addWidget(Color("yellow"))
        layout.setCurrentIndex(3)
        widget = QWidget()
        widget.setLayout(layout)
        self.setCentralWidget(widget)

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

## TabWidget

- provide a built-in TabWidget that provides this kind of layout out of the box - albeit in widget form.
- For documents, you can turn on document mode to give slimline tabs similar to what you see on other platforms.

```py
tabs = QTabWidget()
tabs.setDocumentMode(True)
```
