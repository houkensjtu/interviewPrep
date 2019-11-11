# Python GUI programming

## Pythonic GUI Tutorial \(PyQt5\)

#### 一个最简单的app

```python
import sys

# 1. Import `QApplication` and all the required widgets
from PyQt5.QtWidgets import QApplication
from PyQt5.QtWidgets import QLabel
from PyQt5.QtWidgets import QWidget

# 2. Create an instance of QApplication
app = QApplication(sys.argv)

# 3. Create an instance of your application's GUI
window = QWidget()
window.setWindowTitle("PyQt5 App")
window.setGeometry(100, 100, 280, 80)
window.move(60, 15)
helloMsg = QLabel("<h1>Hello World!</h1>", parent=window)
helloMsg.move(60, 15)

# 4.Show your application's GUI
window.show()

# 5. Run your application's event loop (or main loop)
sys.exit(app.exec_())

```

#### 基本的widget类

* PyQt5.QtWidgets -&gt; QApplication: App的雏形;

```python
app = QApplication(sys.argv)
app.exec_()
```

* PyQt5.QtWidgets -&gt; QWidget: 基本窗口

```python
window = QWidget()
window.show()
```

* PyQt5.QtWidgets -&gt; QLabel: 文字框

```python
label = QLabel("Hello Leah!", parent = window)
```

* PyQt5.QtWidgets -&gt; QPushButton: 按钮
* PyQt5.QtWidgets -&gt; QHBoxLayout, QVBoxLayout, QGridLayout, QFormLayout

  ```python
  from PyQt5.QtWidgets import QHBoxLayout

  window = QtWidget()
  layout = QHBoxLayout
  layout.addWidget(QPushButton("Button 1"))
  layout.addWidget(QPushButton("Button 2"))

  window.setLayout(layout)

  layout = QGridLayout()

  layout.addWidget(QPushButton('Button (0, 0)'), 0, 0)
  layout.addWidget(QPushButton('Button (0, 1)'), 0, 1)
  layout.addWidget(QPushButton('Button (0, 2)'), 0, 2)
  layout.addWidget(QPushButton('Button (1, 0)'), 1, 0)
  layout.addWidget(QPushButton('Button (1, 1)'), 1, 1)
  layout.addWidget(QPushButton('Button (1, 2)'), 1, 2)
  layout.addWidget(QPushButton('Button (2, 0)'), 2, 0)
  layout.addWidget(QPushButton('Button (2, 1) + 2 Columns Span'), 2, 1, 1, 2)
  window.setLayout(layout)

  ```

