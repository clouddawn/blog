# python 中 import 的用法

在 Python 中， `import` 是用来引入外部代码（模块或包）的关键字。通过它，你可以复用标准库、第三方库和自己写的代码，而不必从头造轮子。

## 基础导入方式

假设有一个模块文件 `math_tools.py`，里面定义了一个函数 `add` 和一个变量 `PI = 3.14`。

### 1. 导入整个模块

```python
import math_tools
print(math_tools.add(2, 3)) # 
print(math_tools.PI)
```

模块名变成了一个命名空间，可以避免名字冲突。

### 2. 导入并起别名

```python
import math_tools as mt  # 用 as 起个短名
print(mt.add(2, 3))
```

常用于简化长模块名，如 `import numpy as np` 、`import pandas as pd`。

### 3. 从模块中导入特定成员

```python
from math_tools import add, PI
print(add(2, 3)) # 直接用函数名，不用模块前缀
print(PI)
```

直接导入的名字可能和当前代码中变量冲突，需要谨慎。

## 导入包合子模块

包就是一个包含 `__init__.py` 文件的文件夹，里面可以有多层模块。

```text
my_package/
    __init__.py
    utils.py
    models/
        __init__.py
        linear.py
```

### 1. 导入包中的模块

```python
import my_package.utils
my_package.utils.some_func()

from my_package import utils
utils.some_func()
```

### 2. 导入子包中的模块

```python
from my_package.models import linear
linear.train()
```

## import 的执行机制

当你执行 `import` 时，Python 会做三件事：

* 搜索：在 `sys.path` 中的路径里寻找对应模块或包。
* 加载：找到后，运行该模块的全部代码（定义函数、变量等）。
* 缓存：把模块对象存到 `sys.modules` 字典里。下次再导入同一模块时，直接取缓存，不会重复执行。

这就是为什么一个模块的顶层代码只会执行一次。