# python 中 import 的用法

在





在 Python 中，`import` 是用来**引入外部代码**（模块或包）的关键字。通过它，你可以复用标准库、第三方库或自己写的代码，而不必从头造轮子。

下面从基本到进阶，系统介绍它的用法。

------

### 1. 基础导入方式

假设有一个模块文件 `math_tools.py`，里面定义了一个函数 `add` 和一个变量 `PI = 3.14`。

#### ① 导入整个模块

python

```
import math_tools
print(math_tools.add(2, 3))   # 需要通过模块名.成员 来访问
print(math_tools.PI)
```



模块名变成了一个命名空间，可以避免名字冲突。

#### ② 导入并起别名

python

```
import math_tools as mt       # 用 as 起个短名
print(mt.add(2, 3))
```



常用于简化长模块名，如 `import numpy as np`、`import pandas as pd`。

#### ③ 从模块中导入特定成员

python

```
from math_tools import add, PI
print(add(2, 3))   # 直接用函数名，不用模块前缀
print(PI)
```



直接导入的名字可能和当前代码中变量冲突，需要谨慎。

#### ④ 导入模块中的所有公开成员（不推荐）

python

```
from math_tools import *
print(add(2, 3))
```



这会把模块里所有不以 `_` 开头的名字全部引入当前命名空间，容易污染命名空间且难以追溯，**一般不建议使用**。

------

### 2. 导入包和子模块

包就是一个包含 `__init__.py` 文件的文件夹，里面可以有多层模块。

text

```
my_package/
    __init__.py
    utils.py
    models/
        __init__.py
        linear.py
```



- 导入包中的模块：

python

```
import my_package.utils
my_package.utils.some_func()

from my_package import utils
utils.some_func()
```



- 导入子包中的模块：

python

```
from my_package.models import linear
linear.train()
```



------

### 3. import 的执行机制

当你执行 `import` 时，Python 会做三件事：

1. **搜索**：在 `sys.path` 中的路径里寻找对应模块或包。
2. **加载**：找到后，运行该模块的全部代码（定义函数、变量等）。
3. **缓存**：把模块对象存到 `sys.modules` 字典里。下次再导入同一模块时，直接取缓存，**不会重复执行**。

这就是为什么一个模块的顶层代码只会执行一次。

------

### 4. 相对导入（在包内部使用）

在包内部，一个模块想导入同包下的其他模块，可以用 `.` 和 `..`：

python

```
# 在 my_package/models/linear.py 中
from . import utils          # 导入同级包 my_package 下的 utils
from .. import tools         # 导入上一级 my_package 下的 tools
```



相对导入**只能用在包内**，不能直接运行一个包含相对导入的脚本（会报错）。

------

### 5. `if __name__ == "__main__"`

模块本身既可以作为脚本直接运行，也可以被别人导入。区分方式：

python

```
# my_module.py
def greet():
    print("Hello")

if __name__ == "__main__":
    greet()    # 当直接运行 python my_module.py 时执行
```



- 直接运行时，`__name__` 为 `"__main__"`，会调用 `greet()`。
- 被导入时，`__name__` 为模块名 `"my_module"`，`greet()` 不会自动执行。

这个习惯让模块既能做脚本也能做库。

------

### 6. 常见导入惯例与最佳实践

- **导入顺序建议**：标准库 → 第三方库 → 本地模块，中间用空行隔开。例如：

python

```
import os
import sys

import numpy as np
from sklearn.linear_model import LinearRegression

import my_local_module
```



- **避免循环导入**：A 导入 B，B 又导入 A，会导致错误。解决方法是重构设计，或在函数内部延迟导入。
- **不要使用 import \***，除非在交互式环境或者库明确设计了 `__all__` 列表。
- **使用别名**提高可读性，如 `import matplotlib.pyplot as plt`。

------

### 7. 结合你之前遇到的例子

python

```
from sklearn.feature_selection import VarianceThreshold
import pandas as pd
import numpy as np
```



- 第一行从 `sklearn` 包的 `feature_selection` 模块中**只导入** `VarianceThreshold` 这一个类。
- 后两行分别导入 `pandas` 和 `numpy` 库，并用约定俗成的别名 `pd` 和 `np` 方便调用。

掌握了这些 `import` 的用法，你就可以灵活组织代码、充分利用 Python 庞大的生态了。