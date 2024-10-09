# Widgets

- widget is the name given to a component of the UI that the user can interact with.
  - QLabel
    - a simple one-line piece of text
    - you can also use QLabel to display an image using .setPixmap()
  - QCheckBox
    - checkable box to the user
  - QComboBox
    - drop down list
    - QComboBox can also be editable using .setEditable(True)
  - QListWidget
    - options are presented as a scrollable list of items.
    - supports selection of multiple items at once.
  - QLineEdit
    - a simple single-line text editing box, into which users can type input.
  - QSpinBox and QDoubleSpinBox
    - a small numerical input box with arrows to increase and decrease the value.
    - QDoubleSpinBox supports floats
  - QSlider
    - provides a slide-bar widget
  - QDial
    - is a rotatable widget that functions just like the slider.

- Detailed notes [QWidgets](QtWidgets.md)

```py
import sys
from PyQt6.QtCore import Qt
from PyQt6.QtWidgets import (
    QApplication,
    QLabel,
    QMainWindow,
)

class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setWindowTitle("My App")
        widget = QLabel("Hello")
        font = widget.font()
        font.setPointSize(30)
        widget.setFont(font)
        widget.setAlignment(Qt.AlignmentFlag.AlignHCenter | Qt.AlignmentFlag.AlignVCenter)
        self.setCentralWidget(widget)

app = QApplication(sys.argv)
w = MainWindow()
w.show()
app.exec()
```
