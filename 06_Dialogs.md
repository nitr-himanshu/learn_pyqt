# Dialogs

- Dialogs are useful GUI components that allow you to communicate with the user (hence the name dialog).
- They are small modal (or blocking) windows that sit in front of the main application until they are dismissed.
- To create a new dialog box simply create a new object of QDialog type passing in another widget, e.g. QMainWindow, as its parent.

```python
import sys
from PyQt6.QtWidgets import QApplication, QDialog, QMainWindow, QPushButton

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("My App")
        button = QPushButton("Press me for a dialog!")
        button.clicked.connect(self.button_clicked)
        self.setCentralWidget(button)

    def button_clicked(self, s):
        print("click", s)
        dlg = QDialog(self)
        dlg.setWindowTitle("HELLO!")
        dlg.exec()

app = QApplication(sys.argv)
window = MainWindow()
window.show()
app.exec()
```

## Reference

[pyqt6-dialogs](https://www.pythonguis.com/tutorials/pyqt6-dialogs/)
