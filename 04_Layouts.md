# Layouts

- There are 4 basic layouts available in Qt
  - QHBoxLayout
  - QVBoxLayout
  - QGridLayout -> In indexable grid XxY
  - QStackedLayout -> Stacked (z) in front of one another
    - can control which widget to show at any time by using .setCurrentIndex() or .setCurrentWidget()

## TabWidget

- provide a built-in TabWidget that provides this kind of layout out of the box - albeit in widget form.
- For documents, you can turn on document mode to give slimline tabs similar to what you see on other platforms.

```py
tabs = QTabWidget()
tabs.setDocumentMode(True)
```
