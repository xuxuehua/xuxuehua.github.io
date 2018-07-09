---
title: "os"
date: 2018-07-02 18:06
collection: Python 模块
---



# OS 模块



## system (deprecate)

执行命令，不保存结果

```
import os
print(os.system('ls'))   
```



## popen

可以保存执行结果，必须通过read方法处理

```
import os
cmd_result = os.open('ls').read()
print(cmd_result)
```



## mkdir

创建目录

```
import os
os.mkdir('mydir')
```

