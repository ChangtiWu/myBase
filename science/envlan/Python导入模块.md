导入模块有两种常用方法：`import`语句和`from … import`语句。

### 1 import语句

import语句会导入指定模块中所有的方法，当你需要大量使用该模块中的不同方法时，这种方式很适合你。

```python
import 模块名
```

此时，当你使用该模块中的方法，则需要在方法名前面加上模块名的前缀。

```py
import math
math.pow(2,4) 
```

### 2 from...import语句

如果你只需要使用某个模块中的少数方法，推荐使用from…import语句导入相应的模块。

```python
from 模块名 import 方法名
```

此时，当你调用模块中的方法时，就不需要在方法名前面添加模块名的前缀。

```python
from math import pow, log
pow(2,4)
log(32,2)
```

如果使用`from 模块名 import *`，则表示导入该模块中所有的方法。

```python
from math import *
pow(2,4)
```

>注：使用单下划线“_”开头的模块变量或者函数是受保护的，在使用 from xxx import * 语句从模块中导入时这些变量或者函数不能被导入。

**但是，这种用法有两个坑。**

1. 正常我们只需看一下文件开头的import语句，就能清楚地知道Python代码中使用了哪些类，干净整洁，如果使用`from xxx import *`语句则会丢失该优点。

2. 引发名称方面的困惑。假如现在Python代码中要用到两个模块kxpython1和kxpython2，而这两个模块都有test()函数，如果正常import语句并不会出现什么问题。

   ```python
   import kxpython1
   import kxpython2
   
   kxpython1.test(123456)
   kxpython2.test(123456)
   ```

   但是如果使用`from xxx import *`语句，就芭比Q了。

   在交互式环境中输入如下命令：

   ```python
   from kxpython1 import *
   from kxpython2 import *
   
   test(123456)
   ```

   你猜这时候，test()函数用的是哪个模块？？？

   所以，自然会报错了。

### 3 别名

有时候，当你导入的模块名太长，可为它指定一个别名。别名是模块的另一个名称，类似于外号，语法格式如下所示。

```python
import pandas as pd
```

